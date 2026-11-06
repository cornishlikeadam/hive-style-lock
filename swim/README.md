# Hive Lane Challenge // HiveKey Arena Swimming

A single-file HTML5 pixel-art 3D diorama Olympic swimming game set in an open-air aquatic stadium on a floating island. Built with **three.js r128** from cdnjs, inline WebGL shaders, zero external assets, and procedural Web Audio.

[![Vercel Deployment](https://img.shields.io/badge/Vercel-Live_Game-black?logo=vercel)](https://hive-style-lock.vercel.app/swim)
[![GitHub Repository](https://img.shields.io/badge/GitHub-cornishlikeadam%2Fhive--style--lock-181717?logo=github)](https://github.com/cornishlikeadam/hive-style-lock)
[![Three.js](https://img.shields.io/badge/three.js-r128-black?logo=three.js)](https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js)

---

## Game Formats

1. **50 m Sprint**:
   - Single-length flat-out sprint from starting blocks to touch pad.
   - Dive reaction window on the starter horn (`BEEP!`). False start penalties for jumping early ($< 0.10\,\text{s}$), rocket boost for reactions under $0.22\,\text{s}$.
   - Underwater dolphin glide breakout at $11\,\text{m}$.
   - Rhythmic stroke sweet-spot timing to maximize propulsion against water drag.

2. **100 m Race**:
   - 2 lengths ($50\,\text{m}$ out, flip turn at far wall, $50\,\text{m}$ back).
   - Tumble flip-turn mechanic: approach the wall at $50\,\text{m}$, hit `Space` or `Shift` inside the turn window ($2.8\,\text{m} - 0.8\,\text{m}$ to wall) to execute a somersault turn and push off with streamline speed.
   - Pacing & stamina management (Hydro Surge).

3. **Stroke Challenge**:
   - Rhythm precision trial testing stroke cadence and timing windows.
   - Hit consecutive `PERFECT` stroke windows to build up speed streaks.

---

## Stroke Techniques

- **Freestyle (Front Crawl)**: Alternating windmill arm stroke, bilateral body roll, breathing head rotation, and 6-beat flutter kick.
- **Butterfly**: Symmetrical double arm recovery skimming over the surface and undulating dolphin kick.
- **Breaststroke**: Symmetrical in-sweep arm pull, glide phase with body submerged, and whip kick.
- **Backstroke**: Inverted back swimming with alternating backward windmill arms and continuous surface flutter kick.

---

## Visual Baseline & Architecture

- **Floating Voxel Island**: $2.4\,\text{m}$ bedrock voxel columns with terraced rim, inverted underbelly stalactites, satellite rocks, and animated waterfall dropping into pixel mist particles.
- **50 m Olympic Pool**:
  - $50\,\text{m} \times 21\,\text{m}$ basin, $2.0\,\text{m}$ depth.
  - 8 regulation lanes ($2.5\,\text{m}$ width), player seeded in **Lane 4**.
  - Floating lane ropes with red 5m markers, white/blue alternating cylindrical floats.
  - 8 numbered starting blocks with angled track-start top platform and backstroke handles.
  - Overhead backstroke turn flags suspended 5m from each wall.
  - Underwater lane lines with dark blue cross ("T") marks and end wall target crosses.
  - Yellow electronic touch pads at both ends.
  - Animated procedural water waves and caustics surface simulation.
- **Doll's-House Lifts**:
  - Independent vertical lifts on hydraulic pistons for:
    - Spectator stands with tiered crowd voxels
    - Clubhouse pavilion with working analog clock (hours and minutes)
    - Starting blocks
- **Jumbotron Timing Display**:
  - Dynamic 2D canvas rendered to in-world LED screen showing running race clock, split times, lane positions, and live equalizer audio bars.
- **Lighting & Time of Day**:
  - **Day**: Crisp overhead sunlight, clear turquoise water, bright diorama shadows.
  - **Dusk**: Golden hour purple/orange skies, perimeter floodlights switch on.
  - **Night**: Dark starry sky, 4 tall floodlight towers casting beams, glowing underwater pool wall lanterns.

---

## Controls

| Input | Action |
|---|---|
| `Space` | Dive on start / rhythm stroke (time to sweet spot) |
| `Shift` | Dive reaction / Hydro Surge sprint / Wall turn |
| `C` | Cycle broadcast camera (`TV Follow`, `Overhead`, `Turn Wall`, `Island 850m`) |
| `P` | Pause / Resume |
| `N` | New race / reset |
| `1` / `2` / `3` | Race distance (50m, 100m, Stroke Challenge) |
| `Tab` / `Esc` | Toggle / close retractable dashboard |
| Click pool | Close dashboard and focus gameplay |
| Touch buttons | Mobile touch controls (`STROKE`, `SURGE`, `CAM`) |

---

## Multi-Sport Arena Integration

HiveKey Arena features three sports on the shared floating diorama baseline:
- ⚽ **[Hive Pitch Challenge](/pitch)**: Soccer penalties, free kicks, and 1v1 finish.
- 🥍 **[Hive Stick Challenge](/lacrosse)**: Lacrosse shooting, passing relay, and 1v1 dodge.
- 🏊 **[Hive Lane Challenge](/swim)**: 50m/100m Olympic swimming races and stroke challenges.
