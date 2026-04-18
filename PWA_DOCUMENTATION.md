# PWA & Offline Capabilities - Complete Documentation

## 📋 Overview

The Emotion-Aware Music Recommendation Engine now includes complete Progressive Web App (PWA) capabilities with comprehensive offline support. Users can install the app, use it offline, download playlists, and perform offline emotion detection.

## 🌟 Key Features

### Progressive Web App (PWA)
- ✅ **Installable** - Add to home screen on mobile and desktop
- ✅ **Standalone Mode** - Runs like a native app
- ✅ **App Shortcuts** - Quick access to camera and playlists
- ✅ **Share Target** - Receive shared content from other apps
- ✅ **Custom Protocol** - Handle `web+emotionmusic://` URLs

### Offline Support
- ✅ **Service Worker Caching** - Intelligent cache-first and network-first strategies
- ✅ **IndexedDB Storage** - Local storage for playlists, tracks, emotions
- ✅ **Offline Queue** - Queue API calls when offline, sync when online
- ✅ **Offline Emotion Detection** - Client-side AI using TensorFlow.js
- ✅ **Download Playlists** - Save playlists for offline listening
- ✅ **Offline Indicator** - Real-time connection status display

### User Experience
- ✅ **Install Prompt** - Smart install banner after 30 seconds
- ✅ **Update Notifications** - Alert when new version available
- ✅ **Connection Status** - Visual indicator with queue count
- ✅ **Storage Management** - Display usage and quota
- ✅ **Offline Fallback** - Dedicated offline page with features list

## 🏗️ Architecture

### 1. Service Worker (`frontend/public/service-worker.js`)

**Caching Strategy:**
- **Static Assets**: Cache-first (HTML, CSS, JS, images)
- **API Calls**: Network-first with offline queue fallback

**Cache Management:**
```javascript
CACHE_NAME: 'emotion-music-v1'
RUNTIME_CACHE: 'emotion-music-runtime'
```

**Features:**
- Precaches critical assets on install
- Cleans up old caches on activate
- Queues failed POST/PUT/DELETE requests
- Background sync for queued requests
- Push notification support

**Event Handlers:**
- `install` - Cache static assets
- `activate` - Clean old caches
- `fetch` - Intercept requests, apply caching
- `sync` - Replay queued requests
- `message` - Handle commands (SKIP_WAITING, CACHE_URLS, CLEAR_CACHE)
- `push` - Display push notifications

### 2. IndexedDB Storage (`frontend/src/utils/offlineDB.ts`)

**Database:** `emotion-music-db` (Version 1)

**Object Stores:**

| Store | Purpose | Key | Indexes |
|-------|---------|-----|---------|
| `playlists` | Offline playlists | `id` | `emotion`, `downloaded` |
| `tracks` | Playlist tracks | `id` | `playlistId` |
| `emotions` | Emotion history | `id` (auto) | `timestamp`, `synced` |
| `queue` | Failed requests | `id` (auto) | - |
| `preferences` | User settings | `key` | - |
| `cache-meta` | Cache metadata | `url` | `expiry` |

**Key Methods:**

**Playlists:**
```typescript
savePlaylist(playlist) // Save with downloaded flag
getPlaylist(id) // Retrieve single playlist
getAllPlaylists() // Get all playlists
getDownloadedPlaylists() // Get offline-available playlists
deletePlaylist(id) // Remove from storage
```

**Tracks:**
```typescript
saveTrack(track) // Save track with playlistId
getPlaylistTracks(playlistId) // Get all tracks for playlist
```

**Emotions:**
```typescript
saveEmotion(emotion) // Save emotion detection result
getEmotions(limit) // Get recent emotions
getUnsyncedEmotions() // Get emotions not synced to server
markEmotionSynced(id) // Mark as synced
```

**Queue:**
```typescript
queueRequest(request) // Add failed API call
getQueuedRequests() // Get all queued
removeFromQueue(id) // Remove after sync
clearQueue() // Clear all
```

**Cache:**
```typescript
setCacheMeta(url, data, ttl) // Cache with TTL
getCacheMeta(url) // Get if not expired
```

### 3. Offline Queue Manager (`frontend/src/utils/offlineQueue.ts`)

**Purpose:** Handle API calls when offline and sync when connection restored.

**Features:**
- Monitors `online`/`offline` events
- Queues failed requests in IndexedDB
- Auto-syncs every 60 seconds when online
- Removes successful requests after sync
- Cleans up requests older than 7 days

**Usage:**
```typescript
import { offlineQueue } from '@/utils/offlineQueue';

// Queue a request when offline
await offlineQueue.queueRequest(url, method, data, headers);

// Listen to status changes
offlineQueue.onStatusChange((isOnline) => {
  console.log(`Connection: ${isOnline ? 'online' : 'offline'}`);
});

// Manual sync
await offlineQueue.syncQueue();

// Get queue count
const count = await offlineQueue.getQueueCount();

// Start auto-sync (60s interval)
offlineQueue.startAutoSync();
```

### 4. Offline Emotion Detector (`frontend/src/utils/offlineEmotionDetector.ts`)

**Purpose:** Client-side emotion detection using TensorFlow.js (no API calls needed).

**Model:**
- Attempts to load custom model from `/models/emotion-model/model.json`
- Falls back to simple CNN if custom model not found
- Input: 48x48 grayscale images
- Output: 7 emotions (angry, disgust, fear, happy, neutral, sad, surprise)

**Usage:**
```typescript
import { offlineEmotionDetector } from '@/utils/offlineEmotionDetector';

// Check if ready
if (offlineEmotionDetector.isReady()) {
  // Detect from video element
  const result = await offlineEmotionDetector.detectFromVideo(videoElement);
  
  // Detect from image data
  const result = await offlineEmotionDetector.detectFromImage(imageData);
  
  // Detect from base64
  const result = await offlineEmotionDetector.detectFromBase64(base64String);
}

// Result format:
{
  emotion: 'happy',
  confidence: 0.87,
  allPredictions: [
    { emotion: 'happy', confidence: 0.87 },
    { emotion: 'neutral', confidence: 0.08 },
    // ... other emotions
  ]
}
```

## 🎨 UI Components

### 1. Offline Indicator (`OfflineIndicator.tsx`)

**Features:**
- Real-time connection status (online/offline)
- Queued requests count badge
- Dropdown with details:
  - Connection status
  - Pending sync count with "Sync Now" button
  - Storage usage progress bar
  - Offline features list

**Props:**
```typescript
interface OfflineIndicatorProps {
  showDetails?: boolean; // Show dropdown on click
}
```

**Usage:**
```tsx
<OfflineIndicator showDetails />
```

### 2. Download Playlist Button (`DownloadPlaylistButton.tsx`)

**Features:**
- Download playlists for offline use
- Progress bar during download
- Visual confirmation when downloaded
- Remove from offline storage option

**Props:**
```typescript
interface DownloadPlaylistButtonProps {
  playlist: Playlist;
  onDownloadComplete?: () => void;
  className?: string;
}
```

**Usage:**
```tsx
<DownloadPlaylistButton 
  playlist={playlist}
  onDownloadComplete={() => console.log('Downloaded!')}
/>
```

### 3. PWA Install Prompt (`PWAInstallPrompt.tsx`)

**Features:**
- Automatic prompt after 30 seconds
- Dismissible (won't show again for 7 days)
- Lists app benefits:
  - Quick access from home screen
  - Works offline
  - Faster loading
- "Install App" and "Not Now" buttons

**Usage:**
```tsx
// Add to App.tsx (already integrated)
<PWAInstallPrompt />
```

### 4. Service Worker Update (`ServiceWorkerUpdate.tsx`)

**Features:**
- Detects when new service worker available
- Shows update notification at top of screen
- "Update Now" button to activate new version
- "Later" option to dismiss

**Usage:**
```tsx
// Add to App.tsx (already integrated)
<ServiceWorkerUpdate />
```

## 🚀 Getting Started

### 1. Install Dependencies

```bash
cd frontend
npm install @tensorflow/tfjs @tensorflow/tfjs-backend-webgl
```

### 2. Generate App Icons

Place icons in `frontend/public/icons/`:
- `icon-72x72.png`
- `icon-96x96.png`
- `icon-128x128.png`
- `icon-144x144.png`
- `icon-152x152.png`
- `icon-192x192.png`
- `icon-384x384.png`
- `icon-512x512.png`

Use online tool: https://realfavicongenerator.net/

### 3. (Optional) Add Emotion Detection Model

Place pre-trained model in `frontend/public/models/emotion-model/`:
- `model.json`
- Weight files (e.g., `group1-shard1of1.bin`)

If not provided, fallback simple model will be used.

### 4. Build and Test

```bash
# Development
npm run dev

# Production build
npm run build
npm run preview
```

### 5. Test PWA Features

1. **Service Worker:**
   - DevTools → Application → Service Workers
   - Verify "emotion-music-v1" is active

2. **Offline Mode:**
   - DevTools → Network → Set to "Offline"
   - Navigate app, verify cached content loads
   - Try downloading playlists

3. **Installation:**
   - Look for install prompt in browser
   - Click install icon in address bar
   - Test as standalone app

4. **IndexedDB:**
   - DevTools → Application → IndexedDB
   - Verify `emotion-music-db` database
   - Check object stores have data

## 📱 Platform Support

### Desktop
- ✅ Chrome 67+
- ✅ Edge 79+
- ✅ Opera 54+
- ✅ Brave
- ⚠️ Firefox (PWA support limited)
- ❌ Safari (no PWA installation)

### Mobile
- ✅ Android Chrome 67+
- ✅ Android Edge 79+
- ✅ iOS Safari 11.3+ (via Add to Home Screen)
- ✅ Android Opera 54+
- ✅ Samsung Internet 8.2+

## 🔧 Configuration

### Change Cache Names

Edit `frontend/public/service-worker.js`:
```javascript
const CACHE_NAME = 'emotion-music-v2'; // Increment version
```

### Adjust Auto-Sync Interval

Edit `frontend/src/utils/offlineQueue.ts`:
```typescript
startAutoSync(120000); // 2 minutes instead of 1
```

### Modify Storage TTL

Edit `frontend/src/utils/offlineDB.ts`:
```typescript
setCacheMeta(url, data, 7200000); // 2 hours in ms
```

### Change Theme Color

Edit `frontend/public/manifest.json`:
```json
"theme_color": "#6366f1" // Indigo instead of purple
```

## 🐛 Troubleshooting

### Service Worker Not Updating

1. Clear browser cache
2. Unregister service worker:
   ```javascript
   navigator.serviceWorker.getRegistrations().then(function(registrations) {
     for(let registration of registrations) {
       registration.unregister();
     }
   });
   ```
3. Hard refresh (Ctrl+Shift+R)

### IndexedDB Quota Exceeded

1. Check storage usage:
   ```typescript
   const estimate = await offlineDB.getStorageEstimate();
   console.log(estimate);
   ```
2. Clear old data:
   ```typescript
   await offlineDB.clearAll();
   ```
3. Request persistent storage:
   ```typescript
   await navigator.storage.persist();
   ```

### Offline Queue Not Syncing

1. Check online status:
   ```typescript
   console.log(navigator.onLine);
   ```
2. Verify queue has items:
   ```typescript
   const count = await offlineQueue.getQueueCount();
   console.log(`Queued: ${count}`);
   ```
3. Manual sync:
   ```typescript
   await offlineQueue.syncQueue();
   ```

### Install Prompt Not Showing

1. Verify manifest.json is accessible: `http://localhost:5173/manifest.json`
2. Check icons exist and are correct sizes
3. Ensure app is served over HTTPS (or localhost)
4. Check DevTools → Application → Manifest for errors
5. Wait 30 seconds or trigger user interaction

## 📊 Performance Optimization

### Reduce Cache Size

Edit `service-worker.js` to cache only essential assets:
```javascript
const STATIC_ASSETS = [
  '/',
  '/index.html',
  // Add only critical assets
];
```

### Implement Cache Expiration

Add TTL to runtime cache:
```javascript
async function networkFirstStrategy(request) {
  const cached = await caches.match(request);
  const cacheTime = cached?.headers.get('sw-cache-time');
  
  // Expire after 1 hour
  if (cacheTime && Date.now() - parseInt(cacheTime) > 3600000) {
    await caches.delete(request);
  }
  
  // ... rest of strategy
}
```

### Lazy Load TensorFlow.js

Only load when needed:
```typescript
let tf: any;

async function loadTensorFlow() {
  if (!tf) {
    tf = await import('@tensorflow/tfjs');
  }
  return tf;
}
```

## 🔒 Security Considerations

1. **HTTPS Required**: Service workers only work over HTTPS (except localhost)
2. **Content Security Policy**: Ensure CSP allows service worker scripts
3. **Storage Encryption**: IndexedDB is not encrypted - avoid storing sensitive data
4. **Cache Validation**: Verify cached responses haven't been tampered with
5. **Update Strategy**: Always provide update mechanism for security patches

## 📈 Analytics & Monitoring

Track offline usage:
```typescript
// In service-worker.js
self.addEventListener('fetch', (event) => {
  const isOffline = !navigator.onLine;
  
  if (isOffline) {
    // Log offline request
    console.log('Offline request:', event.request.url);
  }
});
```

Monitor cache size:
```typescript
async function getCacheSize() {
  const cacheNames = await caches.keys();
  let totalSize = 0;
  
  for (const name of cacheNames) {
    const cache = await caches.open(name);
    const requests = await cache.keys();
    
    for (const request of requests) {
      const response = await cache.match(request);
      const blob = await response.blob();
      totalSize += blob.size;
    }
  }
  
  return totalSize;
}
```

## 🎯 Best Practices

1. **Version Your Caches**: Increment `CACHE_NAME` on each deployment
2. **Limit Cache Size**: Don't cache large media files unnecessarily
3. **Test Offline First**: Always test offline functionality before deployment
4. **Provide Feedback**: Show users when they're offline and what's available
5. **Graceful Degradation**: Ensure app works without service worker
6. **Update Promptly**: Notify users of updates and encourage installation
7. **Monitor Quota**: Track storage usage and warn before quota exceeded
8. **Background Sync**: Use background sync for non-critical operations

## 📚 Additional Resources

- [PWA Checklist](https://web.dev/pwa-checklist/)
- [Service Worker Lifecycle](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle)
- [IndexedDB Best Practices](https://developers.google.com/web/ilt/pwa/working-with-indexeddb)
- [TensorFlow.js Guide](https://www.tensorflow.org/js/guide)
- [Workbox Library](https://developers.google.com/web/tools/workbox) - Advanced service worker library

## 🎉 Summary

Your Emotion-Aware Music Recommendation Engine now includes:

✅ **Full PWA Support** - Installable on all platforms
✅ **Complete Offline Functionality** - Works without internet
✅ **Intelligent Caching** - Fast loading with service worker
✅ **Offline AI** - Client-side emotion detection
✅ **Smart Sync** - Automatic queue management
✅ **Storage Management** - IndexedDB for persistence
✅ **Great UX** - Install prompts, update notifications, status indicators

The app provides a native-like experience while remaining a web application!
