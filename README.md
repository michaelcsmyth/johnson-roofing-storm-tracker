# Storm Tracker Dashboard #JR

Dark-mode, interactive storm tracking dashboard for the Phoenix Valley, built for Johnson Roofing's website. Free/no-key data sources only (NWS + Open-Meteo + Windy embed).

## Status: Completed for now (2026-06-30) — GitHub live, Vercel connect still pending

See `(C) Storm Tracker Dashboard - Project Notes.md` for full project notes, decisions, and to-dos.

## Steps
- [x] **Step 1 — Layout/Wireframe** (2026-06-30): Static dark-mode wireframe built with placeholder data. Navy/gold base palette (matches Insurance Navigator page) + amber/orange/red storm-severity accents. Layout: header → alert ribbon → 3-col (Live Conditions / Radar / Active Alerts) → 2-col (Hail-Rain Estimator / 7-Day Forecast) → footer. Fully responsive (stacks on mobile).
- [x] **Step 2 — API Integration** (2026-06-30): Live data wired and verified in-browser. NWS station `KPHX` for current conditions (temp, wind, gusts, precip, humidity, compass), NWS zone `AZC013` for active Maricopa County alerts (feed + auto-color-coded ribbon banner that hides itself when clear), Open-Meteo for the 7-day forecast, Windy free embed for the interactive radar. Hail/Rainfall/Wind-damage estimator is a heuristic derived from active alert keywords + live wind/precip (clearly labeled as non-official). Auto-refresh: alerts + conditions every 5 min, forecast hourly. All fetches fail gracefully (shows "unavailable — retrying" instead of breaking the page).
- [~] **Step 3 — Deployment** (2026-06-30): GitHub repo created and pushed: https://github.com/michaelcsmyth/johnson-roofing-storm-tracker (`index.html` at root, zero build config needed — Vercel auto-detects static sites). Installed GitHub CLI (`gh`) and authenticated as michaelcsmyth to do this. Remaining: connect the repo in Vercel ("Import Project" from GitHub) to get a live public URL, then point the johnsonroofingaz.com website to it.

## Files
- `index.html` — deployment entry point (Vercel/GitHub). Identical to the working build below.
- `(C) Storm Tracker Dashboard.html` — working build (Step 2/3), kept in sync with `index.html`. Live data, single self-contained file, no build step.
- `(C) Storm Tracker Dashboard - Wireframe.html` — Step 1 reference. Static layout with placeholder data, kept for design history.
- `jr-logo.png` — Johnson Roofing logo asset (extracted from the Pricing Calculator build), referenced by both HTML files.

## Post-Step-3 additions (2026-06-30)
- Added the real Johnson Roofing logo to the header (top-left, white badge for contrast against the dark theme — the logo itself is navy-on-transparent).
- Added a Storm Risk + CTA banner at the top of the page: shows a live risk level (Low/Moderate/High/Extreme, driven by the same hail/rain/wind estimator) plus two always-visible CTAs — "Schedule Online" (links to johnsonroofingaz.com) and "Call Now: 480-467-4572" (tel: link). Banner color escalates (gold → orange → red) as risk rises.

## Repo & Deployment
- GitHub: https://github.com/michaelcsmyth/johnson-roofing-storm-tracker (public)
- To deploy: go to vercel.com → Add New Project → Import `johnson-roofing-storm-tracker` from GitHub → Deploy (no config needed, it's a static `index.html`).

## Data Sources (all free, no API key)
- NWS Observations: `https://api.weather.gov/stations/KPHX/observations/latest`
- NWS Alerts: `https://api.weather.gov/alerts/active?zone=AZC013`
- Open-Meteo Forecast: `https://api.open-meteo.com/v1/forecast` (lat 33.4484, lon -112.0740)
- Windy Radar: free embed iframe, centered on Phoenix

## Design Reference
Palette/style pulled from the Insurance Navigator Page build (`05 Marketing & Ads/Website Redesign/Insurance Navigator Page/`) — navy `#0d1b2a` + gold `#c8973a`, Oswald/Inter fonts. Storm-specific accents added: amber `#ffb300` (watch), orange `#ff6b35` (warning), red `#e63946` (severe).
