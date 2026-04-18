# 🎵 Emotion-Aware Music Recommendation Engine - PWA Edition

A comprehensive Progressive Web App that recommends music based on your emotional state using AI-powered emotion detection. Now with **complete offline support**!

## ✨ Features

### 🎭 Emotion Detection
- **Camera-based detection** - Real-time facial emotion analysis
- **Text-based detection** - Natural language processing
- **Offline AI** - Client-side emotion detection using TensorFlow.js
- **Live tracking** - Real-time emotion monitoring with WebSocket

### 🎵 Music Recommendations
- **Emotion-based filtering** - Matches music to your mood
- **Collaborative filtering** - Learns from community preferences
- **Content-based filtering** - Analyzes track characteristics
- **Hybrid system** - Combines multiple recommendation strategies

### 👥 Social Features
- **Share playlists** - Generate shareable links with expiration
- **Follow users** - Build your music community
- **Public gallery** - Discover trending emotional playlists
- **Comments & ratings** - Engage with playlists (5-star system)
- **Collaborative playlists** - Create playlists with friends
- **Activity feed** - See what your network is listening to
- **Notifications** - Stay updated on social interactions

### 📱 Progressive Web App (NEW!)
- **✅ Installable** - Add to home screen on any device
- **✅ Works Offline** - Full functionality without internet
- **✅ Smart Caching** - Lightning-fast loading
- **✅ Auto-sync** - Changes sync when connection restored
- **✅ Push Notifications** - Stay engaged (Chrome/Edge)
- **✅ Native-like** - Runs like a real app

### 💾 Offline Capabilities (NEW!)
- **Download playlists** - Save for offline listening
- **Cached emotion history** - View past detections
- **Offline emotion detection** - Camera works without internet
- **Request queue** - Actions sync automatically when online
- **Storage management** - Monitor and control storage usage
- **Background sync** - Seamless data synchronization

### 📊 Analytics Dashboard
- **Emotion distribution** - Visualize your emotional patterns
- **Listening history** - Track your music journey
- **Social stats** - Followers, likes, shares
- **Interactive charts** - Powered by Recharts

## 🏗️ Architecture

### Frontend
- **React 18** + TypeScript
- **Redux Toolkit** - State management
- **React Router** - Navigation
- **Tailwind CSS** - Styling
- **Recharts** - Data visualization
- **Framer Motion** - Animations
- **Socket.io Client** - Real-time features
- **TensorFlow.js** - Offline AI
- **Service Worker** - PWA functionality
- **IndexedDB** - Offline storage

### Backend
- **Node.js** + Express
- **TypeScript** - Type safety
- **MongoDB** - Database
- **JWT** - Authentication
- **Socket.IO** - WebSocket
- **Mongoose** - ODM

## 📦 Installation

### Prerequisites
- Node.js 18+
- MongoDB 6+
- npm or yarn

### Backend Setup
```bash
cd backend
npm install
cp .env.example .env
# Edit .env with your configuration
npm run dev
```

### Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

## 🚀 Quick Start

1. **Start MongoDB**
   ```bash
   mongod --dbpath ./data/db
   ```

2. **Start Backend**
   ```bash
   cd backend
   npm run dev
   ```

3. **Start Frontend**
   ```bash
   cd frontend
   npm run dev
   ```

4. **Open Browser**
   - Navigate to http://localhost:5173
   - Register an account
   - Start detecting emotions!

## 📱 PWA Features

### Installation

**Desktop (Chrome/Edge):**
- Look for install icon in address bar
- Click and select "Install"

**Android:**
- Menu → "Install app"
- Or use the install banner

**iOS:**
- Share → "Add to Home Screen"

### Offline Usage

1. **Download Playlists**
   - Click download button on any playlist
   - Access offline anytime

2. **Offline Emotion Detection**
   - Camera works without internet
   - Results save locally and sync later

3. **Auto-Sync**
   - Changes queue when offline
   - Sync automatically when back online

## 🎯 Usage Guide

### Detect Emotion

**Camera Mode:**
1. Navigate to Camera page
2. Allow camera access
3. Face the camera
4. Emotion detected in real-time
5. Get music recommendations

**Text Mode:**
1. Navigate to Text Input
2. Describe your feelings
3. AI analyzes your text
4. Get matching recommendations

### Download for Offline

1. Browse to any playlist
2. Click "Download" button
3. Wait for progress to complete
4. Playlist now available offline!

### Share Playlists

1. Open any playlist
2. Click "Share" button
3. Configure privacy settings
4. Copy share link
5. Send to friends!

### Follow & Discover

1. Visit Discover page
2. Browse trending playlists
3. Click user profiles
4. Click "Follow" button
5. See their activity in your feed

## 🔧 Configuration

### Backend Environment Variables
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/emotion-music
JWT_SECRET=your-secret-key
NODE_ENV=development
```

### PWA Configuration

**Manifest** (`frontend/public/manifest.json`):
- Theme color: `#9333ea` (purple)
- App name: "Emotion-Aware Music Recommendation"
- Display: standalone

**Service Worker** (`frontend/public/service-worker.js`):
- Cache name: `emotion-music-v1`
- Static assets cached on install
- API calls use network-first strategy

## 📊 Database Schema

### Collections
- **users** - User accounts and profiles
- **emotions** - Emotion detection history
- **playlists** - Generated playlists
- **follows** - User follow relationships
- **sharedplaylists** - Shared playlist metadata
- **comments** - Playlist comments
- **ratings** - Playlist ratings
- **collaborativeplaylists** - Collaborative playlist data
- **activities** - User activity feed
- **notifications** - User notifications

## 🔒 Security

- JWT-based authentication
- Password hashing with bcrypt
- CORS configured
- Input validation
- HTTPS required for PWA (production)
- Secure service worker scope

## 🎨 Customization

### Change Theme Color
Edit `manifest.json` and `index.html`:
```json
"theme_color": "#6366f1"
```

### Modify Cache Strategy
Edit `service-worker.js`:
```javascript
const CACHE_NAME = 'emotion-music-v2';
```

### Adjust Storage Limits
Edit `offlineDB.ts`:
```typescript
setCacheMeta(url, data, ttl);
```

## 📈 Performance

- **First Load**: ~1-2s (cached: <500ms)
- **Emotion Detection**: Real-time (<100ms offline)
- **Offline Storage**: Up to 50% of available disk
- **Background Sync**: 60s interval (configurable)
- **Cache TTL**: 1 hour (configurable)

## 🐛 Troubleshooting

### Service Worker Not Working
1. Ensure using HTTPS (or localhost)
2. Clear browser cache
3. Check DevTools → Application → Service Workers

### Offline Detection Failing
1. Verify TensorFlow.js loaded
2. Check model files exist
3. Grant camera permissions

### Install Prompt Not Showing
1. Wait 30 seconds
2. Ensure icons exist (8 sizes)
3. Check manifest.json is valid
4. Verify HTTPS (or localhost)

## 📚 Documentation

- **[PWA_DOCUMENTATION.md](./PWA_DOCUMENTATION.md)** - Complete PWA guide
- **[OFFLINE_SETUP.md](./OFFLINE_SETUP.md)** - Setup instructions
- **[OFFLINE_QUICK_REFERENCE.md](./OFFLINE_QUICK_REFERENCE.md)** - User guide
- **[SOCIAL_FEATURES.md](./SOCIAL_FEATURES.md)** - Social features documentation
- **[OFFLINE_IMPLEMENTATION_SUMMARY.md](./OFFLINE_IMPLEMENTATION_SUMMARY.md)** - Implementation details

## 🛠️ Tech Stack

### Frontend
- React 18.2.0
- TypeScript 5.2.2
- Redux Toolkit 2.0.0
- React Router 6.20.0
- Tailwind CSS 3.3.6
- Recharts 2.10.0
- Framer Motion 10.16.0
- Socket.io Client 4.5.4
- TensorFlow.js 4.x
- Axios 1.6.0

### Backend
- Node.js 20+
- Express 4.18.2
- TypeScript 5.2.2
- MongoDB 6+
- Mongoose 8.0.0
- Socket.IO 4.5.4
- JWT (jsonwebtoken) 9.0.2
- Bcrypt 5.1.1

### DevOps
- Vite 5.0.0
- ESLint 8.55.0
- Prettier 3.1.0

## 🎯 Roadmap

### Completed ✅
- Emotion detection (camera + text)
- Music recommendations
- Dashboard analytics
- Social features (sharing, following, comments)
- PWA implementation
- Offline support
- Real-time tracking

### Future Enhancements 🚀
- Spotify integration
- Advanced emotion models
- Machine learning personalization
- Multi-language support
- Voice-based emotion detection
- Mood-based playlists
- Social challenges/badges
- Export listening history

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License.

## 👥 Authors

Built with ❤️ by the Emotion Music team

## 🙏 Acknowledgments

- TensorFlow.js team for offline AI
- Spotify API for music data
- React community
- MongoDB team
- All contributors

## 📞 Support

- **Documentation**: See docs folder
- **Issues**: GitHub Issues
- **Discussions**: GitHub Discussions

## 🌟 Show Your Support

Give a ⭐️ if this project helped you!

---

**Version**: 2.0.0 (PWA Edition)  
**Status**: Production Ready  
**Last Updated**: December 2024

---

## 🎉 What's New in v2.0 (PWA Edition)

### Progressive Web App
- ✨ Install to home screen on any device
- ✨ Works completely offline
- ✨ Smart caching for instant loading
- ✨ Background sync for seamless experience
- ✨ Native app-like interface

### Offline Features
- ✨ Download playlists for offline listening
- ✨ Offline emotion detection with TensorFlow.js
- ✨ Queue system for offline changes
- ✨ Storage management UI
- ✨ Auto-sync when connection restored

### UI Enhancements
- ✨ Connection status indicator
- ✨ Download progress tracking
- ✨ Install prompt banner
- ✨ Update notifications
- ✨ Offline features list

### Performance
- ✨ 90+ Lighthouse PWA score
- ✨ Sub-second load times (cached)
- ✨ Optimized storage usage
- ✨ Efficient background sync

---

**Built with modern web technologies to deliver a native app experience in the browser!** 🚀
