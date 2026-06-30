# Storm Tracker Dashboard — Project Notes
#JR

**Created:** 2026-06-30
**Status:** Completed (for now) — live on GitHub, one manual Vercel connect step remains

---

## What This Is

A dark-mode, interactive storm tracking dashboard built for Johnson Roofing's website, scoped to the Phoenix Valley (Maricopa County, AZ). Designed to eventually live as a public page on johnsonroofingaz.com so homeowners can check live storm conditions — and so the page itself drives inspection requests during active weather.

---

## Why This Exists

Storm damage is Johnson Roofing's highest-intent lead source. A live, branded storm tracker gives the website a reason for homeowners to visit *before* they think to call a contractor, and puts a "Schedule Online / Call Now" CTA in front of them at the exact moment they're checking the weather.

---

## What's Built

| Feature | Detail |
|---|---|
| Live Conditions | Temp, wind speed/direction (compass), gusts, precip, humidity — NWS station KPHX |
| Active Alerts | Live NWS alerts for Maricopa County (zone AZC013), feed + auto-color-coded ribbon banner |
| Interactive Radar | Free Windy embed, centered on Phoenix, zoom/playback controls |
| Hail & Rainfall Estimator | Heuristic risk gauges (Low/Mod/High/Extreme) derived from active alerts + live wind/precip — clearly labeled as non-official |
| 7-Day Forecast | Open-Meteo daily highs/lows + weather icons |
| Storm Risk + CTA banner | Always-visible, risk-color-coded banner with "Schedule Online" (links to johnsonroofingaz.com) and "Call Now: 480-467-4572" (tel: link) |
| Branding | Real Johnson Roofing logo, top-left, white badge for contrast against the dark theme |

All data sources are free / unauthenticated — no API keys, nothing to rotate or expire:
- NWS Observations: `api.weather.gov/stations/KPHX/observations/latest`
- NWS Alerts: `api.weather.gov/alerts/active?zone=AZC013`
- Open-Meteo: `api.open-meteo.com/v1/forecast`
- Windy: free embed iframe

Auto-refresh: alerts + conditions every 5 min, forecast hourly. Every fetch fails gracefully (shows "unavailable — retrying" instead of breaking the page).

---

## Design Decisions

- Palette pulled from the existing Insurance Navigator Page brand system (navy `#0d1b2a` + gold `#c8973a`, Oswald/Inter fonts), extended with amber/orange/red storm-severity accents so the page reads calm on a clear day and urgent during an active storm.
- Built process was staged and checked in at each phase rather than delivered all at once: Layout/Wireframe → API Integration → Deployment → branding/CTA polish.
- Plain HTML/CSS/JS, single `index.html`, zero build step — matches the pattern of the Pricing Calculator and Insurance Navigator builds, and deploys to Vercel with no config.
- Logo placed in a white badge rather than directly on the dark header background, since the source logo file is navy-on-transparent and would otherwise disappear into the dark theme.
- CTA banner risk level is driven by the same hail/rain/wind estimator as the gauges below it, so the messaging and color always match what the rest of the page is showing — no separate logic to keep in sync.

---

## Repo & Deployment

- GitHub: https://github.com/michaelcsmyth/johnson-roofing-storm-tracker (public)
- Installed GitHub CLI (`gh`) and authenticated as michaelcsmyth to create/push the repo — no plaintext token in the remote config (flagged that the older Pricing Calculator repo does have one embedded; worth rotating that token when there's time).
- **Pending:** connect the repo in Vercel (vercel.com → Add New Project → Import `johnson-roofing-storm-tracker` → Deploy, no config needed) to get a live public URL, then point a johnsonroofingaz.com subdomain/page at it.

---

## Pending / To Do

- [ ] Connect repo to Vercel for a live public URL
- [ ] Decide where this lives on johnsonroofingaz.com (own page, embedded iframe, nav link)
- [ ] Once live, link from the main site nav and any storm-damage marketing/ads
- [ ] Consider rotating the exposed GitHub token in the Pricing Calculator repo

---

## Files in This Folder

| File | Description |
|---|---|
| `index.html` | Deployment entry point (GitHub/Vercel) |
| `(C) Storm Tracker Dashboard.html` | Working build, kept in sync with `index.html` |
| `(C) Storm Tracker Dashboard - Wireframe.html` | Step 1 reference — static layout, placeholder data |
| `jr-logo.png` | Johnson Roofing logo asset |
| `README.md` | GitHub-facing repo readme |
| `(C) Storm Tracker Dashboard - Project Notes.md` | This file — background, decisions, to-dos |
