# 🚀 Quick Start Guide - Emotion-Aware Music Recommendation Engine

## ✅ Prerequisites Check

- [x] Node.js installed
- [x] Frontend dependencies installed
- [x] Backend dependencies installed
- [x] Environment files created
- [ ] MongoDB running (required for backend)
- [ ] ML Service running (optional - for emotion detection)

---

## 🏃 Running the Project

### Option 1: Frontend Only (Recommended for UI Testing)

If you just want to test the authentication UI without backend:

```powershell
# Terminal 1 - Frontend
cd "d:\Emotion-Aware Music Recommendation Engine\frontend"
npm run dev
```

Then open: **http://localhost:5173**

**Note:** Login/Register won't work without backend, but you can see the UI, forms, validation, and password strength meter.

---

### Option 2: Full Stack (Frontend + Backend + Database)

#### Step 1: Start MongoDB

**Option A - Install MongoDB locally:**
```powershell
# Download from: https://www.mongodb.com/try/download/community
# Or use MongoDB Atlas (cloud): https://www.mongodb.com/cloud/atlas
```

**Option B - Use Docker:**
```powershell
docker run -d -p 27017:27017 --name mongodb mongo:latest
```

**Option C - Update backend/.env to use MongoDB Atlas:**
```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/emotion-music-db
```

#### Step 2: Start Backend Server

```powershell
# Terminal 1 - Backend
cd "d:\Emotion-Aware Music Recommendation Engine\backend"
npm run dev
```

Backend will run on: **http://localhost:5000**

#### Step 3: Start Frontend

```powershell
# Terminal 2 - Frontend  
cd "d:\Emotion-Aware Music Recommendation Engine\frontend"
npm run dev
```

Frontend will run on: **http://localhost:5173**

---

### Option 3: With ML Service (Full Features)

For emotion detection from camera and text:

#### Terminal 1 - ML Service
```powershell
cd "d:\Emotion-Aware Music Recommendation Engine\ml-service"
python -m venv venv
.\venv\Scripts\Activate
pip install -r requirements.txt
python app.py
```

#### Terminal 2 - Backend
```powershell
cd "d:\Emotion-Aware Music Recommendation Engine\backend"
npm run dev
```

#### Terminal 3 - Frontend
```powershell
cd "d:\Emotion-Aware Music Recommendation Engine\frontend"
npm run dev
```

---

## 🎯 What You Can Test Right Now

### ✅ Available Without Backend

1. **UI/UX Testing**
   - Beautiful gradient backgrounds
   - Smooth animations
   - Responsive design
   
2. **Form Validation**
   - Email regex validation
   - Password strength meter
   - Real-time error messages
   - Form submission handling

3. **Navigation**
   - Route switching
   - Protected route logic (will redirect to login)

### ✅ Available With Backend + MongoDB

1. **User Registration**
   - Create new account
   - Password strength enforcement
   - Email validation
   
2. **User Login**
   - Authenticate with credentials
   - Remember me functionality
   - Auto-redirect after login
   - Token storage with expiry

3. **Protected Routes**
   - Dashboard access
   - Camera page
   - Text input page
   - Playlist page

4. **Token Management**
   - Auto token refresh
   - Session expiry handling
   - Logout functionality

### ✅ Available With Full Stack (Backend + ML Service)

1. **Facial Emotion Detection**
   - Camera access
   - Real-time emotion analysis
   - Music recommendations based on emotion

2. **Text Sentiment Analysis**
   - Analyze text input
   - Emotion detection from text
   - Mood-based music suggestions

3. **Playlist Management**
   - Create playlists
   - Save to Spotify
   - View emotion history

---

## 📝 Quick Test Scenarios

### Test 1: Authentication UI (No Backend Needed)

```powershell
cd "d:\Emotion-Aware Music Recommendation Engine\frontend"
npm run dev
```

1. Open http://localhost:5173
2. Click "Sign up for free"
3. Try entering a weak password → See strength meter in red
4. Enter a strong password (e.g., "Test123!@#") → See green strength meter
5. Check all validation messages appear correctly

### Test 2: Full Authentication Flow (Requires Backend + MongoDB)

1. Start MongoDB (Docker or local)
2. Start backend: `npm run dev` in backend folder
3. Start frontend: `npm run dev` in frontend folder
4. Register a new account
5. Login with credentials
6. See dashboard
7. Logout and verify redirect to login

---

## 🐛 Troubleshooting

### Port Already in Use

```powershell
# Frontend (5173)
netstat -ano | findstr :5173
taskkill /PID <PID> /F

# Backend (5000)
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

### MongoDB Connection Failed

Check backend/.env:
```env
MONGODB_URI=mongodb://localhost:27017/emotion-music-db
```

Or use MongoDB Atlas cloud database.

### TypeScript Errors

```powershell
# Frontend
cd frontend
npm run build

# Backend  
cd backend
npm run build
```

### Missing Dependencies

```powershell
# Frontend
cd frontend
npm install

# Backend
cd backend
npm install
```

---

## 🎨 Default Credentials (After Registration)

You'll need to register your own account. No default users exist.

**Test Account Example:**
- Name: Test User
- Email: test@example.com
- Password: Test123!@# (meets all requirements)

---

## 📊 Environment Configuration

### Frontend (.env)
```env
VITE_API_URL=http://localhost:5000
VITE_ML_SERVICE_URL=http://localhost:8000
VITE_ENABLE_FACIAL_RECOGNITION=true
VITE_ENABLE_SENTIMENT_ANALYSIS=true
```

### Backend (.env)
```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/emotion-music-db
ML_SERVICE_URL=http://localhost:8000

# Optional: Add Spotify credentials for music features
SPOTIFY_CLIENT_ID=your_client_id
SPOTIFY_CLIENT_SECRET=your_client_secret
```

---

## 🔗 Application URLs

| Service | URL | Status |
|---------|-----|--------|
| Frontend | http://localhost:5173 | ✅ Ready |
| Backend API | http://localhost:5000 | ⚠️ Needs MongoDB |
| ML Service | http://localhost:8000 | ⚠️ Optional |
| MongoDB | mongodb://localhost:27017 | ⚠️ Needs Installation |

---

## 🎯 Recommended Starting Point

**For immediate testing:**

```powershell
# Just start the frontend to see the beautiful UI
cd "d:\Emotion-Aware Music Recommendation Engine\frontend"
npm run dev
```

**Then visit:**
- http://localhost:5173 - Home page
- http://localhost:5173/login - Login page with validation
- http://localhost:5173/register - Registration with password strength meter

**For full functionality:**
1. Install MongoDB or set up MongoDB Atlas
2. Update backend/.env with MongoDB URI
3. Start backend server
4. Start frontend
5. Register and test complete auth flow

---

## 🚀 Production Build

```powershell
# Frontend
cd frontend
npm run build
# Output in: dist/

# Backend
cd backend
npm run build
# Output in: dist/
```

---

**Status: Frontend is ready to run! Backend needs MongoDB to be fully functional.**

**Recommendation:** Start with frontend-only to test the beautiful authentication UI, then add backend when MongoDB is ready.
