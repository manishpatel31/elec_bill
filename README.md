# ⚡ Bijli Tracker — SBPDCL Electricity Bill Analyser

A smart, AI-powered electricity bill analyser designed for **SBPDCL (South Bihar Power Distribution Company)** consumers. Upload your bill, and Claude AI extracts all data automatically — no manual typing needed.

---

## 🚀 Features

| Feature | Description |
|---|---|
| 🤖 AI Bill Parsing | Upload PDF/image of bill → Claude extracts all fields automatically |
| 📊 Analytics Dashboard | Monthly consumption, amount, power factor, solar trends |
| ☀️ Solar Tracker | Net metering balance, savings estimation, trend charts |
| 💾 Firebase Sync | Store bills in Firestore, sync across devices |
| 🌙 Dark Mode | Full dark/light theme support |
| 📱 Mobile-Friendly | Bottom tab bar, responsive layout, PWA-ready |
| 📥 Export | Download as CSV or JSON backup |
| 🔒 Local Fallback | Works offline with localStorage if Firebase isn't set up |

---

## 🌐 Hosting on GitHub Pages

### Step 1 — Create Repository
```bash
git init
git add index.html README.md
git commit -m "Initial: Bijli Tracker"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/bijli-tracker.git
git push -u origin main
```

### Step 2 — Enable GitHub Pages
1. Go to your repo on GitHub
2. **Settings → Pages**
3. Under **Source**, select `Deploy from a branch`
4. Branch: `main`, Folder: `/ (root)`
5. Click **Save**
6. Your site will be live at: `https://YOUR_USERNAME.github.io/bijli-tracker/`

---

## 🔥 Firebase Setup (for Cloud Sync)

### Step 1 — Create Firebase Project
1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → Name it `bijli-tracker`
3. Disable Google Analytics (optional) → Create project

### Step 2 — Add Web App
1. Click the **`</>`** (Web) icon on project homepage
2. Name it `bijli-tracker-web`
3. Click **Register app**
4. Copy the `firebaseConfig` object

### Step 3 — Enable Firestore
1. Left sidebar → **Firestore Database**
2. Click **Create database**
3. Choose **Start in test mode**
4. Select your nearest region → **Done**

### Step 4 — Set Firestore Rules (Production)
In Firestore → **Rules** tab, replace with:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /billdata/{document} {
      allow read, write: if true; // Change to auth-based rules in production
    }
    match /_test/{document} {
      allow read, write: if true;
    }
  }
}
```

### Step 5 — Add Config to App
1. Open the hosted website
2. Go to **Settings** tab → **Firebase Configuration**
3. Paste your Firebase config JSON:
```json
{
  "apiKey": "AIza...",
  "authDomain": "bijli-tracker.firebaseapp.com",
  "projectId": "bijli-tracker",
  "storageBucket": "bijli-tracker.appspot.com",
  "messagingSenderId": "123456789",
  "appId": "1:123456789:web:abc123"
}
```
4. Click **Save & Reload**
5. Click **Test Connection** to verify

---

## 📋 How to Use

### Upload a Bill
1. Go to **Upload Bill** tab
2. Drag & drop or tap to select your SBPDCL bill (PDF or image)
3. AI analyses it and extracts all fields
4. Review the extracted data
5. Click **Save Bill**

### Manual Entry
If AI parsing fails or you want to enter old bills:
1. Click **Enter Manually** on the Upload tab
2. Fill in the form fields
3. Click **Save**

### View Analytics
- **Analytics** tab: consumption trends, amount trends, charge breakdown, solar vs grid, power factor
- **Solar** tab: solar balance trend, savings estimate, insights
- **History** tab: all bills in a table, filterable; export as CSV

---

## 🗂 File Structure

```
bijli-tracker/
├── index.html          ← Single file — the entire app
└── README.md           ← This file
```

Everything is in one `index.html` file — no build step, no dependencies to install, no server needed.

---

## 🔑 Data Extracted from Bill

| Field | Description |
|---|---|
| Bill Month | e.g. MAY-2026 |
| Account Number | CA number |
| Consumer Name & Address | Full details |
| Total Units (kWh) | All phases combined |
| Energy Charge | ₹ per unit charges |
| Fixed/Demand Charge | Monthly fixed charges |
| State Subsidy | Free + subsidised unit subsidy |
| Net Bill Amount | Final amount due |
| Solar Balance | Net metering units banked |
| Power Factor | Electrical efficiency ratio |
| Previous Reading | Meter reading previous month |
| Current Reading | Latest meter reading |
| Previous Payment | Last payment amount & date |

---

## 💡 Tips

- Upload bills as **clear photos** or PDFs for best AI accuracy
- If AI misreads a field, use **Edit** button to correct before saving
- Enable **Firebase** to sync bills across multiple devices (phone + desktop)
- Export monthly via **CSV** to keep a spreadsheet backup
- Power Factor < 0.95 → check your capacitors/appliances

---

## 🛠 Tech Stack

- **Vanilla HTML/CSS/JS** — no frameworks, no build tools
- **Claude AI (claude-sonnet-4)** — bill parsing via Anthropic API
- **Firebase Firestore** — optional cloud storage
- **Chart.js** — all charts and graphs
- **Font Awesome** — icons
- **Google Fonts** — Plus Jakarta Sans, JetBrains Mono, Syne

---

Made with ❤️ for SBPDCL consumers in Bihar
