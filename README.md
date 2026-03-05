# 📷 Photobooth Stock Management

Real-time inventory system for LSQ / TCR / CAM / Office.

---

## 🚀 Setup Guide (15 minutes total)

### Step 1 — Create Firebase Project (free)

1. Go to **https://console.firebase.google.com**
2. Click **"Create a project"** → name it `photobooth-stock` → Continue
3. Disable Google Analytics (not needed) → **Create project**

### Step 2 — Set up Realtime Database

1. In your project sidebar → **Build → Realtime Database**
2. Click **"Create Database"**
3. Choose a region (e.g. `europe-west1` for UK)
4. Start in **test mode** (we'll lock it down later) → Enable

### Step 3 — Get your Firebase config

1. Go to **Project Settings** (gear icon, top left)
2. Scroll down to **"Your apps"** → click **"</> Web"**
3. Register app name `photobooth-web` → **Register app**
4. You'll see a config object like this:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "photobooth-stock.firebaseapp.com",
  databaseURL: "https://photobooth-stock-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "photobooth-stock",
  storageBucket: "photobooth-stock.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

### Step 4 — Paste your config into all 3 files

Open each of these files and replace `YOUR_API_KEY`, `YOUR_PROJECT`, etc. with your actual values:
- `index.html` (search for `YOUR_API_KEY`)
- `sales.html` (search for `YOUR_API_KEY`)
- `inventory.html` (search for `YOUR_API_KEY`)

The `databaseURL` field is especially important — copy it exactly.

### Step 5 — Push to GitHub

```bash
git init
git add .
git commit -m "Initial photobooth stock app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/photobooth-stock.git
git push -u origin main
```

### Step 6 — Enable GitHub Pages

1. Go to your repo on GitHub → **Settings → Pages**
2. Source: **Deploy from a branch** → Branch: `main` → `/ (root)` → Save
3. Your app will be live at: `https://YOUR_USERNAME.github.io/photobooth-stock/`

Share this URL with all 3 stores — it works on any phone or desktop browser.

---

## 📱 How to Use

### Dashboard (`index.html`)
- See real-time stock for all 4 locations at a glance
- Red numbers = out of stock, amber = low stock (≤3)
- Recent sales feed at the bottom
- Alert banner appears when anything is low/out

### Record Sale (`sales.html`)
- Select your store → product → qty + amount → Confirm
- Stock deducts automatically in real time
- Can also link directly: `sales.html?loc=LSQ`

### Manage Stock (`inventory.html`)
- `+` / `−` buttons to adjust by 1
- Click the number to type any value directly
- **Bulk Stock In** — add multiple units at once (e.g. after delivery)
- **Transfer** — move stock between locations

---

## 💳 Stripe Integration (future)

When you're ready to connect Stripe:
- Sales amounts already log to Firebase → easy to pull into Stripe reports
- Add Stripe Checkout links per product in `sales.html`
- Or use **Stripe Payment Links** and webhook to auto-log sales

---

## 🔒 Securing the Database (when ready)

In Firebase Console → Realtime Database → **Rules**, replace with:

```json
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

Then add Firebase Authentication (email/password) so only your team can access it.

---

## 📁 File Structure

```
/
├── index.html        ← Dashboard (stock overview)
├── sales.html        ← Record a sale
├── inventory.html    ← Adjust / manage stock
└── README.md         ← This file
```
