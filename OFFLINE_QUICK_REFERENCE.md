# Offline Features - Quick Reference Guide

## 🚀 Quick Start

Your app now works completely offline! Here's what you can do:

## 📱 Installing the App

### Desktop (Chrome/Edge)
1. Look for the install icon (⊕) in the address bar
2. Click it and select "Install"
3. The app opens in its own window

### Android
1. Open menu (⋮) → "Install app" or "Add to Home screen"
2. Confirm installation
3. Find the app icon on your home screen

### iOS
1. Tap the Share button (□↑)
2. Select "Add to Home Screen"
3. Tap "Add"

## 🌐 Working Offline

### What Works Offline?
- ✅ Downloaded playlists
- ✅ Cached emotion history
- ✅ Offline emotion detection (camera)
- ✅ Saved preferences
- ✅ Previously visited pages
- ✅ Making changes (queued for sync)

### What Requires Internet?
- ❌ New playlist generation
- ❌ Social features (sharing, following)
- ❌ Real-time tracking
- ❌ Discovering new playlists

## 💾 Downloading Playlists

1. Go to any playlist page
2. Click the "Download" button
3. Wait for progress bar to complete
4. Playlist is now available offline!

**To Remove:**
- Click the "Downloaded" button on any saved playlist

## 📊 Checking Connection Status

Look at the top navigation bar:
- 🟢 **Green Badge** = Online
- 🟡 **Yellow Badge** = Offline
- **Number** = Queued requests waiting to sync

Click the badge to see:
- Storage usage
- Sync status
- Offline features available

## 🔄 Syncing When Back Online

Sync happens automatically, but you can also:
1. Click the connection status badge
2. Click "Sync Now" button
3. Your changes upload immediately

## 🧠 Offline Emotion Detection

When offline, the camera still works!
1. Go to the Camera page
2. Allow camera access
3. Emotion detection runs on your device
4. Results save locally and sync when online

## 💡 Tips & Tricks

### Save Storage Space
- Only download playlists you'll listen to offline
- Check storage usage in the connection badge
- Remove old downloaded playlists

### Best Offline Experience
1. Download your favorite playlists before going offline
2. Visit pages you want available while still online
3. The app caches recently visited pages automatically

### Installing on Multiple Devices
- Install on phone for on-the-go listening
- Install on desktop for full experience
- Sync happens across all devices when online

## 🔧 Troubleshooting

### "Install" Button Not Showing?
- Wait 30 seconds after opening the app
- Interact with the app (click around)
- Check if already installed

### Downloaded Playlist Won't Play Offline?
- Ensure download completed (check for "Downloaded" badge)
- Check storage quota hasn't been exceeded
- Try re-downloading the playlist

### Changes Not Syncing?
- Check connection status (should be green/online)
- Click "Sync Now" in the status dropdown
- Check if storage quota is exceeded

### App Won't Load Offline?
- Ensure you visited the page at least once while online
- Check if service worker is active (DevTools → Application)
- Clear browser cache and reload while online

## 📈 Storage Management

### Checking Usage
1. Click connection status badge in nav bar
2. View storage bar showing used/available space

### Freeing Up Space
- Remove downloaded playlists you don't need
- Clear cache in browser settings
- Offline data is prioritized over cache

### Storage Limits
- Browser automatically manages storage
- Typical limit: 50% of available disk space
- You'll be warned before running out

## 🎯 Common Scenarios

### Scenario: Commute/Flight
1. **Before leaving WiFi:**
   - Download 3-5 playlists for your mood
   - Let app cache your recent pages
   
2. **While offline:**
   - Browse downloaded playlists
   - Detect emotions with camera
   - Like/rate content (syncs later)
   
3. **When back online:**
   - Changes sync automatically
   - New recommendations load
   - Social updates appear

### Scenario: Low/Unstable Connection
1. **App handles this automatically:**
   - Uses cached content when possible
   - Queues failed requests
   - Retries when connection improves
   
2. **You'll see:**
   - Yellow status badge
   - Queue count increasing
   - Auto-sync when stable

### Scenario: Fresh Install on New Device
1. **First time opening:**
   - App downloads and caches core files
   - Service worker registers
   - Install prompt may appear after 30s
   
2. **To prepare for offline:**
   - Browse the app while online
   - Download favorite playlists
   - Visit pages you want offline

## 🔔 Notifications

### Install Prompt
- Appears after 30 seconds of use
- Can dismiss (won't show for 7 days)
- Shows app benefits

### Update Available
- Shows when new version detected
- Click "Update Now" to get latest
- App reloads with new version

## 🎨 App Shortcuts (After Install)

Right-click app icon (desktop) or long-press (mobile):
- **Detect Emotion** - Opens camera directly
- **My Playlists** - Opens your playlists page

## ⚡ Performance Tips

### Faster Loading
- App loads faster after first visit (cached)
- Downloaded playlists load instantly
- Recent pages open from cache

### Smooth Experience
- Cache refreshes in background when online
- Old cache cleaned automatically
- Storage managed efficiently

## 🆘 Getting Help

### Check Connection Status
- Badge color indicates online/offline
- Click for detailed status

### View Queued Changes
- Click connection badge
- See pending sync count
- Manual sync available

### Storage Issues
- Check usage in status dropdown
- Free up space by removing downloads
- Browser may prompt to increase quota

## 📱 Platform-Specific Notes

### iOS
- Add to home screen manually (no automatic prompt)
- Works great once installed
- Notifications not supported

### Android
- Full PWA support with install banner
- Background sync works great
- Notifications fully supported

### Desktop
- Install from address bar icon
- Runs in separate window
- Full keyboard shortcuts

## 🎉 You're Ready!

Your app now works offline with:
- ✅ Installable on any device
- ✅ Downloaded playlists for offline listening
- ✅ Offline emotion detection
- ✅ Automatic sync when back online
- ✅ Smart caching for fast loading

Enjoy your music anywhere, anytime! 🎵
