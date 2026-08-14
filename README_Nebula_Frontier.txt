NEBULA FRONTIER 2.0
Single-file sci-fi tile-placement browser strategy game

RUN LOCALLY
1. Open index.html in a modern browser.
2. Choose Player vs AI or Two Players (same device).
3. Set the tile count (18–120), seed, commanders, AI difficulty and optional skirmish rules.
4. Launch the expedition.

HOST ONLINE
Upload index.html to any static host such as GitHub Pages, Netlify, Cloudflare Pages or a normal web server.
No build process, server code, CDN, framework or external library is required.

PLACEMENT + ROTATION CONTROLS
- GREEN marker: the current orientation fits. Click to place immediately.
- AMBER marker: the location is legal only after rotation. Click the amber marker and the navigation assist automatically chooses a legal rotation and places the tile.
- RED marker: impossible for the current tile in every orientation.
- Amber markers now display the required rotation, such as ↻90°, ↺90° or ↻180°.
- Hover over a legal/amber board cell for a translucent tile ghost and placement instruction.
- Q rotates 90° counter-clockwise.
- E or R rotates 90° clockwise.
- Right-click the board rotates 90° clockwise.
- The 0° / 90° / 180° / 270° selector shows how many legal board positions exist at each exact orientation.
- “Best orientation” selects the rotation with the most legal positions.
- “Find a legal spot” rotates if necessary, centres a valid position and highlights it in cyan. Press F for the same action.
- Mouse wheel zooms.
- Shift + drag pans.
- Fit-board button recentres the map.

2.0 UI IMPROVEMENTS
- Large live placement coach explains whether rotation is optional, required or impossible.
- Floating board guide keeps placement instructions visible without looking away from the map.
- Exact-angle rotation selector with per-orientation legal-placement counts.
- Larger current-tile preview and clear north/orientation reference.
- Improved placement legend and keyboard hints.
- Hover ghost preview before committing a tile.
- Suggested-placement cyan highlight.
- Mobile inspector/panel toggle.
- Clearer impossible-placement feedback and automatic rotation feedback in the mission log.

GAME FEATURES
- Procedural square sci-fi sector tiles
- Slipstream Lanes, Nebula Regions, Worlds, Stations, signal/anomaly/artifact symbols
- Connected-feature occupancy and scoring
- Optional network skirmishes
- Six original commander characters with implemented passive abilities
- Configurable 18–120 tile stack and deterministic seed
- Player-vs-AI and two-player hot-seat play
- Hot-seat privacy handoff overlay
- Final scoring for incomplete occupied features
- Save/resume through browser localStorage
- Self-contained HTML/CSS/JavaScript; no external assets
