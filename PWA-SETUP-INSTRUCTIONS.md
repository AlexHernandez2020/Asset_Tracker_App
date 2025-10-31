# TSU Asset Inventory Tracker - PWA Setup Instructions

## What You Have Now

Your asset inventory tracker has been converted into a **Progressive Web App (PWA)**! This means users can install it on their phones like a native app.

## Files Created

1. **asset-inventory.html** - Main app (updated with PWA support)
2. **manifest.json** - App configuration and metadata
3. **service-worker.js** - Enables offline functionality
4. **PWA-SETUP-INSTRUCTIONS.md** - This file

## What's Missing: App Icons

You need to create two icon files:
- `icon-192.png` (192x192 pixels)
- `icon-512.png` (512x512 pixels)

### Option 1: Create Icons Online (Easiest)

1. Go to **https://realfavicongenerator.net/** or **https://www.pwabuilder.com/imageGenerator**
2. Upload a square logo/image (TSU logo or custom design)
3. Download the generated icons
4. Rename them to `icon-192.png` and `icon-512.png`
5. Place them in the same folder as your HTML file

### Option 2: Use a Placeholder

For testing, you can create simple colored squares:
- Use any image editor (Paint, Photoshop, Canva)
- Create 192x192 and 512x512 PNG images
- Use TSU colors (maroon/gray)
- Add text "TSU Assets" in the center

## Deployment Steps

### Step 1: Host Your Files

You **MUST** host these files on a web server with **HTTPS** (required for PWAs and camera access).

**Free Hosting Options:**

1. **GitHub Pages** (Recommended - Free)
   ```bash
   # Create a new repository on GitHub
   # Upload all files (HTML, JSON, JS, icons)
   # Enable GitHub Pages in repository settings
   # Your URL will be: https://username.github.io/repo-name/asset-inventory.html
   ```

2. **Netlify** (Free)
   - Drag and drop your folder at netlify.com/drop
   - Get instant HTTPS URL

3. **Vercel** (Free)
   - Sign up at vercel.com
   - Import your files
   - Get instant HTTPS URL

4. **Firebase Hosting** (Free)
   ```bash
   npm install -g firebase-tools
   firebase login
   firebase init hosting
   firebase deploy
   ```

### Step 2: Update File Paths (If Needed)

If your files are NOT in the root directory, update these files:

**In manifest.json:**
```json
"start_url": "/your-path/asset-inventory.html"
```

**In service-worker.js:**
```javascript
const urlsToCache = [
  '/your-path/asset-inventory.html',
  // ... other URLs
];
```

**In asset-inventory.html:**
```html
<link rel="manifest" href="/your-path/manifest.json">
```

### Step 3: Test the PWA

1. Open your hosted URL in Chrome on your phone
2. Check the browser console for any errors
3. Verify camera access works
4. Test the install prompt (see below)

## Installing the PWA on Devices

### Android (Chrome/Edge)

1. Open the website in Chrome/Edge
2. Tap the **three dots menu** (⋮)
3. Select **"Install app"** or **"Add to Home Screen"**
4. Confirm installation
5. App icon appears on home screen
6. Opens full-screen without browser UI

### iPhone/iPad (Safari)

1. Open the website in Safari
2. Tap the **Share button** (□↑)
3. Scroll and tap **"Add to Home Screen"**
4. Edit name if desired
5. Tap **"Add"**
6. App icon appears on home screen

### Desktop (Chrome/Edge)

1. Open the website in Chrome/Edge
2. Look for **install icon** (⊕) in address bar
3. Click to install
4. App opens in its own window

## Features Enabled

✅ **Offline Access** - Works without internet (after first load)
✅ **Camera Scanner** - Barcode scanning on mobile devices
✅ **Local Storage** - Data persists on device
✅ **App-like Experience** - Full-screen, no browser UI
✅ **Home Screen Icon** - Launches like native app
✅ **Auto-Updates** - Changes deploy instantly

## Troubleshooting

### "Add to Home Screen" not showing
- Ensure you're using HTTPS (not HTTP)
- Check browser console for service worker errors
- Make sure manifest.json is loading correctly

### Camera not working
- PWA requires HTTPS or localhost
- User must grant camera permissions
- Check if device/browser supports camera API

### Offline mode not working
- Open browser DevTools → Application → Service Workers
- Check if service worker is registered and active
- Clear cache and reload to test fresh install

### Icons not showing
- Verify icon files are in correct location
- Check file names match manifest.json exactly
- Icons must be PNG format
- Clear browser cache after adding icons

## Testing Locally

To test on localhost before deploying:

```bash
# Option 1: Python
python -m http.server 8000
# Visit: http://localhost:8000/asset-inventory.html

# Option 2: Node.js
npx http-server -p 8000
# Visit: http://localhost:8000/asset-inventory.html

# Option 3: PHP
php -S localhost:8000
# Visit: http://localhost:8000/asset-inventory.html
```

**Note:** Camera access works on `localhost` even without HTTPS.

## Updating the App

When you make changes:
1. Update files on your server
2. Increment cache version in `service-worker.js`:
   ```javascript
   const CACHE_NAME = 'tsu-asset-tracker-v2'; // Change v1 to v2
   ```
3. Users will automatically get updates on next visit

## Security Notes

- All data stored locally on user's device
- No data transmitted to external servers
- Camera access requires user permission
- HTTPS ensures secure connection

## Support

**Browser Requirements:**
- Chrome 67+ (Android/Desktop)
- Safari 11.3+ (iOS)
- Edge 79+ (Android/Desktop)
- Firefox 68+ (Android/Desktop)

**Not Supported:**
- Internet Explorer (any version)
- Very old mobile browsers

## Next Steps

1. ✅ Create icon files (192px and 512px)
2. ✅ Choose a hosting provider
3. ✅ Upload all files to hosting
4. ✅ Test installation on mobile device
5. ✅ Share the URL with your technicians

## Need Native Apps Later?

If you need to publish to Google Play or Apple App Store:

1. Go to **https://www.pwabuilder.com**
2. Enter your PWA URL
3. Click "Package For Stores"
4. Download Android APK and iOS package
5. Submit to app stores

This generates native app packages from your PWA automatically!

---

**Questions or Issues?**

Check the browser console for error messages. Most PWA issues are related to:
- Missing HTTPS
- Incorrect file paths
- Missing icon files
- Service worker not registering
