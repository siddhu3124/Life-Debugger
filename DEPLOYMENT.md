# Life Debugger - Deployment Guide

## 🔒 Security Status: ✅ SECURE

Your Gemini API key is properly protected:
- ✅ Stored in `backend/.env` file
- ✅ Backend has `.gitignore` to prevent pushing to GitHub
- ✅ Uses `process.env.GEMINI_API_KEY` (server-side only)

---

## Prerequisites

### 1. Environment Variables Setup

#### Backend Environment Variables
Create a `.env` file in the `backend/` directory:

```env
# MongoDB Connection (get from MongoDB Atlas)
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/life-debugger

# JWT Secret (generate a strong random string)
JWT_SECRET=your-super-secret-jwt-key-change-this

# Gemini AI API Key (get from https://aistudio.google.com/app/apikey)
GEMINI_API_KEY=your-actual-gemini-api-key

# Client Origin (your deployed frontend URL)
CLIENT_ORIGIN=https://your-frontend.vercel.app

# Server Port
PORT=5000
```

#### Frontend Environment Variables
Create a `.env` file in the `frontend/` directory:

```env
# API URL (use your deployed backend URL)
VITE_API_URL=https://your-backend-url.onrender.com/api
```

> **Note:** The frontend `.env` is already in `.gitignore` so it won't be pushed to GitHub.

---

## Deployment Options

### Option 1: Vercel + Render/Heroku (Recommended)

#### Frontend (Vercel)
1. Push your code to GitHub
2. Go to [Vercel.com](https://vercel.com)
3. Import your repository
4. Configure:
   - Framework: Vite
   - Build Command: `npm run build`
   - Output Directory: `dist`
5. Add Environment Variable in Vercel dashboard:
   - `VITE_API_URL` = `https://your-backend-url.onrender.com/api`
6. Deploy

#### Backend (Render/Railway/Heroku)
1. Create account on [Render.com](https://render.com)
2. Connect your GitHub repository
3. Create a new Web Service
4. **IMPORTANT** - Set Root Directory to: `backend`
5. Configure:
   - Build Command: `npm install`
   - Start Command: `npm start`
6. Add Environment Variables in Render dashboard:
   - `MONGODB_URI`
   - `JWT_SECRET`
   - `GEMINI_API_KEY`
   - `CLIENT_ORIGIN`
7. Deploy

---

### Option 2: Railway

1. Go to [Railway.app](https://railway.app)
2. Connect GitHub repo
3. Create new project
4. Add MySQL database (or MongoDB)
5. Add environment variables
6. Deploy both frontend and backend

---

## Local Development

### Install Dependencies
```bash
# Backend
cd backend
npm install

# Frontend
cd frontend
npm install
```

### Run Development Servers
```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm run dev
```

### Build for Production
```bash
# Frontend
cd frontend
npm run build
```

---

## Verification Checklist

Before pushing to GitHub:

- [ ] Backend `.env` file exists with API keys
- [ ] Backend `.gitignore` excludes `.env`
- [ ] Frontend `.gitignore` excludes `.env`
- [ ] No API keys are hardcoded in source files
- [ ] All dependencies are in `package.json`
- [ ] Frontend builds successfully (`npm run build`)
- [ ] Frontend `VITE_API_URL` is set correctly in deployment

---

## Troubleshooting

### "GEMINI_API_KEY missing" error
- Ensure `.env` file exists in `backend/` directory
- Restart the server after adding `.env`

### CORS errors in production
- Update `CLIENT_ORIGIN` in `.env` to match your deployed frontend URL

### MongoDB connection errors
- Verify `MONGODB_URI` is correct
- Ensure MongoDB Atlas IP whitelist includes your deployment IP

---

## Important Notes

1. **Never commit `.env` files** - They are already in `.gitignore`
2. **Rotate your API keys** periodically
3. **Use environment variables** for all sensitive data
4. **HTTPS is required** for production deployment

