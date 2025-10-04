# Meteor Madness - Vercel Deployment Guide

## Overview
This project has been converted to a frontend-only application that can be deployed to Vercel as a static site. All server-side functionality has been moved to client-side calculations and direct API calls to external services.

## Changes Made

### 1. Color Scheme Update
- Updated the entire app to use the new color palette:
  - Primary Dark: `#3C3D37` (Dark olive)
  - Primary Medium: `#697565` (Medium olive)
  - Primary Light: `#ECDFCC` (Light cream)

### 2. Server Removal
- Removed Node.js and Python server dependencies
- Converted all API calls to use external services directly:
  - NASA NEO API: `https://api.nasa.gov/neo/rest/v1`
  - USGS Earthquake API: `https://earthquake.usgs.gov/fdsnws/event/1`
  - USGS Elevation API: `https://nationalmap.gov/epqs/pqs.php`
  - JPL APIs: `https://ssd-api.jpl.nasa.gov`

### 3. Client-Side Calculations
- Impact effects are now calculated client-side using scientific formulas
- Mitigation strategies are calculated using orbital mechanics principles
- Planetary positions are calculated using simplified NASA formulas

### 4. Vercel Configuration
- Updated `vercel.json` for static deployment
- Removed server function builds
- Configured proper routing for static files

## Deployment Instructions

### Option 1: Vercel CLI
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Follow the prompts to configure your project
```

### Option 2: Vercel Dashboard
1. Go to [vercel.com](https://vercel.com)
2. Import your GitHub repository
3. Vercel will automatically detect the static configuration
4. Deploy with default settings

### Option 3: GitHub Integration
1. Connect your GitHub repository to Vercel
2. Enable automatic deployments on push
3. Every push to main branch will trigger a deployment

## Environment Variables
No environment variables are required for basic functionality. The app uses NASA's DEMO_KEY by default.

To use your own NASA API key:
1. Get a free API key from [api.nasa.gov](https://api.nasa.gov)
2. In `public/app.js`, replace `DEMO_KEY` with your actual key:
   ```javascript
   const NASA_API_KEY = 'YOUR_API_KEY_HERE';
   ```

## Features
- ✅ Real-time NASA NEO data
- ✅ 3D asteroid visualization
- ✅ Impact effect calculations
- ✅ Mitigation strategy analysis
- ✅ USGS earthquake comparisons
- ✅ Planetary position calculations
- ✅ Comet data from NASA
- ✅ Simulated NEOSSAT data
- ✅ Responsive design
- ✅ Mobile-friendly interface

## File Structure
```
├── public/
│   ├── index.html          # Main application
│   ├── app.js             # Core functionality
│   ├── defend-earth-game.js
│   ├── regional-impact-maps.js
│   └── other JS modules
├── vercel.json            # Vercel configuration
├── package.json           # Dependencies (minimal)
└── DEPLOYMENT.md          # This file
```

## Testing Locally
```bash
# Option 1: Python HTTP server
cd public
python -m http.server 8000
# Open http://localhost:8000

# Option 2: Node.js serve
npx serve public
# Open the provided URL
```

## Troubleshooting

### CORS Issues
If you encounter CORS issues with external APIs:

**The Problem:**
- NASA APIs may block direct browser requests due to CORS policies
- This is a browser security feature, not an app issue

**Solutions:**
1. **Demo Mode (Automatic)**: The app automatically falls back to demo data when APIs fail
2. **CORS Proxy**: The app tries to use a CORS proxy as a fallback
3. **Browser Extension**: Install a CORS browser extension for development
4. **Local Server**: Use a local development server (recommended)

**For Development:**
```bash
# Use a local server instead of opening files directly
cd public
python -m http.server 8000
# Then open http://localhost:8000
```

**Expected Behavior:**
- If NASA APIs work: You'll see real asteroid data
- If NASA APIs fail: You'll see demo data with a message in console
- The app will still be fully functional with demo data

### API Rate Limits
- NASA API: 1000 requests per hour with DEMO_KEY
- USGS APIs: No rate limits for public use
- JPL APIs: No rate limits for public use

### Performance
- The app loads demo data first for fast initial experience
- Real NASA data loads in the background
- All calculations are performed client-side for responsiveness

## Support
For issues or questions:
1. Check the browser console for errors
2. Verify all external APIs are accessible
3. Ensure your NASA API key is valid (if using custom key)
4. Test with different browsers if experiencing issues