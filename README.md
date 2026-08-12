# ASHG 2026 Program Planner

An elegant, fast, static single-page planner for the **ASHG 2026 Annual Meeting** (Montréal, Oct 18–24, 2026). It's a clean, Linear-style front-end over the full conference program so you can browse and filter sessions without fighting the official scheduler app.

- **257 sessions** with **3,100 nested presentations/abstracts**
- Filter by **day**, **session type**, **track**, and **room** (faceted counts update live)
- Full-text **search** across titles, speakers, and abstract text
- **★ My Schedule** — star sessions; saved in your browser (`localStorage`)
- Expandable session detail with description, chairs/speakers, and each talk's time, presenter, and abstract
- Dark, minimal, keyboard-friendly (`/` focuses search), responsive down to mobile

No build step, no framework, no backend — just three files.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire app (HTML + CSS + JS, inline) |
| `data.js` | The program data (`window.ASHG_DATA`), pre-processed with local Montréal times (EDT / UTC−4) |
| `README.md` | This file |

## Run locally

Because `data.js` is loaded as a plain `<script>`, you can just open the file — no server needed:

```bash
open index.html
```

Or serve it (any static server works):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Host on GitHub Pages

1. Create a new repository on GitHub (e.g. `ashg-2026-planner`).
2. Push these files to it:

```bash
git init
git add .
git commit -m "ASHG 2026 program planner"
git branch -M main
git remote add origin https://github.com/<your-username>/ashg-2026-planner.git
git push -u origin main
```

3. In the repo, go to **Settings → Pages**, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`, and save.
4. Your planner will be live at `https://<your-username>.github.io/ashg-2026-planner/` within a minute or two.

## Refreshing the data

The program data was captured from the official app's own cached API responses (AWS AppSync / floq.live) and joined into a single resolved dataset — session times, rooms, tracks, session types, and speakers are all pre-resolved to human-readable names, so the front-end needs no lookups. If the official program changes before the meeting, `data.js` can be regenerated the same way and dropped in without touching `index.html`.

## Notes

- All times are shown in **Montréal local time (Eastern, UTC−4)**, matching the official app.
- Some administrative sessions (industry events, socials, ancillary meetings) don't carry a scientific track — these appear under **"No track assigned"** in the Track filter.
