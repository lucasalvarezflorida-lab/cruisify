# Cruisify 🚢

A next-gen cruise ship fleet tracker — proof of concept.

**Live demo:** https://lucasalvarezflorida-lab.github.io/cruisify/

## What it does

- Interactive dark-theme map (Leaflet + CartoDB Dark Matter tiles) tracking a simulated cruise fleet in the Caribbean
- Directional ship markers rotated to live heading; docked vessels render as ring dots
- Fleet search by ship name, class, or cruise line
- Per-vessel detail panel: live telemetry (coordinates, speed/heading, tonnage, AIS data freshness), CDC health score, current itinerary, next port of call, and port congestion context
- **Live AIS positions** via AISStream.io WebSocket (bring your own free API key), with a simulated fallback when no key is set
- **Dead reckoning** — when a ship goes quiet between shore receivers, its position is projected along its last course/speed and drawn as a dimmed, dashed marker with "(est.)" coordinates (capped at 6 hours)

## Why it exists

Built to explore product concepts at the intersection of cruise operations and guest-facing data: port congestion awareness, health scores, and itinerary context surfaced in one view. Informed by hands-on experience in cruise line casino sales/support and land-based casino operations.

## Stack

Single-file static app: HTML + Tailwind (CDN) + Leaflet. No build step, no backend — deploys anywhere that serves static files.

## Roadmap

- [x] Replace simulated tick with live AIS via AISStream.io WebSocket (filtered to cruise ship MMSIs)
- [ ] Real itinerary data source
- [ ] Interactive deck plan / blueprint viewer
- [ ] Port congestion scoring from ships-in-port counts

## Getting live data

Positions are simulated until an [AISStream.io](https://aisstream.io) API key (free) is provided:

- **On the site:** click **AIS KEY** in the header and paste your key. It's stored only in your browser's localStorage and sent only to AISStream.
- **Local dev:** create a `config.js` next to `index.html` (it's gitignored):

  ```js
  window.CRUISIFY_CONFIG = { aisApiKey: "your-key-here" };
  ```

Note: AISStream uses terrestrial AIS receivers, so ships far from shore can go quiet for stretches — the detail panel shows how fresh each ship's last report is. Quiet ships are dead-reckoned along their last course and speed (shown as estimated); after 6 hours of silence the projection stops at the last estimate.

## Running locally

Open `index.html` in a browser. That's it.
