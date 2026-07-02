# Cruisify — Project Context for Claude Code

## What this is
Single-file static web app (`index.html`): a cruise fleet tracker PoC. HTML + Tailwind CDN + Leaflet. No build step, no dependencies, no backend.

## Deployment
GitHub Pages, deploy-from-branch (`main`, root). Every push to `main` auto-deploys. There is no CI config — Pages handles it.

## Conventions
- Keep it single-file until the AIS integration lands. Do not introduce a bundler or framework for small changes.
- All vessel data lives in the `vessels` array. New telemetry belongs there as data fields, never hardcoded in render functions.
- Visual language: slate-950/900 surfaces, cyan-400 accent, amber-400 for selection/warnings, font-mono for telemetry labels. Match it.
- Marker rendering goes through `markerIcon(ship, selected)` — extend that, don't add parallel marker logic.
- Live AIS is the `connectAIS()`/`handlePositionReport()` block (AISStream.io WebSocket, filtered to the fleet's MMSIs). `aisTick()` is the simulated fallback and only moves ships that have never received live data (`lastSeen` unset). Both mutate `vessels`, call `setLatLng`, and refresh the detail panel if selected — keep that shape.
- API key resolution: `window.CRUISIFY_CONFIG` from `config.js` (gitignored, local dev) → localStorage `cruisify_ais_key` (set via the AIS KEY header button) → none (simulation). Never commit a key; the repo and Pages site are public.

## Workflow
- Mechanical changes (add a vessel, tweak styles, fix bugs): implement directly, verify with `node --check` on extracted JS, commit with a conventional message, push.
- Anything touching architecture (real data feed, multi-file split): propose a plan first.
