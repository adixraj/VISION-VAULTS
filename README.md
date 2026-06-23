Project Zenith: The Celestial Eye 🛰️

A real-time cosmic radar built for the web. Pick any point on Earth and see exactly what's passing through the sky above it — live satellites, the ISS, the Sun, the Moon, and planets — updating automatically, with personalized alerts for upcoming flyovers and meteor showers.

Built for **AstralWeb Innovate** by **Team Vision Vaults**.

🔗 **Live demo:** {sparkly-chaja-faeaac.netlify.app}

---

## What this project does

Project Zenith answers one simple question: *"What's above me right now?"*

You open the page, pick a location (search, click the map, or use GPS), and the platform shows you:

- **A live ground-track map** — see real satellites moving across a world map in real time, click any of them for live stats (altitude, speed, whether they're currently above your horizon)
- **The Zenith Dial** — a radar-style instrument that shows everything currently visible in your sky, with the center representing straight up (your zenith) and the edge representing your horizon
- **Live object tracking** — the International Space Station, Hubble Space Telescope, a Starlink satellite, and a weather satellite, all tracked using real orbital data
- **Sun, Moon, and planet positions** — calculated live using real astronomical formulas, so you always know where they are relative to your location
- **An event feed** — upcoming ISS flyovers, well-placed planets, and the next annual meteor shower, personalized to your exact coordinates

Everything updates automatically every 5 seconds — no refreshing needed.

---

## Functionality breakdown

| Feature | How it works |
|---|---|
| Satellite positions | Real orbital element data (TLE) is fetched from CelesTrak, then converted into live latitude/longitude/altitude using the `satellite.js` library, which runs the same SGP4 orbital math real ground stations use |
| Location picker | Click anywhere on the map, type a city name, or tap "Use my location" to access your browser's GPS |
| Sun / Moon / planet positions | Calculated using standard low-precision astronomical formulas — no external API needed, works instantly and offline |
| Event alerts | The app scans the next 36 hours of satellite movement to predict flyover times, checks which planets will be well-placed tonight, and looks up the next annual meteor shower |
| Offline fallback | If CelesTrak can't be reached (network issue, rate limit, etc.), the app automatically switches to a small set of saved sample satellite data so the demo never breaks |

---

## Setup instructions

This is a **single HTML file** — there is no build step, no installation, and nothing to compile.

### Option 1 — Just open it
Download `index.html` and double-click it. It opens directly in your browser. Some live features (satellite data, location search) need an internet connection to work, since they fetch real data from external sources.

### Option 2 — Run it on a local server (optional, slightly smoother for testing)
```bash
# From the folder containing index.html
python3 -m http.server 8000
```
Then open `http://localhost:8000` in your browser.

### Option 3 — Deploy it for free (what we used for our live demo)
- **Netlify:** go to [app.netlify.com/drop](https://app.netlify.com/drop) and drag in `index.html`. You get a free public link instantly.
- **GitHub Pages:** upload `index.html` to a GitHub repo, rename it `index.html` if needed, then go to Settings → Pages → enable Pages from the `main` branch. GitHub gives you a free public link.

No payment, domain purchase, or account billing setup is required for either option — both have a free tier that's more than enough for this project.

---

## API keys required

**None.** This was an intentional design decision — every data source this project uses is free and keyless:

| Source | What it provides | API key needed? |
|---|---|---|
| [CelesTrak](https://celestrak.org) | Live satellite orbital data (TLE) | No |
| [OpenStreetMap Nominatim](https://nominatim.org) | Location search (city name → coordinates) | No |
| [CARTO](https://carto.com) | Dark-themed map tiles | No |
| Browser Geolocation API | "Use my location" GPS button | No (just browser permission) |

If you fork this project and want to extend it with NASA APIs (like NASA Horizons for higher-precision planet positions, or NASA APOD for daily images), those require a free key from [api.nasa.gov](https://api.nasa.gov) — but the current version does not use them.

---

## Dependencies

All loaded directly from public CDNs inside `index.html` — nothing to install:

- **[Leaflet.js](https://leafletjs.com/)** (v1.9.4) — the interactive 2D map
- **[satellite.js](https://github.com/shashwatak/satellite.js)** (v5.0.0) — orbital mechanics / SGP4 propagation
- **Google Fonts** — Space Grotesk, Inter, JetBrains Mono

There is no `package.json`, no `node_modules`, and no npm install step. Opening the file in a browser with an internet connection is enough for every dependency to load.

---

## Project structure
We chose a single-file structure deliberately for this round — it's the fastest way to demo a working prototype with zero setup friction for judges.

---

## What's simplified for this demo (and what a full version would add)

| In this prototype | In a full production version |
|---|---|
| 4 tracked satellites (ISS, Hubble, one Starlink, one weather satellite) | Full CelesTrak catalog (20,000+ satellites) with category filters |
| Planet positions from lightweight orbital formulas | NASA Horizons API for arc-second precision |
| 2D map only (Leaflet) | Optional 3D globe view (CesiumJS) for desktop users |
| Event predictions recalculated in-browser every 60 seconds | Server-side cron job pre-computing and caching predictions |

---

## Team

**Vision Vaults** — AstralWeb Innovate, Project Zenith: The Celestial Eye
