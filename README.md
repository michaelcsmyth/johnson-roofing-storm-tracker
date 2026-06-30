# Storm Tracker Dashboard #JR

Dark-mode, interactive storm tracking dashboard for the Phoenix Valley, built for Johnson Roofing's website. Free/no-key data sources only (NWS + Open-Meteo + Windy embed).

## Status: Step 2 of 3 complete — API Integration

## Steps
- [x] **Step 1 — Layout/Wireframe** (2026-06-30): Static dark-mode wireframe built with placeholder data. Navy/gold base palette (matches Insurance Navigator page) + amber/orange/red storm-severity accents. Layout: header → alert ribbon → 3-col (Live Conditions / Radar / Active Alerts) → 2-col (Hail-Rain Estimator / 7-Day Forecast) → footer. Fully responsive (stacks on mobile).
- [x] **Step 2 — API Integration** (2026-06-30): Live data wired and verified in-browser. NWS station `KPHX` for current conditions (temp, wind, gusts, precip, humidity, compass), NWS zone `AZC013` for active Maricopa County alerts (feed + auto-color-coded ribbon banner that hides itself when clear), Open-Meteo for the 7-day forecast, Windy free embed for the interactive radar. Hail/Rainfall/Wind-damage estimator is a heuristic derived from active alert keywords + live wind/precip (clearly labeled as non-official). Auto-refresh: alerts + conditions every 5 min, forecast hourly. All fetches fail gracefully (shows "unavailable — retrying" instead of breaking the page).
- [ ] **Step 3 — Deployment**: Production-ready repo structure, GitHub push, Vercel deployment config, final QA before going live on johnsonroofingaz.com.

## Files
- `(C) Storm Tracker Dashboard.html` — current working build (Step 2). Live data, single self-contained file, no build step.
- `(C) Storm Tracker Dashboard - Wireframe.html` — Step 1 reference. Static layout with placeholder data, kept for design history.

## Data Sources (all free, no API key)
- NWS Observations: `https://api.weather.gov/stations/KPHX/observations/latest`
- NWS Alerts: `https://api.weather.gov/alerts/active?zone=AZC013`
- Open-Meteo Forecast: `https://api.open-meteo.com/v1/forecast` (lat 33.4484, lon -112.0740)
- Windy Radar: free embed iframe, centered on Phoenix

## Design Reference
Palette/style pulled from the Insurance Navigator Page build (`05 Marketing & Ads/Website Redesign/Insurance Navigator Page/`) — navy `#0d1b2a` + gold `#c8973a`, Oswald/Inter fonts. Storm-specific accents added: amber `#ffb300` (watch), orange `#ff6b35` (warning), red `#e63946` (severe).
