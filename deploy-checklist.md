# 📋 Deployment Checklist

## Step 1: Google Apps Script Setup ✅

1. **Create Google Sheet**
   - Go to [sheets.new](https://sheets.new)
   - Name it "WizeWealth Subscribers"

2. **Deploy Google Apps Script**
   - Open your Google Sheet
   - Go to **Extensions** → **Apps Script**
   - Replace default code with `google-apps-script.js` content
   - Save (Ctrl+S)
   - Click **Deploy** → **New deployment**
   - Type: **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Click **Deploy**
   - **Copy the Web app URL** (starts with `https://script.google.com/macros/s/`)

## Step 2: Backend Deployment ✅

1. **Push to GitHub**
   - Create new repository on GitHub
   - Push these files: `server.js`, `package.json`, `README.md`

2. **Deploy on Render**
   - Go to [render.com](https://render.com)
   - Click **New** → **Web Service**
   - Connect your GitHub repository
   - Configure:
     - Name: `wizewealth-newsletter-backend`
     - Build Command: `npm install`
     - Start Command: `npm start`
   - Click **Create Web Service**
   - Wait for deployment
   - **Copy the Service URL** (e.g., `https://your-app.onrender.com`)

## Step 3: Update Configuration ✅

1. **Update server.js**
   ```javascript
   const GOOGLE_SHEETS_WEBHOOK_URL = 'YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL';
   ```

2. **Update invest.html**
   ```javascript
   const backendUrl = 'YOUR_RENDER_BACKEND_URL/subscribe';
   ```

## Step 4: Test Everything ✅

1. **Test Google Apps Script**
   - Visit your Google Apps Script web app URL
   - Should show: `{"status":"healthy"}`

2. **Test Backend**
   - Visit your Render backend URL
   - Should show: `{"message":"WizeWealth Newsletter Backend is running!"}`

3. **Test Complete Flow**
   - Open your frontend
   - Fill newsletter form
   - Submit
   - Check Google Sheet for new entry

## Common Issues to Check:

- [ ] Google Apps Script URL is the **web app URL**, not edit URL
- [ ] Backend URL in `invest.html` includes `/subscribe`
- [ ] All URLs are accessible (no 404 errors)
- [ ] No CORS errors in browser console
- [ ] Google Sheet has proper permissions

## Quick Test Commands:

```bash
# Test backend
curl https://your-backend.onrender.com/

# Test Google Apps Script
curl https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
```

## If Still Having Issues:

1. Check browser console for errors
2. Check Render logs for backend errors
3. Verify all URLs are correct
4. Test each component individually
5. Make sure Google Sheet is accessible

