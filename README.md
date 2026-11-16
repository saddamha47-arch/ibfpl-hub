# 111

Engineering dashboard. Single-page web app hosted on GitHub Pages (free), with Firebase Authentication and Cloud Firestore (free Spark plan) for sign-in and shared records.

Owner and sole administrator: the repository owner. No collaborators are required.

## Files
| File / folder | Purpose | Goes to |
|---|---|---|
| `index.html` | The whole application | GitHub repo root |
| `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png` | Installable web-app support | GitHub repo root |
| `sec/` | Encrypted data and photos (AES-256-GCM); unreadable without the key | GitHub repo root (folder) |
| `flow3d.html`, `flow3d_full.html`, `three.min.js`, `narration_*.mp3`, `ibfpl_3d_summary.mp4` | 3D flow guide and video | GitHub repo root |
| `.nojekyll` | Tells GitHub Pages to serve files as-is | GitHub repo root |
| `firestore.rules` | Firestore security rules | Firebase console → Firestore → Rules (not served by the site) |
| `firebase.json` | Optional: lets the Firebase CLI deploy the rules | Keep with the source; not required for the website |
| `SETUP_GUIDE_BN.md` | Step-by-step setup and deployment guide (Bangla) | Read only |

## Deploy
See `SETUP_GUIDE_BN.md`. Short version:
1. Put every file above (and the whole `sec` folder) in the repository root, names unchanged.
2. GitHub → Settings → Pages → Deploy from a branch → `main` / root.
3. Firebase console → Firestore → Rules → paste `firestore.rules` → Publish.
4. Sign in as admin, unlock once with the admin passphrase, press the share button on the Stations tab.

## Modules
Dashboard · Parcels (with validated import) · Notices · Pipeline Guide · Map · 3D Flow · Stations (equipment encyclopedia + maintenance history) · Connections (training diagrams) · DG & Fuel · Bills (electricity + internet) · Executive Brief · Oil Price · SOP · P&ID · Emergency · Vault · Academy · 6-Month Plan · Case Studies · I&E Tools · Work Orders · Schedule · Leave · Documents · Reports & Backup.

## Access protection
- Station data, photos, bills, SOP, P&ID, emergency data, map, executive brief and the built-in parcel history are stored encrypted in `sec/`. They open only for the admin (passphrase) or for users the admin has marked **Verified** (key delivered from Firestore `secure/main`).
- Firestore records are governed by `firestore.rules`: only the admin can change roles; only approvers can write operational records.
- The Firebase web config inside `index.html` (apiKey, projectId) is a public identifier by design, not a secret. Security comes from the rules. No Admin SDK key or service-account file is used anywhere in this project, and none must ever be added to the repository.
- The admin passphrase is not stored in any file. Keep it offline.

## Parcel data entry
New parcel reports are read from the survey image, checked (tank rows must add up to the total; SV-01 comparison must be within limits) and offered in **Parcels → Parcel Import** with a preview. Existing parcels are never overwritten; a parcel number that already exists with different values is shown as a conflict and left untouched.

## Backup
Reports tab → **Full backup (JSON)** downloads all Firestore records. Do this monthly and before any bulk change. The GitHub repository history is the backup of the site files.

## Data rules
- Values come from site photographs and documents; anything not verified is marked "Information Required".
- Connection diagrams are training illustrations, not as-built drawings.
- Never commit passwords, the admin passphrase, IP addresses, network configuration or SCADA backups.
