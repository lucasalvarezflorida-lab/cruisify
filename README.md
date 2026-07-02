# Cruisify 🚢

A next-gen cruise ship fleet tracker — proof of concept.

**Live demo:** https://YOUR-USERNAME.github.io/cruisify/

## What it does

- Interactive dark-theme map (Leaflet + CartoDB Dark Matter tiles) tracking a simulated cruise fleet in the Caribbean
- Directional ship markers rotated to live heading; docked vessels render as ring dots
- Fleet search by ship name, class, or cruise line
- Per-vessel detail panel: live telemetry (coordinates, speed/heading, tonnage), CDC health score, current itinerary, next port of call, and port congestion context
- Simulated AIS tick — underway vessels advance along their heading every 5 seconds

## Why it exists

Built to explore product concepts at the intersection of cruise operations and guest-facing data: port congestion awareness, health scores, and itinerary context surfaced in one view. Informed by hands-on experience in cruise line casino sales/support and land-based casino operations.

## Stack

Single-file static app: HTML + Tailwind (CDN) + Leaflet. No build step, no backend — deploys anywhere that serves static files.

## Roadmap

- [ ] Replace simulated tick with live AIS via AISStream.io WebSocket (filtered to cruise ship MMSIs)
- [ ] Real itinerary data source
- [ ] Interactive deck plan / blueprint viewer
- [ ] Port congestion scoring from ships-in-port counts

## Running locally

Open `index.html` in a browser. That's it.
