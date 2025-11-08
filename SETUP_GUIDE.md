# Rent-a-Ride Setup Guide

This guide will help you set up and run the Rent-a-Ride project locally.

## Prerequisites

- Node.js (v16 or higher)
- MongoDB (local installation or MongoDB Atlas account)
- npm or yarn package manager

## Project Structure

```
Rent-a-Ride/
├── backend/          # Express.js backend server
├── client/           # React frontend application
└── package.json      # Root package.json
```

## Step 1: Backend Setup

### 1.1 Install Dependencies

```bash
cd backend
npm install
```

### 1.2 Configure Environment Variables

Create a `.env` file in the `backend` directory with the following variables:

```env
# MongoDB Connection
MONGO_URI=mongodb://localhost:27017/rent-a-ride
# Or use MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/rent-a-ride

# Server Port
PORT=4000

# JWT Tokens (generate secure random strings)
ACCESS_TOKEN=your_access_token_secret_key_here_min_32_chars
REFRESH_TOKEN=your_refresh_token_secret_key_here_min_32_chars

# Cloudinary Configuration (get from https://cloudinary.com)
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret

# Razorpay Configuration (get from https://razorpay.com)
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_SECRET=your_razorpay_secret

# Email Configuration (for Nodemailer - use App Password for Gmail)
EMAIL_HOST=your_email@gmail.com
EMAIL_PASSWORD=your_email_app_password

# Node Environment
NODE_ENV=development
```

### 1.3 Generate JWT Secrets

You can generate secure JWT secrets using:

**Linux/Mac:**
```bash
openssl rand -base64 32
```

**Windows (PowerShell):**
```powershell
[Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes([System.Guid]::NewGuid().ToString() + [System.Guid]::NewGuid().ToString()))
```

### 1.4 Start Backend Server

From the root directory:
```bash
npm run dev
```

Or from the backend directory:
```bash
cd backend
npm run dev
```

The backend server will start on `http://localhost:4000`

## Step 2: Frontend Setup

### 2.1 Install Dependencies

```bash
cd client
npm install
```

### 2.2 Configure Environment Variables

Create a `.env` file in the `client` directory:

```env
# Backend API URL
# For local development:
VITE_PRODUCTION_BACKEND_URL=http://localhost:4000

# Firebase Configuration (for Google OAuth)
VITE_FIREBASE_API_KEY=your_firebase_api_key_here
```

**Note:** The Vite proxy is configured to forward `/api` requests to the backend in development mode, so relative paths should work, but it's better to use the BASE_URL for consistency.

### 2.3 Start Frontend Development Server

```bash
cd client
npm run dev
```

The frontend will start on `http://localhost:5173`

## Step 3: Database Setup

### Option A: Local MongoDB

1. Install MongoDB locally
2. Start MongoDB service
3. Update `MONGO_URI` in backend `.env` to: `mongodb://localhost:27017/rent-a-ride`

### Option B: MongoDB Atlas (Cloud)

1. Create a free account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster
3. Get your connection string
4. Update `MONGO_URI` in backend `.env` with your Atlas connection string

### 3.1 Seed Database (Optional)

If you have a seed script:
```bash
cd backend
node seed.js
```

## Step 4: Verify Installation

### 4.1 Test Backend

Open your browser and navigate to:
```
http://localhost:4000/api/test
```

You should see:
```json
{
  "success": true,
  "message": "Backend is running with .env!"
}
```

### 4.2 Test Frontend

Open your browser and navigate to:
```
http://localhost:5173
```

You should see the Rent-a-Ride homepage.

## Common Issues and Solutions

### Issue: MongoDB Connection Error

**Solution:**
- Ensure MongoDB is running (if using local MongoDB)
- Check your `MONGO_URI` in the `.env` file
- Verify network access if using MongoDB Atlas

### Issue: CORS Error

**Solution:**
- Ensure `VITE_PRODUCTION_BACKEND_URL` in client `.env` matches your backend URL
- Check `allowedOrigins` in `backend/server.js` includes your frontend URL

### Issue: API Calls Failing

**Solution:**
- Verify backend is running on port 4000
- Check that `.env` files are in the correct directories
- Ensure all environment variables are set correctly
- Check browser console for specific error messages

### Issue: Cloudinary Upload Failing

**Solution:**
- Verify your Cloudinary credentials in backend `.env`
- Check that your Cloudinary account is active

### Issue: Email Not Sending

**Solution:**
- For Gmail, use an App Password instead of your regular password
- Ensure `EMAIL_HOST` and `EMAIL_PASSWORD` are correct
- Check your email provider's SMTP settings

## API Endpoints

### User Routes (`/api/user`)
- `GET /api/user/listAllVehicles` - Get all vehicles
- `POST /api/user/showVehicleDetails` - Get vehicle details
- `POST /api/user/bookCar` - Book a vehicle
- `POST /api/user/filterVehicles` - Filter vehicles

### Auth Routes (`/api/auth`)
- `POST /api/auth/signup` - User signup
- `POST /api/auth/signin` - User signin
- `POST /api/auth/google` - Google OAuth
- `POST /api/auth/refreshToken` - Refresh access token

### Admin Routes (`/api/admin`)
- `GET /api/admin/showVehicles` - Get all vehicles (admin)
- `GET /api/admin/getVehicleModels` - Get vehicle models and locations

### Vendor Routes (`/api/vendor`)
- `POST /api/vendor/signup` - Vendor signup
- `POST /api/vendor/signin` - Vendor signin

## Development Workflow

1. Start MongoDB (if using local)
2. Start backend server: `npm run dev` (from root) or `cd backend && npm run dev`
3. Start frontend server: `cd client && npm run dev`
4. Open `http://localhost:5173` in your browser

## Production Deployment

For production deployment:
1. Update `NODE_ENV=production` in backend `.env`
2. Update `VITE_PRODUCTION_BACKEND_URL` in client `.env` to your production backend URL
3. Build the frontend: `cd client && npm run build`
4. Deploy backend and frontend to your hosting service

## Additional Resources

- [MongoDB Documentation](https://docs.mongodb.com/)
- [Express.js Documentation](https://expressjs.com/)
- [React Documentation](https://react.dev/)
- [Vite Documentation](https://vitejs.dev/)

