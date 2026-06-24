# IronTide ⚔️

<img width="1856" height="931" alt="Screenshot" src="https://github.com/user-attachments/assets/bbc4e915-ad28-4ec8-8919-cd0f8bae2554" />

---

IronTide is a browser-based real-time war strategy game played on an interactive satellite world map. Pick any two neighbouring countries from the full world atlas, deploy your forces, and fight for total territorial control — all in a single HTML file.

The project was built as a personal experiment to learn real-time simulation architecture, geographic rendering, AI opponent design, and complex game-state management inside a zero-dependency single-file web app.

## 🌐 Live Website

IronTide runs online using Vercel.

**Live site:** https://iron-tide-beryl.vercel.app/

---

## ⚔️ About the Project

IronTide renders a real satellite imagery map (powered by ArcGIS) overlaid with a dense invisible grid that divides both chosen countries into thousands of individual territory cells. Those cells change colour in real time as your army pushes forward and the enemy pushes back.

The simulation runs on a virtual clock — battles resolve every 240ms, troops regenerate over time, the AI launches autonomous offensives, and the map redraws continuously to reflect the shifting front line.

Troop sizes are seeded from real-world population figures, so picking a superpower actually matters.

---

## 🚀 Features

### World Map & Territory System

* **Full World Atlas:** Every country in the world is selectable, loaded from live TopoJSON + world-countries data.
* **Land Border Enforcement:** The enemy selector only shows countries that share a real land border with your nation — no island-hopping.
* **Cell Grid Engine:** Both countries are carved into ~7,000 invisible square cells. Each cell tracks its owner, its neighbours, and whether it sits on the active front line.
* **Live Front Line Rendering:** Border cells are outlined in a warm yellow highlight — interior territory has no borders, so the coloured mass looks smooth and organic.
* **Satellite Map Base:** ArcGIS World Imagery tiles provide a realistic satellite background at all zoom levels.

### Combat & Order System

* **Order-Driven Combat:** Nothing happens automatically on your side — you issue explicit orders.
  * **Click enemy territory → Attack Order:** Commits a chosen percentage of your troops as a focused offensive push toward that point on the map. The front line pressure concentrates around your target.
  * **Click your own territory → Move Order:** Redeploys troops toward that point — use it to retreat, regroup, or shift reserves before launching an attack. Pulling troops off the border weakens it for real.
* **Troop Commit Slider:** A 1–99% slider lets you choose exactly how much of your force to commit before confirming any order.
* **Stand Down Command:** Cancel an active order at any time to halt the advance or redeployment.

### Enemy AI

* **Autonomous AI Offensives:** The enemy periodically decides to launch attacks on its own, independent of anything the player does.
* **Auto-Defend on AI Attack:** While the enemy is pressing, your troops near the front automatically defend and reclaim lost ground — but will never automatically invade. Only your orders can push into enemy territory.
* **AI Grace Period:** A brief grace period at game start before the AI is allowed to roll for its first attack, giving you time to orient.
* **Retreat System:** Both the player and the AI can fall back to consolidate their front line.

### Troop & Simulation System

* **Population-Scaled Armies:** Max troop counts are derived from real 2023 population data (25% of population, capped at 80 million). Small countries genuinely have smaller armies.
* **Proportional Casualty Scaling:** Losses are calculated as a fraction of each side's maximum army, so a small nation and a superpower bleed at the same *relative* rate — preventing small armies from dying in minutes.
* **Continuous Troop Regeneration:** Both sides slowly rebuild troops over time, scaled by how much of their original territory they still hold.
* **Real-Time Virtual Clock:** The simulation runs on an internal clock that drives combat ticks, regen ticks, AI rolls, and the in-game date display simultaneously.
* **Speed Controls:** Step through the war at 1×, 2× or 3× real-time speed — everything in the simulation genuinely runs faster, not just the date counter.

### HUD & Interface

* **Live Troop Counter:** Smooth interpolated display of your current force strength with a proportional capacity bar.
* **Casualties Panel:** Real-time smoothed counters for both your losses and the enemy's.
* **In-Game Date:** Simulated calendar starting from 2020/01/01, advancing one game-day per second at 1× speed.
* **Active Order Readout:** The HUD shows your current standing order and warns you when the enemy is on the offensive.
* **Flag Icons on Territory:** Your flag and the enemy flag are scattered across controlled territory, with density and size that scale dynamically with your troop count and zoom level.
* **Animated Focus Rings:** A pulsing ring marks your attack target (red) or muster point (blue), and a separate orange ring marks the AI's active offensive target.

### Atmosphere

* **Background Audio:** A looping ambient war soundtrack plays during the battle, with a 5-second gap between loops. Mutable via the HUD.
* **Corner Video Widget:** A small 16:9 video panel in the bottom-left cycles through three clips with automatic fade transitions and a 10-second gap between each.
* **Victory / Defeat Screen:** When one side's territory is fully overrun, an end screen appears with final casualty counts, the reason for the outcome, and the total number of war days elapsed.
* **Surrender Option:** End the war on your terms at any time.

---

## 🛠 Tools & Technologies Used

* **HTML5:** Single-file structure, all logic and UI in one document
* **CSS3:** Custom monospace military aesthetic, dark theme, animated HUD panels
* **JavaScript:** ES6+, real-time simulation loops, ray-casting point-in-polygon, geographic math
* **Leaflet.js:** Interactive map rendering, marker management, polygon layers
* **TopoJSON / world-atlas:** High-resolution country geometry (110m scale)
* **world-countries:** Country metadata — names, ISO codes, borders, population, coordinates
* **flagcdn.com:** Live country flag images via ISO 2-letter codes
* **ArcGIS World Imagery:** Satellite map tile layer
* **Vercel:** Deployment
* **AI Assistance:** Planning, debugging, and optimization

---

## ▶️ How to Run Locally

IronTide runs entirely inside a single file and can be opened using any local server environment.

Recommended method:

1. Open the project folder in VS Code.
2. Install the **Live Server** extension.
3. Right-click `index.html`.
4. Select **Open with Live Server**.

The site should open in your browser at:

```text
http://127.0.0.1:5500/index.html
```

> ⚠️ Opening `index.html` directly as a `file://` URL may cause fetch errors when loading the world atlas. Always use a local server.

---

## 🗂 Project Structure

```text
irontide/
│
├── index.html          # Main single-file app — all logic, UI, and rendering
├── README.md           # Repository documentation
├── Media/
│   ├── audio.MP3       # Background war soundtrack
│   ├── Video 1.mp4     # Corner video clip 1
│   ├── Video 2.mp4     # Corner video clip 2
│   └── Video 3.mp4     # Corner video clip 3
└── Screenshots/        # UI and gameplay screenshots
```

---

## 🎮 How to Play

1. **Pick your nation** from the full world country list.
2. **Pick an enemy** — only countries that share a real land border with you will appear.
3. **Click Deploy Forces** to start the war.
4. **Click enemy territory** to issue an attack order. Use the slider to commit 1–99% of your troops and confirm.
5. **Click your own territory** to muster and reposition your forces.
6. **Watch the front line.** The yellow border shows where fighting is happening.
7. **Overrun the enemy** before they overrun you. First side to lose all cells loses the war.

---

## 📌 Status

This is an actively maintained experimental project.

Updates are focused on expanding the AI behaviour, adding multi-front conflict support, improving troop mechanics, and refining the visual rendering of large-scale territorial shifts.

---

## ⚠️ Note

IronTide is a standalone, independent web application built for educational and portfolio purposes.

All country geometry, population data, and border information is sourced from publicly available open datasets. The game does not reflect or endorse any real-world geopolitical positions.

---

## 🧠 What I Learned

While building IronTide, I gained hands-on experience with:

* **Geographic Data Pipelines:** Loading, parsing, and rendering TopoJSON world geometry at runtime.
* **Cell-Grid Simulation:** Building a dense invisible ownership grid with neighbour adjacency, gap-filling, and dynamic front line detection.
* **Real-Time Game Loops:** Running combat, regeneration, AI decision-making, and display interpolation on a unified virtual clock with speed scaling.
* **Point-in-Polygon Math:** Implementing ray-casting hit tests for arbitrary polygon and MultiPolygon GeoJSON features.
* **AI Architecture:** Designing an autonomous enemy that issues timed offensives, manages retreat, and responds to the player's troop distribution.
* **Proportional Simulation Balancing:** Tuning combat math so every country matchup is playable regardless of the population size difference.
* **Single-File App Architecture:** Managing map state, simulation state, audio, video, UI modals, and rendering layers inside a monolithic vanilla JS structure.
