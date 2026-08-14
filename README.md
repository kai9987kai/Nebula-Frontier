# Nebula Frontier 2.0

**Nebula Frontier** is a self-contained browser strategy game about exploring and connecting a procedurally assembled science-fiction frontier one sector at a time. Players draw square sector tiles, rotate them, connect compatible edges, deploy operatives onto networks and worlds, compete for control, complete features for points, and attempt to finish the expedition with the highest command score.

The game is designed as an **original sci-fi tile-placement ruleset** inspired by the broader connected-feature board-game genre. It is not a reproduction of Carcassonne, Carcassonne: Star Wars, or any other licensed game, and it does not require or embed their artwork, trademarks, components, or external assets.

Nebula Frontier 2.0 is delivered as a **single HTML file** containing the complete HTML, CSS, JavaScript, procedural artwork, UI, AI, rules, and save system. There is no build step, package manager, server-side code, framework, CDN, or runtime dependency.

---

## Contents

1. [Highlights](#highlights)
2. [Quick start](#quick-start)
3. [Game objective](#game-objective)
4. [Game setup](#game-setup)
5. [Turn sequence](#turn-sequence)
6. [Tile placement and rotation](#tile-placement-and-rotation)
7. [Placement colours](#placement-colours)
8. [Operatives and feature control](#operatives-and-feature-control)
9. [Skirmishes](#skirmishes)
10. [Scoring](#scoring)
11. [Commanders](#commanders)
12. [Sector tile catalogue](#sector-tile-catalogue)
13. [AI opponent](#ai-opponent)
14. [Two-player hot-seat mode](#two-player-hot-seat-mode)
15. [Controls](#controls)
16. [User interface guide](#user-interface-guide)
17. [Seeds and deterministic decks](#seeds-and-deterministic-decks)
18. [Saving and resuming](#saving-and-resuming)
19. [Running locally](#running-locally)
20. [Hosting online](#hosting-online)
21. [GitHub Pages deployment](#github-pages-deployment)
22. [Technical architecture](#technical-architecture)
23. [Customising the game](#customising-the-game)
24. [Browser support](#browser-support)
25. [Troubleshooting](#troubleshooting)
26. [Known limitations](#known-limitations)
27. [Ideas for future development](#ideas-for-future-development)
28. [Version 2.0 changes](#version-20-changes)
29. [Project status and licensing](#project-status-and-licensing)

---

## Highlights

Nebula Frontier 2.0 currently includes:

- A complete browser-playable sci-fi tile-placement game.
- **Player vs AI** mode.
- **Two-player hot-seat** mode on the same computer, tablet, or phone.
- A configurable match length from **18 to 120 tiles**.
- A deterministic **world seed** system so the same seed and tile count reproduce the same shuffled sector deck.
- Six original commander characters, each with a functional special ability.
- Procedurally rendered sci-fi sector artwork generated directly with the HTML5 Canvas API.
- Slipstream Lanes, Nebula Regions, Worlds, Stations, Signals, Anomalies, Artifacts, faction markers, and Operatives.
- Feature tracing and connected-network detection across multiple tiles.
- Immediate scoring for completed features.
- Reduced final scoring for incomplete occupied features.
- Optional network-merger skirmishes using dice.
- A mission log recording important placement, deployment, scoring, battle, and rotation events.
- Automatic browser saving using `localStorage`.
- Resume support from the setup screen.
- Board zooming, panning, recentering, and automatic fitting.
- Hover previews before placement.
- Legal-placement detection across all four tile orientations.
- A dedicated placement coach explaining whether rotation is optional, required, or impossible.
- Exact orientation selection at **0°, 90°, 180°, and 270°**.
- One-click **Find a legal spot** assistance.
- One-click **Best orientation** assistance.
- Auto-rotation when an amber placement marker is selected.
- Keyboard and mouse shortcuts for faster play.
- A privacy handoff screen for same-device multiplayer.
- Responsive layout behaviour for smaller displays.
- No external libraries or assets.

---

## Quick start

1. Open `index.html` in a modern browser.
2. Choose either **Player vs AI** or **Two players — same device**.
3. Enter the player names.
4. Choose a tile count between **18 and 120**.
5. Enter or keep the world seed.
6. If playing against AI, select an AI difficulty.
7. Enable or disable optional skirmishes.
8. Enable or disable the hot-seat privacy handoff screen.
9. Choose a commander for each side.
10. Press **Launch expedition**.
11. On your turn, inspect the current sector in the right-hand panel.
12. Place it on a highlighted legal board position.
13. Rotate when necessary using the board marker, rotation controls, keyboard, or right-click.
14. Optionally deploy an operative.
15. Completed features are scored automatically.
16. Continue until the tile stack is exhausted.
17. Final scoring is resolved automatically and the highest-scoring explorer leads the expedition.

---

## Game objective

The goal is to finish the expedition with more command points than your opponent.

You gain points by controlling and completing connected features such as:

- **Slipstream Lanes** — navigational routes running between sector edges.
- **Nebula Regions** — connected clouds occupying compatible tile edges.
- **Worlds** — planets that become complete when all eight neighbouring grid positions are occupied.
- Special tile details such as **Signals**, **Anomalies**, and **Artifacts** can increase feature value.
- Commander abilities can add additional points under specific conditions.

Operatives are the main control resource. Deploying them can secure valuable features, but an operative committed to an unfinished feature remains unavailable until that feature completes or until another game effect returns it to reserve.

This creates the central strategic tension: **score now, build for later, block your rival, or conserve operatives for future opportunities**.

---

## Game setup

The setup screen exposes the main match parameters.

### Game mode

#### Player vs AI

One human player competes against the ORION AI. The AI automatically places tiles, decides whether to deploy an operative, and evaluates placement opportunities according to the chosen difficulty.

#### Two players — same device

Two human players alternate turns on the same browser. If the privacy handoff option is enabled, the game displays a pass-the-device overlay between turns so the incoming player can reveal their own turn deliberately.

### Player names

Both player names are editable. Names are displayed on the scoreboard, player cards, mission log, handoff screen, and scoring messages.

### Tile count

The match tile stack is configurable from **18 to 120 sectors**.

Suggested lengths:

- **18–30 tiles:** quick game or testing session.
- **40–60 tiles:** medium-length match.
- **72 tiles:** standard long-form setting used by the default configuration.
- **90–120 tiles:** large or "epic" frontier.

The tile count affects match duration and how much room there is for long-term network planning.

### World seed

The seed controls the pseudo-random tile sequence and tile visual variation.

The game uses a deterministic seeded pseudo-random generator. In practical terms:

> **Same seed + same tile count = same generated deck sequence.**

This makes seeds useful for:

- replaying a particularly interesting match,
- comparing strategies,
- AI testing,
- challenge seeds,
- debugging,
- tournament-style shared scenarios.

### AI difficulty

Three AI settings are available:

- **Cadet — relaxed**
- **Navigator — tactical**
- **Strategist — aggressive**

Higher difficulty reduces randomness in AI placement selection and gives greater weight to connected placement quality.

### Optional skirmishes

The **Skirmish when rival networks merge** switch enables the dice-based conflict system described later in this README.

Turning this off produces a more peaceful network-building game while retaining normal feature scoring and control rules.

### Hot-seat privacy handoff

When enabled in two-player mode, a full-screen handoff prompt appears between turns. This is useful on a shared tablet or laptop and clearly indicates whose turn is next.

---

## Turn sequence

A normal turn has four conceptual stages.

### 1. Draw the current sector

The current tile is drawn automatically from the shuffled stack and appears in the sector inspector.

The interface immediately analyses every open frontier cell and all four rotations of the tile.

### 2. Place the sector

Choose a legal highlighted board position.

All touching edges must match:

- **Void ↔ Void**
- **Slipstream Lane ↔ Slipstream Lane**
- **Nebula ↔ Nebula**

A tile can touch several existing tiles at once, so every touching side must be compatible simultaneously.

### 3. Deploy an operative or keep it in reserve

After placing a tile, the game displays any eligible deployment options created on that tile.

An operative can potentially be placed on:

- a Slipstream Lane,
- a Nebula Region,
- a World.

You may also keep the operative in reserve and end the deployment phase without placing one.

### 4. Resolve conflicts and scoring

If enabled, newly connected rival networks may trigger a skirmish.

The engine then checks whether the newly placed tile completed:

- a Slipstream Lane,
- a Nebula Region,
- the World on the tile,
- or a neighbouring World whose final surrounding position was just filled.

Completed occupied features score automatically, and their operatives return to reserve.

The next player's turn then begins.

---

## Tile placement and rotation

Version 2.0 substantially expands the placement interface because knowing **whether a tile can rotate into a position** is one of the most important parts of the game.

### Current orientation

The sector preview has a small **N** marker at its top edge. This makes the displayed orientation explicit.

The inspector also displays the current angle:

- `0°`
- `90°`
- `180°`
- `270°`

### Exact-angle selector

Four orientation buttons are shown beside the current tile.

Each button reports how many legal placements exist when the tile is rotated to that exact orientation. For example:

- `0° — 3 legal`
- `90° — no fit`
- `180° — 1 legal`
- `270° — 5 legal`

This lets you evaluate rotation before changing the tile.

### Rotate buttons

The side panel contains manual rotation controls for turning the tile left or right.

### Keyboard rotation

While a human player is in the placement phase:

- **Q** — rotate 90° counter-clockwise.
- **E** — rotate 90° clockwise.
- **R** — rotate 90° clockwise.

### Right-click rotation

Right-click the board during the placement phase to rotate the current tile **90° clockwise**.

This is particularly convenient when using the mouse to inspect several frontier positions rapidly.

### Auto-rotation from amber markers

You do not have to rotate manually.

If a frontier cell is amber, the tile is illegal there at its current angle but **does fit in at least one other orientation**.

Clicking an amber marker automatically:

1. identifies a valid rotation,
2. rotates the tile,
3. places it at that position.

The marker itself displays the required rotation instruction, such as:

- `↻90°`
- `↺90°`
- `↻180°`

### Best orientation

The **Best orientation** control chooses the orientation with the greatest number of currently legal board positions.

This does not necessarily mean it is strategically the strongest move; it simply maximises placement flexibility.

### Find a legal spot

The **Find a legal spot** control searches current legal moves, rotates when required, centres the board on a usable position, and marks a recommended cell in cyan.

Press **F** for the keyboard equivalent.

This feature is especially useful when the frontier becomes large and the valid target is off-screen.

### Hover ghost preview

Hover over a green or amber location to preview the sector on the board before committing.

For amber positions, the ghost preview uses the orientation that would be applied automatically.

The preview label states either:

- **CLICK TO PLACE**, or
- **AUTO [rotation] + PLACE**.

---

## Placement colours

The placement system uses three primary colours plus a cyan suggestion state.

### Green — legal now

A green marker means:

> The tile can be placed here in its **current orientation**.

No rotation is necessary.

Click the green cell to place the tile immediately.

### Amber — legal after rotation

An amber marker means:

> The tile does **not** fit here at the current angle, but at least one other rotation is legal.

Clicking the amber cell automatically rotates and places the tile.

You can also read the rotation shown inside the marker and perform it manually.

### Red — impossible for this tile

A red marker means:

> This frontier cell cannot accept the current tile in **any of its four orientations**.

Rotating the tile will not make that particular position legal.

This is different from an amber marker, where rotation solves the mismatch.

### Cyan — suggested legal placement

A cyan-highlighted cell is produced by **Find a legal spot**.

It is a convenience hint, not an additional rule state.

### Placement coach

The inspector summarises the whole placement situation as one of three states:

#### Rotation optional — tile fits now

At least one green placement exists in the current orientation.

#### Rotation required

The current orientation has no green placements, but one or more amber placements are available after rotation.

#### No legal placement

The current sector cannot connect to the frontier in any orientation. The game attempts to handle unplayable sectors automatically rather than leaving the player stuck.

---

## Operatives and feature control

Each commander has a reserve of operatives represented by stylised faction figures.

After placing a tile, you can deploy one operative to an eligible feature on that newly placed tile.

### Occupancy rule

A connected Slipstream Lane or Nebula Region cannot receive a new operative if that connected feature already contains an operative.

The important word is **connected**. A feature may extend through many tiles. The game traces the complete network rather than checking only the newly placed sector.

This allows separate occupied features to be established independently and later joined together by a future tile.

### Worlds

A World can also receive an operative if that World itself is currently unoccupied.

World occupancy is associated with that specific planet tile rather than an edge network.

### Returning operatives

When a completed feature scores during the game, operatives on that feature return to their owners' reserves and can be deployed again on future turns.

If a feature remains incomplete at game end, final scoring occurs without a normal subsequent turn.

### Sentinel K-7

Sentinel K-7's **Expanded Chassis** ability increases its owner's starting reserve by one operative.

---

## Skirmishes

Skirmishes are optional.

They occur when a newly placed tile causes previously separate occupied networks to merge so that operatives belonging to both players now occupy the same connected Slipstream Lane or Nebula Region.

### Dice pool

For each side:

- each operative present contributes to the side's dice pool,
- a matching faction mark in the feature can contribute an additional die,
- the pool is capped at **3 dice**.

Each player rolls their pool and uses their **highest die result**.

### Winning

The side with the higher top result wins the skirmish.

The defeated side's operatives on that feature are removed from the network and returned to reserve.

### Compensation

The defeated player receives compensation points based on the number of dice they used in that skirmish.

This softens the cost of losing an established network while still giving the winner control of the merged feature.

### Ties

If both sides have the same highest result:

- both tied sides gain a point,
- the dice are rolled again.

The engine includes a safety limit against an endless sequence of ties. If repeated ties persist beyond the internal limit, the skirmish is treated as a deadlock and the forces remain.

### Vexa Nox

Vexa Nox's **Combat Algorithms** ability adds `+1` to their highest rolled die in a skirmish, capped at a final result of 6.

---

## Scoring

Scoring is handled automatically by the engine.

### Majority

For connected Lane and Nebula features, the player with the greatest number of operatives on that feature receives the feature score.

If both players are tied for the highest operative count, both are treated as winners and receive the full feature value.

### Completed Slipstream Lane

A completed Slipstream Lane scores:

**1 point per sector in the connected lane + 2 points per Signal in the feature.**

Astra Venn receives an additional **+1** when scoring a completed Slipstream Lane.

### Completed Nebula Region

A completed Nebula Region scores:

**2 points per sector in the connected region + 1 point per Anomaly in the feature.**

Dr. Orin Vale receives an additional **+1** when scoring a completed Nebula Region.

### Completed World

A World is complete when all **8 surrounding grid positions** are occupied by tiles.

During normal scoring, its value is:

**1 point for the World tile + 1 point for each surrounding tile + 2 points if the World contains an Artifact.**

A fully surrounded artifact World is therefore worth 11 base points.

Nyra Sol receives an additional **+2** when scoring a completed World.

### Stations and Kade Flux

Kade Flux has **Salvage Rights**. The first time during a turn that Kade deploys to a sector containing a Station, that player gains **+1 point**.

### Final scoring

When the deck is exhausted, remaining occupied features receive reduced values.

#### Remaining Slipstream Lane

**1 point per sector + 1 point per Signal.**

#### Remaining Nebula Region

**1 point per sector + 1 point per Anomaly.**

#### Remaining World

**1 point for the World + 1 point per currently occupied neighbouring position + 1 point for an Artifact.**

Normal commander completion bonuses do not apply to final-scoring features.

---

## Commanders

Nebula Frontier contains six original commanders.

### Astra Venn — Slipstream Pathfinder

**Ability: Route Savant**

Whenever Astra's player scores a completed Slipstream Lane, gain **+1 point**.

Recommended for players who prefer long routes, network engineering, and predictable completion scoring.

### Dr. Orin Vale — Nebula Xenobiologist

**Ability: Anomaly Specialist**

Whenever Orin's player scores a completed Nebula Region, gain **+1 point**.

Recommended for players who prefer territorial regions and anomaly-rich sectors.

### Nyra Sol — Interstellar Envoy

**Ability: World Accord**

Whenever Nyra's player scores a completed World, gain **+2 points**.

Recommended for players willing to commit operatives for longer periods while building around planets.

### Kade Flux — Rift Salvager

**Ability: Salvage Rights**

The first time each turn Kade's player deploys onto a sector containing a Station, gain **+1 point**.

Recommended for opportunistic play around junctions, endpoints, and station-heavy tile configurations.

### Sentinel K-7 — Autonomous Survey Unit

**Ability: Expanded Chassis**

Begin the expedition with **one additional operative in reserve**.

Recommended for players who value deployment flexibility and the ability to occupy more simultaneous long-term features.

### Vexa Nox — Void Corsair

**Ability: Combat Algorithms**

During skirmishes, add **+1 to the highest die**, with a maximum final result of 6.

Recommended when the optional skirmish system is enabled and aggressive network merging is expected.

### Commander stat graphics

Commander cards also display stylised stat values as part of their character presentation. In the current build, the commander's written ability is the mechanically active component; the visual stat values are not a separate combat or movement subsystem.

---

## Sector tile catalogue

The deck is generated from weighted tile templates. This means some sector archetypes are deliberately more common than others.

### Slipstream-focused sectors

#### Transit Spine

A straight connected Slipstream Lane crossing the tile.

#### Gravitic Bend

A curved route connecting two adjacent edges.

#### Relay Junction

A three-way connected Lane centred on a Station.

#### Beacon Nexus

A four-way Lane intersection with a Station and Signal.

#### Frontier Station

A single Lane ending inside the sector at a remote Station, with a Signal bonus.

#### Twin Vector Gate

Two independent Lane segments share one sector without being internally connected.

This tile is strategically important because operatives can potentially occupy the two separate networks independently.

### Nebula-focused sectors

#### Ion Veil

A single-ended Nebula feature containing an Anomaly.

#### Violet Expanse

A connected Nebula corner.

#### Dust Meridian

A straight Nebula band connecting opposite edges.

#### Shattered Cloud

A three-edge Nebula network containing an Anomaly.

### Mixed sectors

#### Rift Crossing

A Slipstream Lane runs across the sector while an independent Nebula network occupies the other two edges. Includes a Signal.

#### Cloud Skimmer

A Lane and Nebula occupy adjacent edges as independent feature types.

### World sectors

#### Civilised World

A World connected to a Slipstream Lane. Includes an Artifact.

#### Rogue World

An isolated World in Void on all four edges. Includes an Artifact.

#### Veiled World

A World bordering a Nebula edge and containing an Anomaly.

### Utility sector

#### Silent Expanse

A fully Void sector. It can be useful for sealing open areas or occupying positions around Worlds without extending a network.

### Starting sector

#### Origin Beacon

Every expedition begins at the Origin Beacon, a Station with a straight Slipstream connection and a Signal.

---

## AI opponent

The built-in ORION AI operates entirely inside the browser.

No network request, cloud model, external API, or server is involved.

### Placement generation

The AI first generates all legal combinations of:

- frontier coordinate,
- tile orientation.

### Move evaluation

Candidate moves are evaluated using factors including:

- number of adjacent existing tiles,
- current difficulty,
- Signals,
- Anomalies,
- Worlds,
- Stations,
- faction markers.

A controlled random component prevents the AI from making exactly the same type of decision in every equivalent state.

### Difficulty behaviour

- **Cadet** uses substantially more random variation.
- **Navigator** uses moderate tactical weighting.
- **Strategist** reduces randomness and favours the engine's higher-scoring move evaluations more consistently.

### Operative deployment

The AI also evaluates available deployment targets after placement. It gives weight to factors such as:

- Worlds,
- feature size,
- whether a feature is already complete,
- Nebula value,
- commander affinity.

The AI may deliberately keep an operative in reserve rather than always deploying.

### Scope of the AI

The current AI is a tactical heuristic opponent, not a deep-search or machine-learning system. It does not perform full-game Monte Carlo simulation or multi-turn minimax search.

---

## Two-player hot-seat mode

Hot-seat mode is designed for two players sharing one physical device.

After a turn ends, control changes to the other player.

With **privacy handoff** enabled, the board is covered by a handoff screen showing:

- the next player's name,
- the turn number,
- a **Reveal turn** button.

The outgoing player can physically pass the device before the next player reveals the board.

This mode requires no account, network connection, second browser, or multiplayer server.

---

## Controls

### Mouse

- **Left-click green marker** — place at the current orientation.
- **Left-click amber marker** — automatically rotate to a legal orientation and place.
- **Hover legal marker** — show a ghost preview.
- **Right-click board** — rotate current tile 90° clockwise.
- **Mouse wheel** — zoom the board.
- **Shift + drag** — pan the board.

### Keyboard

- **Q** — rotate 90° counter-clockwise.
- **E** — rotate 90° clockwise.
- **R** — rotate 90° clockwise.
- **F** — find/cycle a legal placement hint.

Keyboard rotation shortcuts work during the human player's tile-placement phase.

### UI controls

- **0° / 90° / 180° / 270° buttons** — choose an exact tile orientation.
- **Rotate left/right** — manual rotation.
- **Best orientation** — select the orientation with the most currently legal targets.
- **Find a legal spot** — highlight and centre a legal placement.
- **Fit board** — recentre and resize the board view to the current frontier.
- **Menu** — resume, restart the match, or return to setup.
- **Rules** — open the in-game rules summary.

---

## User interface guide

### Top bar

The top bar displays current-turn information, phase information, tile stack status, and utility controls.

### Main board

The centre of the interface contains the expanding frontier.

The board renderer handles:

- placed tiles,
- stars and deep-space backdrop,
- open frontier markers,
- hover previews,
- operative figures,
- suggestion highlights,
- zoom and pan transforms.

### Board guide

A floating guide in the upper area of the board provides immediate contextual help.

It changes depending on the current state, for example:

- green placements available,
- rotation required,
- deployment phase,
- expedition complete.

### Sector inspector

The side panel shows the current sector, including:

- procedural artwork,
- tile name,
- orientation,
- feature tags,
- description,
- legal-placement counts,
- rotation controls,
- placement coach.

### Player cards

Each player card shows:

- commander portrait,
- player name,
- AI indicator where applicable,
- commander role,
- score,
- operatives in reserve,
- operatives currently deployed,
- commander ability.

### Tile stack panel

Displays the number of sectors remaining and a progress indicator.

### Mission log

Records recent game events such as:

- placements,
- auto-rotations,
- operative deployment,
- points earned,
- commander bonuses,
- skirmish results,
- final expedition result.

---

## Seeds and deterministic decks

Nebula Frontier hashes the entered seed string and uses a seeded pseudo-random number generator when constructing the deck.

The deck builder selects from weighted tile templates and shuffles the resulting sectors deterministically.

A sector also receives a visual seed used to vary procedural details without requiring external image files.

Because of this system, a seed can act like a scenario identifier.

Example challenge workflow:

1. Player A chooses `RIFT-DELTA-07` with 72 tiles.
2. Player B uses exactly the same seed and tile count.
3. Both receive the same tile sequence.
4. Their decisions rather than deck randomness can then be compared.

Changing the tile count can change the generated deck even when the text seed is otherwise the same, so share both values when sharing a scenario.

---

## Saving and resuming

The game automatically stores the current expedition in the browser after turns.

The save is stored using the browser's `localStorage` API under the key:

```text
nebula_frontier_save_v1
```

The saved state includes the important match data required to reconstruct the board and continue play.

### Resume

If a saved match exists, the setup screen displays **Resume saved expedition**.

Selecting it restores the board and relevant game state.

### Important save limitations

Browser storage is local to that browser profile and origin.

Therefore:

- a save in one browser may not appear in another,
- private/incognito sessions may discard storage,
- clearing site data can delete the save,
- a local `file://` copy and an online hosted copy may have separate storage,
- the game currently uses a single automatic save slot rather than a named-save library.

---

## Running locally

Nebula Frontier requires no installation.

### Simplest method

1. Download `index.html`.
2. Double-click it.
3. It should open in your default browser.
4. Start a game.

Because all game code and artwork are embedded, an internet connection is not required once you have the file.

### Optional local web server

For development, you can serve the folder over localhost.

Python example:

```bash
python -m http.server 8000
```

Then visit:

```text
http://localhost:8000/
```

A local server is not required for ordinary play, but it can provide behaviour closer to production hosting when testing browser storage and deployment.

---

## Hosting online

Nebula Frontier is a static web application.

You only need to host `index.html`.

Suitable hosting options include:

- GitHub Pages,
- Cloudflare Pages,
- Netlify,
- Vercel static hosting,
- ordinary Apache/Nginx web hosting,
- university/personal web space,
- any static object-storage website host.

No server-side database is needed.

No environment variables are needed.

No API keys are needed.

No build command is needed.

No `node_modules` directory is needed.

---

## GitHub Pages deployment

A minimal GitHub Pages deployment can be done as follows:

1. Create a new GitHub repository.
2. Add the game file as `index.html` at the repository root.
3. Optionally add this README as `README.md`.
4. Commit and push the files.
5. Open the repository **Settings**.
6. Open **Pages**.
7. Under **Build and deployment**, choose deployment from a branch.
8. Select the branch containing `index.html` and the root folder.
9. Save the Pages configuration.
10. Wait for GitHub Pages to publish the site.

The game does not require path rewriting because its resources are embedded in the page itself.

---

## Technical architecture

Nebula Frontier intentionally keeps the deployment model simple while still separating its internal systems conceptually.

### Rendering

The game board and tile artwork are rendered through the **HTML5 Canvas 2D API**.

Procedural rendering functions create:

- starfields,
- gradient space backgrounds,
- Slipstream Lane paths,
- glowing Nebula Regions,
- planets and rings,
- Stations,
- Signal/Anomaly glyphs,
- faction markers,
- Operative figures,
- placement overlays.

### Tile topology

Every tile carries explicit edge types.

Conceptually:

```text
North / East / South / West
        ↓
VOID | LANE | NEBULA
```

The tile also stores internal connection groups so two edges of the same visible type are not automatically assumed to connect internally.

This is important for designs such as **Twin Vector Gate**, where two Lane edges are deliberately separate features.

### Rotation

A 90° clockwise rotation remaps:

```text
West  -> North
North -> East
East  -> South
South -> West
```

Internal Lane and Nebula connection indices are rotated at the same time, keeping visual orientation and feature topology consistent.

### Board representation

Placed sectors are stored using integer grid coordinates.

Conceptually:

```javascript
"x,y" -> placed tile record
```

This allows the board to expand in any direction without allocating a fixed-size matrix.

### Frontier discovery

The legal-placement system examines empty cells adjacent to existing tiles. These form the current placement frontier.

For every frontier cell, the engine tests the current tile at each of its four orientations.

That information produces the green, amber, and red placement classifications.

### Connected-feature tracing

Lane and Nebula control uses graph-style traversal through neighbouring tiles.

The tracer follows:

- local internal feature groups,
- matching edges,
- matching neighbouring edges,
- the connected feature across the board.

The resulting feature structure is used for:

- completion detection,
- operative occupancy,
- majority,
- faction marks,
- Signal/Anomaly bonuses,
- skirmishes,
- scoring.

### Worlds

Worlds use neighbourhood completion rather than edge-network closure.

A World is considered complete when the eight surrounding grid cells are all occupied.

### AI

The AI is a deterministic/rule-based heuristic layer with randomised move evaluation proportional to difficulty.

### Persistence

Game state is serialised to JSON and stored in `localStorage`.

Because JavaScript `Map` and `Set` objects are not directly JSON serialisable, the save layer converts the board and scored-feature collections into array forms and reconstructs them when loading.

### Dependency model

The application uses:

- standard HTML,
- CSS,
- vanilla JavaScript,
- Canvas 2D,
- DOM APIs,
- browser `localStorage`.

It does **not** use:

- React,
- Vue,
- Angular,
- Phaser,
- Three.js,
- jQuery,
- npm packages,
- external fonts,
- third-party image assets,
- server APIs.

---

## Customising the game

Because the entire application is contained in one source file, most gameplay parameters can be found directly in `index.html`.

Back up the working file before making large changes.

### Adding a commander

Commanders are defined in the `CHARACTERS` array.

A commander entry includes fields such as:

```javascript
{
  id: 'astra',
  name: 'Astra Venn',
  role: 'Slipstream Pathfinder',
  accent: '#55e8ff',
  affinity: 'lane',
  ability: 'Route Savant',
  text: 'Whenever you score a completed Slipstream Lane, gain +1 command point.'
}
```

Adding a card visually is straightforward, but a genuinely new mechanical ability may require adding corresponding logic to scoring, deployment, battle, or setup functions.

### Adding a tile template

Sector archetypes are stored in the `TEMPLATES` collection.

A tile template defines properties including:

- `id`
- `name`
- `weight`
- four edge types
- Lane connection groups
- Nebula connection groups
- optional Station
- optional World
- optional Signal
- optional Anomaly
- optional Artifact
- description

The `weight` determines how frequently that archetype is selected when building the deck.

### Changing tile frequency

Increase a template's `weight` to make it more common or reduce the value to make it rarer.

### Changing deck limits

The setup slider currently uses:

```text
minimum: 18
maximum: 120
```

These values can be changed in the tile-count input, although extremely large matches may require UI/performance tuning.

### Changing player colours

Player colours are controlled by the game's colour constants/CSS variables and are also used when rendering Operatives and player-specific UI.

### Adding new feature types

This is a larger architectural change.

A new edge-connected feature would need support in several systems:

1. edge compatibility,
2. tile template data,
3. procedural renderer,
4. rotation mapping,
5. feature tracing,
6. operative deployment,
7. completion detection,
8. scoring,
9. AI evaluation,
10. UI tags and descriptions.

The existing Lane/Nebula implementation provides the pattern to follow.

---

## Browser support

The game is designed for current versions of major modern browsers with Canvas, ES6 JavaScript, and `localStorage` support.

Recommended:

- Google Chrome / Chromium-based browsers,
- Microsoft Edge,
- Mozilla Firefox,
- Safari on current macOS/iOS versions.

Very old browsers are not supported.

For the best experience, use a device with a reasonably large screen, although the interface includes responsive behaviour for smaller displays.

---

## Troubleshooting

### I cannot place the current tile

Check the placement colours.

- **Green:** click immediately.
- **Amber:** click it and the game will rotate automatically.
- **Red:** that location is impossible for the current tile in every orientation.

If no green targets exist but amber targets do, rotation is required.

Use **Find a legal spot** or press **F** if the legal location is hard to find.

### I keep rotating but a red position never becomes legal

That is expected. Red means the cell fails in **all four rotations**.

Choose an amber or green location instead.

### I do not understand the tile's direction

Look at the **N** marker in the tile preview and the angle indicator.

You can also use the four exact-orientation buttons to select a known angle directly.

### I cannot deploy an operative

Possible reasons include:

- you have no operatives left in reserve,
- the connected Lane or Nebula already contains an operative,
- the World is already occupied,
- the current tile does not provide that feature as a deployment option.

You can always choose **Keep reserve** when deployment is optional.

### My save disappeared

Check whether you:

- opened the game in a different browser,
- switched browser profiles,
- cleared site data,
- used private/incognito mode,
- switched between a local file and a hosted URL.

Each of those can result in a different or cleared `localStorage` area.

### The board is off-screen

Use **Fit board**.

You can also zoom with the mouse wheel and pan with **Shift + drag**.

### The AI appears to pause

Short delays are intentionally used so AI turns are readable rather than resolving instantaneously.

### The game does not start when double-clicked

Try a current browser. If local file security behaviour causes an issue, run a tiny local server such as:

```bash
python -m http.server 8000
```

and open `http://localhost:8000/`.

---

## Known limitations

Nebula Frontier 2.0 is a substantial playable prototype, but it is intentionally self-contained and still has room to grow.

Current limitations include:

- Two participants only.
- No internet/network multiplayer.
- No matchmaking or accounts.
- No cloud save synchronisation.
- One automatic browser save slot.
- Square tile geometry only in the current playable implementation.
- AI uses tactical heuristics rather than deep game-tree search.
- No campaign progression between matches.
- No sound or music system.
- No animated 3D board mode.
- No native mobile application package.
- No dedicated accessibility settings panel yet.
- No undo system for committed placements.
- Commander visual stat bars are presentation data rather than a complete secondary stat mechanic.
- Tile artwork is generated procedurally rather than loaded from a large hand-painted asset library.

---

## Ideas for future development

The following are development directions, **not features claimed to exist in the current build**.

### Gameplay

- 3–6 player support.
- Alternative objective cards.
- Private commander missions.
- Research/technology trees.
- Resource economy layered over tile control.
- Rare event sectors.
- Wormholes connecting non-adjacent tiles.
- Mobile neutral entities.
- Fleet pieces in addition to Operatives.
- Commander levelling.
- Asymmetric factions.
- Cooperative scenario mode.
- Solo challenge scenarios.
- Campaign persistence.

### Tile system

- Hexagonal board geometry.
- Triangular tiles.
- Oversized multi-cell landmarks.
- Double-width sectors.
- Special border pieces.
- Elevation layers.
- Fog-of-war tiles.
- Drafting from multiple visible tiles rather than one blind stack.

### AI

- Monte Carlo Tree Search.
- Multi-turn feature valuation.
- Opponent modelling.
- Tile-probability tracking.
- Configurable AI personalities.
- AI explanation panel showing why a move was selected.

### Presentation

- Animated route energy.
- Moving nebula shaders/effects.
- 3D miniature mode.
- Sound effects and adaptive music.
- More detailed commander illustrations.
- Animated scoring transitions.
- End-of-game statistics dashboard.
- Match replay timeline.

### Multiplayer

- WebRTC peer-to-peer mode.
- Hosted room codes.
- Spectator mode.
- Turn timers.
- Reconnect support.
- Shared challenge leaderboards.

### Accessibility

- Colour-blind marker palettes.
- Pattern-based placement markers in addition to colour.
- Larger UI scale controls.
- Full keyboard-only board navigation.
- Screen-reader-oriented placement descriptions.
- Reduced-motion mode.
- High-contrast mode.

---

## Version 2.0 changes

Version 2.0 focuses heavily on clarity, rotation, placement feedback, and interface refinement.

### Rotation improvements

- Added explicit **0° / 90° / 180° / 270°** selection.
- Each orientation reports its number of legal positions.
- Added clearer current-orientation display.
- Added a north reference on the sector preview.
- Added left/right manual rotation controls.
- Added **Q**, **E**, and **R** keyboard rotation shortcuts.
- Added right-click clockwise rotation.
- Added automatic rotation when clicking amber cells.
- Amber markers display the required rotation.

### Placement improvements

- Added green/amber/red frontier classification.
- Added cyan suggested placement state.
- Added **Find a legal spot**.
- Added **Best orientation**.
- Added board-centering behaviour for placement hints.
- Added hover ghost previews.
- Added clear preview text before committing a move.
- Added separate counts for legal-now, rotation-required, and impossible locations.

### UX improvements

- Added contextual placement coach.
- Added floating board instructions.
- Improved side-panel hierarchy.
- Enlarged current-sector preview.
- Improved visual tile tags.
- Improved player information cards.
- Added responsive inspector behaviour.
- Improved error/toast messages.
- Added rotation events to mission logging.

### Existing systems retained

Version 2.0 retains the original major systems:

- AI mode,
- hot-seat mode,
- configurable deck length,
- seeded generation,
- six commanders,
- feature tracing,
- Operatives,
- optional skirmishes,
- scoring,
- automatic saving,
- procedural graphics,
- zoom/pan/fit-board controls.

---

## Project status and licensing

Nebula Frontier is an original custom browser-game prototype intended for experimentation, personal projects, learning, and further development.

The current package does **not** include an explicit open-source licence file. If the project is going to be published as an open-source repository, choose and add an appropriate licence rather than assuming unrestricted reuse automatically.

The game intentionally uses original names, original rules variations, procedural graphics, and original commander characters instead of redistributing artwork from commercial board games.

Third-party game names referenced in development discussion are the property of their respective owners. Nebula Frontier is not presented as an official product of those publishers or rights holders.

---

## File structure

The minimal deployment is:

```text
Nebula-Frontier/
├── index.html
└── README.md
```

`index.html` contains the complete runnable game.

No `/assets`, `/scripts`, `/styles`, or dependency folders are required for the current build.

---

## Development philosophy

Nebula Frontier is built around a few principles:

1. **Placement should be understandable.** The game should explicitly show what works, what requires rotation, and what is impossible.
2. **The browser build should be portable.** One HTML file should be enough to run or host the complete game.
3. **Rules and visuals should be data-driven where practical.** Tiles describe topology while renderers draw the presentation.
4. **Connected features should be real graph structures.** Occupancy and scoring should operate on the whole connected feature rather than only the current tile.
5. **Players should have meaningful asymmetry without excessive complexity.** Commander abilities provide strategic identity while preserving a common base ruleset.
6. **Random generation should be reproducible.** Seeds make procedural sessions replayable and testable.
7. **Local multiplayer should remain simple.** Two people can play on one device without accounts or networking.
8. **Assistance should reduce interface friction, not make strategic decisions for the player.** Auto-rotation and legal-placement hints explain possibilities while leaving the actual strategic choice to the player.

---

## Summary

Nebula Frontier 2.0 is a complete standalone sci-fi tile-placement browser game with procedural sectors, connected-network scoring, commander abilities, operatives, optional skirmishes, deterministic seeds, configurable match length, AI and same-device multiplayer.

The central placement interface is deliberately explicit:

- **Green = place now.**
- **Amber = rotation can make it legal; click to auto-rotate and place.**
- **Red = impossible at that position in every orientation.**
- **Cyan = suggested legal location.**

If you only remember one control when learning the game, press **F** or use **Find a legal spot** whenever you cannot immediately see where the current sector can go.

Enjoy exploring the frontier.
