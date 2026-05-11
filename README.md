# Train_

A single-file CrossFit return-to-fitness PWA. Pick equipment, mark injuries,
get day-by-day workouts that scale weights and reps to your 1RMs and current
phase. Log sessions, build your own workouts, run guided timer-driven sessions.

Everything is one `index.html` + a small service worker — no build step, no
dependencies. Data lives in the browser's `localStorage`.

## What's in here

| File | Purpose |
|---|---|
| `index.html` | The whole app — UI, data, state, generator, player, builder |
| `manifest.webmanifest` | PWA manifest (install + standalone display) |
| `sw.js` | Service worker — offline caching |
| `icon.svg` | App icon (used by manifest + Apple touch icon) |
| `images/` | Form-reminder images per movement (`<Movement Name>.png`) |

## Run it

### Locally (quick check)

```powershell
# from this folder
python -m http.server 8000
```

Then open `http://localhost:8000` in a browser. Service worker registration
works on `http://localhost` but not on `file://`, so prefer the server.

### Host it (so you can use it on iPhone)

Two easy options:

1. **GitHub Pages** — push this repo to GitHub, enable Pages (`Settings → Pages
   → Source: main / root`). Wait ~1 minute, open the URL on your phone.
2. **Netlify Drop** — drag the folder onto https://app.netlify.com/drop. You
   get a public URL instantly.

### Install on iPhone (PWA)

1. Open the hosted URL in **Safari**
2. Share → **Add to Home Screen**
3. Open the **installed icon** (not Safari) — this is important on iOS 16.4+
   because the installed PWA has its own scoped storage. Do your onboarding
   inside the installed app.

## Features

- **Today** — generated session for today: warm-up, strength block, WOD
  (timer-aware format), cool-down. Movement reference card collapses by
  default; expand to see images.
- **Workouts** — two tabs:
  - **Recommended** — every default pairing across session types, with a
    live preview (specific movements, reps, weights) you can re-roll.
    Pairings of session types already done this week are dimmed.
  - **Mine** — your custom workouts. Build new ones in a form, edit, delete,
    or export as JSON.
- **Log** — history of saved sessions with weights, reps, RPE, notes.
- **Settings** — equipment, injuries, 1RMs (back squat, front squat, bench,
  deadlift, clean, snatch, push press), blacklist movements, phase
  (auto/manual), recommendations toggle, scaled-mode toggle with
  per-movement scale level pickers, export/import JSON.
- **Reference** — searchable A-Z movement library with images.
- **Session player** — guided run-through with auto-detected timer format
  (EMOM / AMRAP / Rounds For Time / Every-N-min / count-up with cap),
  audible beeps at minute/round boundaries, pause/resume, auto-advance
  through warm-up → strength → WOD → cool-down → logger.

## Data

Stored locally in `localStorage` under `train_state_v1`. Per-device,
per-domain. Export JSON in Settings for backup, import JSON to restore or
move data to another device.

## Adding movement images

Drop a PNG into `images/` with the filename matching the movement's display
name exactly, e.g. `Back Squat.png`, `DB Push Jerk.png`, `Pike Push Up (box).png`.
Movements without images show a striped "image soon" placeholder.
