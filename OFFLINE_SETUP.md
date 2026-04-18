# Offline Capabilities Implementation

This document provides instructions for completing the offline PWA implementation.

## 📦 Required Dependencies

Install TensorFlow.js for offline emotion detection:

```bash
npm install @tensorflow/tfjs @tensorflow/tfjs-backend-webgl
```

## 🎨 App Icons

Generate app icons for PWA. You need to create icons in the following sizes and place them in `frontend/public/icons/`:

### Required Icon Sizes:
- `icon-72x72.png`
- `icon-96x96.png`
- `icon-128x128.png`
- `icon-144x144.png`
- `icon-152x152.png`
- `icon-192x192.png`
- `icon-384x384.png`
- `icon-512x512.png`

### Icon Generation Options:

**Option 1: Using Online Tool**
1. Create a base icon (512x512 recommended)
2. Use https://realfavicongenerator.net/ or https://www.pwabuilder.com/imageGenerator
3. Upload your base icon
4. Download generated icon set
5. Place in `frontend/public/icons/`

**Option 2: Using ImageMagick (CLI)**
```bash
# Install ImageMagick first
# On Windows: choco install imagemagick
# On macOS: brew install imagemagick

# Convert base icon to all sizes
convert base-icon.png -resize 72x72 icon-72x72.png
convert base-icon.png -resize 96x96 icon-96x96.png
convert base-icon.png -resize 128x128 icon-128x128.png
convert base-icon.png -resize 144x144 icon-144x144.png
convert base-icon.png -resize 152x152 icon-152x152.png
convert base-icon.png -resize 192x192 icon-192x192.png
convert base-icon.png -resize 384x384 icon-384x384.png
convert base-icon.png -resize 512x512 icon-512x512.png
```

**Option 3: Using npm package**
```bash
npm install -g pwa-asset-generator

# Generate all icons
pwa-asset-generator base-icon.png ./public/icons --icon-only --path-override /icons
```

## 🧠 Emotion Detection Model

The offline emotion detector needs a pre-trained model. You have two options:

### Option 1: Use the Built-in Simple Model (Default)
The `offlineEmotionDetector.ts` will create a basic model automatically. No additional setup needed, but accuracy will be limited.

### Option 2: Use a Pre-trained Model (Recommended)
1. Download a pre-trained emotion detection model (e.g., from TensorFlow Hub)
2. Place the model files in `frontend/public/models/emotion-model/`
3. The folder should contain:
   - `model.json` - Model architecture
   - `group1-shard1of1.bin` (or similar) - Model weights

**Recommended Model Sources:**
- [FER-2013 Emotion Recognition Model](https://github.com/oarriaga/face_classification)
- [TensorFlow.js Models](https://github.com/tensorflow/tfjs-models)

## 🚀 Testing Offline Functionality

1. **Build the app:**
   ```bash
   npm run build
   npm run preview
   ```

2. **Test Service Worker:**
   - Open DevTools → Application → Service Workers
   - Verify service worker is active
   - Check "Offline" checkbox
   - Navigate app to ensure offline functionality

3. **Test IndexedDB:**
   - Open DevTools → Application → IndexedDB
   - Verify `emotion-music-db` database exists
   - Check object stores: playlists, tracks, emotions, queue, preferences, cache-meta

4. **Test Offline Queue:**
   - Go offline (DevTools → Network → Offline)
   - Perform actions (like, comment, etc.)
   - Go back online
   - Verify queued requests sync automatically

5. **Test PWA Installation:**
   - Chrome: Look for install icon in address bar
   - Edge: Click "App available" in address bar
   - Mobile: Look for "Add to Home Screen" prompt

## 📱 Platform-Specific Testing

### iOS Safari
- PWA installation via "Share → Add to Home Screen"
- Test offline mode in standalone mode
- Verify apple-touch-icons display correctly

### Android Chrome
- Look for install banner
- Test offline functionality
- Verify maskable icons work correctly

### Desktop Chrome/Edge
- Click install icon in omnibox
- Test as installed app
- Verify shortcuts work

## 🎯 Features Checklist

- [x] Service Worker with cache strategies
- [x] PWA manifest.json
- [x] Offline fallback page
- [x] IndexedDB storage layer
- [x] Offline queue manager
- [x] TensorFlow.js emotion detector (code ready, needs model)
- [x] Offline indicator component
- [x] Download playlist button
- [x] PWA install prompt
- [x] Service worker update notification
- [x] Service worker registration
- [ ] App icons (need generation)
- [ ] Emotion detection model (optional, has fallback)

## 🔧 Troubleshooting

### Service Worker Not Registering
- Check browser console for errors
- Ensure app is served over HTTPS (or localhost)
- Clear browser cache and reload

### IndexedDB Errors
- Check browser storage quota
- Try clearing IndexedDB in DevTools
- Verify browser supports IndexedDB

### Offline Detection Not Working
- Check if model files are accessible
- Verify TensorFlow.js is loaded
- Check console for loading errors

### Install Prompt Not Showing
- Verify manifest.json is accessible
- Check manifest validation in DevTools
- Ensure icons are correct sizes
- May need user interaction before prompt appears

## 🎨 Customization

### Change Theme Color
Edit `manifest.json` and `index.html`:
```json
"theme_color": "#9333ea"
```

### Modify Cache Strategy
Edit `service-worker.js` cache handling functions.

### Adjust Storage Limits
Edit `offlineDB.ts` to change cache TTL and limits.

## 📚 Resources

- [PWA Documentation](https://web.dev/progressive-web-apps/)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
- [IndexedDB Guide](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)
- [TensorFlow.js](https://www.tensorflow.org/js)
- [Workbox (Advanced SW)](https://developers.google.com/web/tools/workbox)
