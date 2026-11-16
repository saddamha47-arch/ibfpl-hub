# 111 — Setup ও Deployment গাইড (ধাপে ধাপে)

এই গাইড ধরে নিচ্ছে আপনার GitHub account ও Firebase project (`ibfpl-hub`) আগে থেকেই আছে। সবকিছু বিনামূল্যের plan-এ চলে।

## ক. কোন ফাইল কোথায় যাবে

| ফাইল | কোথায় |
|---|---|
| `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`, `.nojekyll` | GitHub repository-র একদম উপরের স্তরে (root) |
| `sec` ফোল্ডার (ভেতরের সব `.bin` ফাইলসহ) | GitHub repository-র root-এ, ফোল্ডার হিসেবেই |
| `flow3d.html`, `flow3d_full.html`, `three.min.js`, `narration_full.mp3`, `narration_summary.mp3`, `ibfpl_3d_summary.mp4` | GitHub repository-র root-এ |
| `README.md`, `SETUP_GUIDE_BN.md`, `firebase.json` | GitHub repository-র root-এ (ওয়েবসাইট এগুলো ব্যবহার করে না) |
| `firestore.rules` | Firebase Console-এ paste করতে হবে (নিচে ধাপ গ) |

**GitHub-এ যা রাখবেন না:** পুরোনো `eq` ফোল্ডার (খোলা ছবি), admin passphrase, কোনো password, service-account JSON ফাইল।

## খ. GitHub-এ আপলোড

`sec` ফোল্ডারে প্রায় ৩৮০টি ফাইল আছে। GitHub-এর ওয়েবসাইট একবারে ১০০টির বেশি ফাইল নেয় না। তাই **GitHub Desktop** (বিনামূল্যের) ব্যবহার করাই সহজ।

1. https://desktop.github.com থেকে GitHub Desktop install করে নিজের account দিয়ে sign in করুন।
2. **File → Clone repository** → আপনার repository বেছে নিন → কম্পিউটারে একটি ফোল্ডার তৈরি হবে।
3. zip ফাইলটি unzip করুন। ভেতরের **সব ফাইল ও `sec` ফোল্ডার** ঐ clone করা ফোল্ডারে copy করুন। "Replace" চাইলে হ্যাঁ দিন।
4. ঐ ফোল্ডারে পুরোনো `eq` ফোল্ডার থাকলে মুছে দিন।
5. GitHub Desktop-এ বাঁ পাশে বদলে যাওয়া ফাইলের তালিকা দেখাবে। নিচে Summary ঘরে লিখুন `111 final` → **Commit to main** → উপরে **Push origin**।
6. ১–২ মিনিট পর সাইট খুলে **Ctrl + Shift + R** চাপুন (মোবাইলে: tab বন্ধ করে আবার খুলুন)।

**প্রথমবার হলে GitHub Pages চালু করুন:** repository → **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, folder: `/ (root)` → Save।

**মালিকানা:** repository → **Settings → Collaborators**-এ কাউকে যোগ করবেন না। তাহলে শুধু আপনিই ফাইল বদলাতে পারবেন।

## গ. Firebase — Security Rules

1. https://console.firebase.google.com → project `ibfpl-hub` খুলুন।
2. বাঁ পাশে **Build → Firestore Database → Rules**।
3. ভেতরের সব লেখা মুছে `firestore.rules` ফাইলের পুরো লেখা paste করুন → **Publish**।

এটি না করলে Maintenance History, verified user-দের unlock এবং Parcel Import কাজ করবে না।

## ঘ. Firebase — Authentication ও মালিকানা

1. **Build → Authentication → Sign-in method**: শুধু *Email/Password* চালু থাকবে।
2. **Authentication → Settings → Authorized domains**: আপনার GitHub Pages domain (`<username>.github.io`) তালিকায় আছে কি না দেখুন; না থাকলে যোগ করুন।
3. **Project settings (⚙) → Users and permissions**: শুধু আপনার নিজের Google account থাকবে। অন্য কাউকে Owner/Editor দেবেন না।
4. সাইটে আপনার account-এর role `admin` থাকতে হবে। অন্য কারো role admin করবেন না — সাইটের Users tab থেকে শুধু আপনিই role বদলাতে পারেন।

## ঙ. প্রথমবার চালু করা (একবারই)

1. সাইটে নিজের admin account দিয়ে **Log In** করুন।
2. **Stations** tab → "Admin passphrase দিয়ে খুলুন" → passphrase দিন।
3. উপরে **"Verified user-দের জন্য চালু / হালনাগাদ করুন"** বোতাম চাপুন। এরপর যাদের আপনি Verify করবেন, তারা passphrase ছাড়াই দেখতে পাবে।
4. **Parcels** tab → "📥 Parcel Import" অংশে Parcel 76, 77, 78-এর preview দেখুন → **Save** চাপুন।

## চ. নতুন Parcel যোগ করার নিয়ম

1. Parcel-এর ছবিটি Claude-কে দিন।
2. Claude ছবি পড়ে যাচাই করে একটি **Import code** দেবে।
3. সাইটে **Parcels → Import code বসান** → code paste → **Preview** → সব ঠিক থাকলে **Save**।

আগে থাকা parcel কখনো বদলায় না। একই নম্বরে ভিন্ন মান থাকলে লাল চিহ্ন দেখায় এবং কিছু করা হয় না।

## ছ. Backup

- **মাসে একবার:** সাইটের **Report** tab → **Full backup (JSON)** → ফাইলটি নিজের কম্পিউটার বা pendrive-এ রাখুন।
- বড় কোনো পরিবর্তনের আগেও একবার backup নিন।
- সাইটের ফাইলের backup GitHub-এ নিজে থেকেই থাকে (history)।

## জ. নিরাপত্তার নিয়ম

- Admin passphrase কোথাও online-এ লিখবেন না; কাগজে বা offline-এ রাখুন।
- `index.html`-এর ভেতরের Firebase `apiKey` গোপন কিছু নয় — এটি শুধু project চেনায়। আসল সুরক্ষা Security Rules।
- Firebase-এর **service account key** (Admin SDK JSON) এই project-এ লাগে না। কখনো তৈরি করে GitHub-এ দেবেন না।
- চাইলে বাড়তি সুরক্ষা: Google Cloud Console → APIs & Services → Credentials → ঐ API key → *Website restrictions*-এ শুধু আপনার GitHub Pages ঠিকানা দিন।

## ঝ. সমস্যা হলে

| সমস্যা | সমাধান |
|---|---|
| পুরোনো সাইট দেখাচ্ছে | Ctrl + Shift + R; মোবাইলে browser-এর site data মুছুন |
| "Passphrase ভুল, অথবা ফাইল পাওয়া যায়নি" | `sec` ফোল্ডার পুরো আপলোড হয়েছে কি না দেখুন |
| "Not allowed: permission-denied" | `firestore.rules` publish হয়নি, অথবা আপনার account approver/admin নয় |
| ছবি আসছে না | `sec` ফোল্ডারের সব `.bin` ফাইল আপলোড হয়েছে কি না দেখুন |
