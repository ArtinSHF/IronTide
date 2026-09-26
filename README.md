# IronTide ⚔️

<img width="1856" height="931" alt="Screenshot" src="https://github.com/user-attachments/assets/bbc4e915-ad28-4ec8-8919-cd0f8bae2554" />

---

IronTide is a browser-based real-time war strategy game played on an interactive satellite world map. Build your own alliances, choose one or more enemies from the full world atlas, deploy your forces, and fight for total territorial control — all in a single HTML file.

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
* **Player-Controlled Diplomacy:** Pick zero, one, or several allies — then choose one or more enemy countries. Alliances do not need to make geopolitical sense. That's between you and history. 😂
* **Coalition Territory:** Allied and enemy countries merge their territory, manpower and fronts into real fighting coalitions instead of acting as a cosmetic troop bonus.
* **18 Historical Empire Starts:** Play as the Roman, Byzantine, Ottoman, British, Spanish, Portuguese, Persian, Russian, Soviet, Austro-Hungarian, French Colonial, German, Qing, Mughal, Japanese, Macedonian, Umayyad, or Abbasid Empire.
* **Empires Are One Country:** No exceptions. However many modern nations sit inside its historical borders, an empire fields one flag, one force total, one loss total, and one seat at the diplomacy table — never a pile of separate modern countries wearing an empire's name. Add a real ally on top (say, Roman Empire + Germany) and *that* still shows up as its own country, exactly like it should.
* **High-Detail Cell Grid Engine:** Every selected coalition territory is carved into invisible square cells. Each cell tracks its owner, home nation, current formation, neighbours, and whether it sits on an active front line.
* **Anti-Meridian-Safe Geography:** Date-line-spanning geometry is converted into continuous simulation rings and split safely for rendering. Russia and other seam-crossing countries do not create phantom territory, fronts, or world-spanning lines.
* **Live Front Line Rendering:** Border cells are outlined in a warm yellow highlight — interior territory has no borders, so the coloured mass looks smooth and organic.
* **Satellite Map Base:** ArcGIS World Imagery tiles provide a realistic satellite background at all zoom levels.

### Combat & Order System

* **Order-Driven Combat:** Nothing happens automatically on your side — you issue explicit orders.
  * **Click enemy territory → Attack Order:** Commits a chosen percentage of your troops as a focused offensive push toward that point on the map. Deep objectives follow the nearest viable approach sector instead of stalling at the first border cell.
  * **Click your own territory → Move Order:** Redeploys troops toward that point — use it to retreat, regroup, or shift reserves before launching an attack. Pulling troops off the border weakens it for real.
* **Troop Commit Slider:** A 1–99% slider lets you choose exactly how much of your force to commit before confirming any order.
* **Stand Down Command:** Cancel an active order at any time to halt the advance or redeployment.

### Enemy AI

* **Strategic AI Offensives:** The enemy weighs readiness, territory held, force density across the front, your active offensive and exposed sectors before committing to an attack.
* **Auto-Defend on AI Attack:** While the enemy is pressing, your troops near the front automatically defend and reclaim lost ground — but will never automatically invade. Only your orders can push into enemy territory.
* **AI Grace Period:** A brief grace period at game start before the AI is allowed to roll for its first attack, giving you time to orient.
* **Retreat System:** Both the player and the AI can fall back to consolidate their front line.

### 🤖 AFK Mode

* **Automode:** Press AFK Mode and a second AI — running the exact same strategic playbook as the enemy — takes over your side. It reads readiness, territory held, and front pressure just like the enemy AI does, then attacks, defends, and retreats through the same order system a human player uses. Press it, sit back, and watch two AIs fight the whole war like one of those country-vs-country simulation videos. 🍿
* **Non-Destructive:** AFK Mode plugs into the normal attack/retreat orders instead of a separate combat path, so nothing about how battles resolve changes — it just decides *when* and *where* to click for you.

### Troop & Simulation System

* **Population-Scaled Armies:** Max troop counts are derived from real 2023 population data (3.5% of population, capped at 35 million). Small countries genuinely have smaller armies; superpowers still feel like superpowers.
* **Meaningful Casualties:** Losses are proportional to force scale, and combat effectiveness falls as formations are depleted. Major offensives are deliberately costly, so a battered remnant has less cohesion and cannot fight like a fresh army.
* **Slow, Territory-Scaled Replacements:** Both sides rebuild slowly based on how much original territory they still hold. Reinforcements cannot instantly erase a disastrous battle.
* **Real-Time Virtual Clock:** The simulation runs on an internal clock that drives combat ticks, regen ticks, AI rolls, and the in-game date display simultaneously.
* **Speed Controls:** Step through the war at 1×, 2× or 3× real-time speed — everything in the simulation genuinely runs faster, not just the date counter.

### HUD & Interface

* **Live Troop Counter:** Smooth interpolated display of your current force strength with a proportional capacity bar.
* **Coalition Roster:** The compact HUD shows each main nation, ally, and enemy member with its own current force and casualties.
* **Casualties Panel:** Real-time smoothed counters for both coalition losses.
* **In-Game Date:** Simulated calendar starting from 2020/01/01, advancing one game-day per second at 1× speed.
* **Active Order Readout:** The HUD shows your current standing order and warns you when the enemy is on the offensive.
* **National Flags on Territory:** Each coalition member retains its own flags on the map. Flags follow the formation currently holding territory, with density and size that scale dynamically with strength and zoom level.
* **Front-Aware Force Labels:** Large map troop numbers sit inside friendly ground, face the relevant border, and split into separate major theatres when a war has multiple fronts.
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

1. **Pick your nation** from the full world country list — or choose a historical empire.
2. **Pick allies** if you want them. Leave the list empty to fight alone.
3. **Pick one or more enemy nations.** They can be neighbours, distant rivals, or an objectively terrible idea.
4. **Click Deploy Forces** to start the war.
5. **Click enemy territory** to issue an attack order. Use the slider to commit 1–99% of your troops and confirm.
6. **Click your own territory** to muster and reposition your forces.
7. **Watch the front line.** The yellow border shows where fighting is happening.
8. **Overrun the enemy coalition** before it overruns yours. First side to lose all cells loses the war.
9. **Or just hit AFK Mode** and let the AI run your side while you watch the whole thing play out. 🍿

---

## 📌 Status

This is an actively maintained experimental project.

Updates are focused on expanding the AI behaviour, refining multi-front coalition conflict, improving troop mechanics, and polishing large-scale territorial rendering. Latest pass: a much larger empire roster, a proper empire-as-one-country fix across flags/forces/losses/diplomacy, and AFK Mode.

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
