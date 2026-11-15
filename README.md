# 111-IBFPL

Engineering reference and management dashboard for the India–Bangladesh Friendship Pipeline (IBFPL), Petroleum Transmission Company PLC.

## Files
| File / folder | Purpose |
|---|---|
| `index.html` | The whole application (single file) |
| `manifest.json`, `sw.js`, `icon-*.png` | Installable web app support |
| `eq/` | Equipment photos (`eq/sv1`, `eq/sv5`, …) used by the Stations tab |
| `flow3d.html`, `flow3d_full.html`, `three.min.js`, `narration_*.mp3` | Interactive 3D flow guide |
| `ibfpl_3d_summary.mp4` | Summary video (under 25 MB) |
| `firestore.rules` | Firebase security rules (paste in Firebase console, not served by the site) |

## Deploy (GitHub Pages)
1. Upload all files and the `eq` folder to the repository root, keeping names unchanged.
2. Settings → Pages → Deploy from branch → `main` / root.
3. In Firebase console, publish `firestore.rules`.

## Main modules
Dashboard · Parcels · Notices · IBFPL Guide · Map · 3D Flow · Stations (equipment encyclopedia) · Connections (wiring/HART/communication training diagrams) · DG & Fuel calculator · Bills (electricity) · Oil Price · SOP · P&ID · Emergency · Vault · Academy · Work Orders · Schedule · Leave · Documents · Reports.

## Data rules
- Nameplate data comes from site photographs; anything not verified is marked "Information Required".
- Connection diagrams are training illustrations, not as-built IBFPL drawings.
- Do not commit passwords, IP addresses, network configuration or SCADA backups to this repository. Keep the repository private if operational details are added.
