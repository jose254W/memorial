# Memorial Website — Setup Guide

## Project Structure
```
memorial-website/
├── index.html             ← The full website
├── data.json              ← Edit this to personalise all content
├── firebase-config.js     ← Your Firebase credentials go here
├── photos/
│   ├── portrait.jpg       ← Hero portrait photo
│   ├── photo1.jpg         ← Gallery photos
│   └── README.txt
├── documents/
│   ├── funeral-program.pdf
│   ├── eulogy.pdf
│   └── README.txt
└── README.md
```

---

## Step 1 — Open in VS Code
Unzip and open the `memorial-website` folder in VS Code.
Install the **Live Server** extension → right-click `index.html` → Open with Live Server.

---

## Step 2 — Set up Firebase (for shared real-time condolences)

### Create your free Firebase project
1. Go to https://console.firebase.google.com and sign in with Google
2. Click **"Add project"** → name it (e.g. `james-memorial`) → Create
3. In the project dashboard, click the **</>** (Web) icon → register your app
4. Copy the `firebaseConfig` values shown

### Enable Realtime Database
5. In the left sidebar → **Build → Realtime Database → Create database**
6. Choose your region → Start in **test mode** (allows reads/writes for 30 days)
7. Copy the **database URL** shown (looks like `https://james-memorial-default-rtdb.firebaseio.com`)

### Paste your credentials into `index.html`
8. Open `index.html` in VS Code
9. Find the `firebaseConfig` block (around line 200) and replace the dummy values:

```js
const firebaseConfig = {
  apiKey:            "AIzaSy...",          // paste your real key
  authDomain:        "james-memorial.firebaseapp.com",
  databaseURL:       "https://james-memorial-default-rtdb.firebaseio.com",
  projectId:         "james-memorial",
  storageBucket:     "james-memorial.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc123"
};
```

That's it — condolences are now shared across ALL devices in real time.

---

## Step 3 — Personalise content (edit data.json)

```json
{
  "person": {
    "name": "James Doe",
    "born": "March 15, 1988",
    "passed": "May 20, 2025",
    "tagline": "A heart full of love, a spirit that never fades",
    "profilePhoto": "photos/portrait.jpg"
  }
}
```

### Add photos
Copy images into `photos/` and list them in data.json:
```json
"photos": [
  { "url": "photos/beach.jpg",      "caption": "At the beach, 2022" },
  { "url": "photos/graduation.jpg", "caption": "Graduation day"     }
]
```

### Add life story entries
```json
"lifeStory": [
  { "year": "1988", "title": "Born in Nairobi", "text": "He arrived on a sunny morning..." },
  { "year": "2006", "title": "School at Alliance", "text": "He loved football and science..." }
]
```

---

## Step 4 — Add PDF documents
Copy your files into `documents/`:
- `documents/funeral-program.pdf`
- `documents/eulogy.pdf`

Download buttons on the site link to these automatically.

---

## Step 5 — Deploy to Netlify (free)
1. Go to https://netlify.com → sign up free
2. Click **"Add new site" → "Deploy manually"**
3. Drag and drop your `memorial-website` folder onto the dashboard
4. Netlify gives you a public link instantly — share it with family!

> **Tip:** You can also connect your GitHub repo for auto-deploys.

---

## Firebase test mode expiry
After 30 days, Firebase test mode expires. Before then:
1. Firebase console → Realtime Database → Rules
2. Replace the rules with:
```json
{
  "rules": {
    "condolences": {
      ".read": true,
      ".write": true
    }
  }
}
```
This keeps the database open. For extra security later, you can add authentication.


---

## Contribution Channel (data.json → "contributions")
Edit the message and contact info shown in the Support section:
```json
"contributions": {
  "intro": "A short intro paragraph visible above the card.",
  "title": "How to Contribute",
  "message": "A warm message about how to get in touch.",
  "contacts": [
    { "label": "Phone",   "value": "+254 700 000 000" },
    { "label": "Email",   "value": "family@example.com" },
    { "label": "Contact", "value": "Jane Doe (Sister)" }
  ]
}
```
Add as many contact rows as you need.

---

## Family Appreciation Message (data.json → "familyMessage")
```json
"familyMessage": {
  "title": "A Word of Gratitude",
  "message": "Type the full family message here...",
  "signedBy": "The Doe Family",
  "subtitle": "With love & gratitude",
  "photos": []
}
```
To show small family portrait bubbles below the message, add photo paths:
```json
"photos": [
  { "url": "photos/mum.jpg",  "name": "Mum"  },
  { "url": "photos/dad.jpg",  "name": "Dad"  },
  { "url": "photos/jane.jpg", "name": "Jane" }
]
```
# memorial
