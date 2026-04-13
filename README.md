# N64 Vault — Setup Guide

## Files
- `index.html` — Game library / home page
- `play.html` — Emulator page (EmulatorJS + cloud saves)

---

## Step 1: Set up Firebase (free)

1. Go to https://console.firebase.google.com
2. Click **Add project** → name it (e.g. "n64vault") → Create
3. In the project dashboard, click the **web icon (</>)** to add a web app
4. Copy the `firebaseConfig` object it gives you

5. **Enable Authentication:**
   - Left sidebar → Build → Authentication → Get started
   - Enable **Email/Password** provider

6. **Enable Firestore:**
   - Left sidebar → Build → Firestore Database → Create database
   - Choose **Start in test mode** (fine for personal use)
   - Pick a region → Done

---

## Step 2: Add your Firebase config

Open **both** `index.html` and `play.html` and replace this block near the bottom:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

Paste your real config values from Step 1.

---

## Step 3: Deploy to Netlify

1. Push both HTML files to your GitHub repo
2. In Netlify:
   - **Base directory:** (leave blank)
   - **Build command:** (leave blank — no build needed, it's pure HTML)
   - **Publish directory:** `/` or `.` (or wherever the files are)
3. Done — Netlify will serve the static HTML files directly

---

## How it works

- User clicks a game → file picker opens → they select their `.n64`/`.z64` ROM from their device
- ROM is read into memory (never uploaded to any server)
- EmulatorJS boots the N64 core in the browser at 60fps
- If signed in, saves sync to Firestore automatically every 2 minutes
- Manual save/load buttons also available

## ROM formats supported
`.n64`, `.z64`, `.v64`, `.rom`
