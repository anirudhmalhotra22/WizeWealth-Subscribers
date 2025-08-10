# 🚨 Deployment Troubleshooting Guide

## Common Issues and Solutions

### 1. Google Apps Script Deployment Issues

**Problem**: Getting errors when deploying Google Apps Script
**Solution**:
1. Make sure you're in the correct Google Sheet
2. Go to **Extensions** → **Apps Script**
3. Replace ALL the default code with the contents of `google-apps-script.js`
4. Save the script (Ctrl+S)
5. Click **Deploy** → **New deployment**
6. Choose **Web app** as the type
7. Set **Execute as**: Me
8. Set **Who has access**: Anyone
9. Click **Deploy**
10. **IMPORTANT**: Copy the **Web app URL** (not the edit URL)

**The correct URL format should be**:
```
https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
```

### 2. Backend Deployment Issues on Render

**Problem**: Backend not deploying on Render
**Solution**:
1. Make sure your GitHub repository contains:
   - `server.js`
   - `package.json`
   - `README.md`

2. In Render dashboard:
   - **Name**: wizewealth-newsletter-backend
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Environment**: Node

3. **IMPORTANT**: Add environment variable:
   - Key: `PORT`
   - Value: `3000`

### 3. URL Configuration Issues

**Problem**: Frontend can't connect to backend
**Solution**:

1. **Update server.js** with your Google Apps Script web app URL:
```javascript
const GOOGLE_SHEETS_WEBHOOK_URL = 'https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec';
```

2. **Update invest.html** with your Render backend URL:
```javascript
const backendUrl = 'https://your-app-name.onrender.com/subscribe';
```

### 4. CORS Issues

**Problem**: Getting CORS errors
**Solution**:
The backend already has CORS configured, but if you still get errors:
1. Make sure the backend URL in `invest.html` is correct
2. Check that the backend is actually running on Render

### 5. Google Sheets Integration Issues

**Problem**: Data not appearing in Google Sheets
**Solution**:
1. Make sure the Google Apps Script is deployed as a **Web app**
2. Check that the webhook URL in `server.js` is correct
3. Test the webhook URL directly in browser to see if it responds

### 6. Testing Steps

1. **Test Google Apps Script**:
   - Open your deployed web app URL in browser
   - Should show: `{"status":"healthy","message":"WizeWealth Newsletter Webhook is running"}`

2. **Test Backend**:
   - Visit: `https://your-app-name.onrender.com/`
   - Should show: `{"message":"WizeWealth Newsletter Backend is running!"}`

3. **Test Complete Flow**:
   - Fill out the newsletter form
   - Check Google Sheets for new entry
   - Check browser console for any errors

### 7. Debugging Commands

**Check if backend is running**:
```bash
curl https://your-app-name.onrender.com/
```

**Test Google Apps Script**:
```bash
curl https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
```

### 8. Common Error Messages

- **"Failed to fetch"**: Backend URL is incorrect or backend is down
- **"CORS error"**: Backend URL is wrong or CORS not configured
- **"Google Sheets webhook error"**: Google Apps Script URL is incorrect
- **"Build failed"**: Missing dependencies in package.json

### 9. Final Checklist

- [ ] Google Apps Script deployed as Web app
- [ ] Copied the correct web app URL (not edit URL)
- [ ] Updated `server.js` with Google Apps Script URL
- [ ] Backend deployed on Render successfully
- [ ] Updated `invest.html` with Render backend URL
- [ ] Frontend deployed and accessible
- [ ] Tested complete flow end-to-end

### 10. Getting Help

If you're still having issues:
1. Check the browser console for errors
2. Check Render logs for backend errors
3. Test each component individually
4. Make sure all URLs are correct and accessible

