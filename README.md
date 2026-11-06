# HiveKey Arena // Pixel-Art 3D Sports Suite

> Single-file HTML5 pixel-art 3D diorama sports challenges on floating voxel islands. Built with **three.js r128** from cdnjs, inline WebGL shaders, zero external assets, and procedural Web Audio.

[![Vercel Deployment](https://img.shields.io/badge/Vercel-Live_Arena-black?logo=vercel)](https://hive-style-lock.vercel.app)
[![GitHub Repository](https://img.shields.io/badge/GitHub-cornishlikeadam%2Fhive--style--lock-181717?logo=github)](https://github.com/cornishlikeadam/hive-style-lock)
[![Three.js](https://img.shields.io/badge/three.js-r128-black?logo=three.js)](https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js)

---

## 🏆 Arena Games

| Sport | Title | Route | Description |
|---|---|---|---|
| ⚽ Soccer | **Hive Pitch Challenge** | [`/`](/) &middot; [`/pitch`](/pitch) | Penalty shootout (5 kicks), curling free-kick challenge, and 1v1 finish with realistic goalkeeper AI. |
| 🥍 Lacrosse | **Hive Stick Challenge** | [`/lacrosse`](/lacrosse) | Shooting accuracy around crease, passing relay on routes, and 1v1 dodge & shoot vs defender and keeper. |
| 🏊 Swimming | **Hive Lane Challenge** | [`/swim`](/swim) &middot; [`/lane`](/lane) | 50m sprint, 100m turn race, and stroke timing challenge in an Olympic pool with 7 AI rivals. |

---

## Hive Pitch Challenge (Soccer)

## Game Formats

1. **Penalty Shootout (5 Kicks)**:
   - Ball spotted at regulation penalty spot ($11.0\,\text{m}$ / 12 yards).
   - Aim with arrow keys / WASD or direct canvas click.
   - Charge power bar into the green sweet spot ($62\% - 80\%$) for clinical top bins finishes.
   - AI goalkeeper reacts, reads anticipation, and dives with realistic skill curves.

2. **Free-Kick Challenge (Timed: 60s)**:
   - Dynamic spawn positions from $20\,\text{m}$ to $28\,\text{m}$ out at variable angles.
   - 4-man defensive wall set $9.15\,\text{m}$ away that jumps as the shot is taken.
   - Inside/outside curl keys (`Q` / `E` or mobile button) to bend the ball around or over the wall.

3. **1v1 Finish (Timed: 30s)**:
   - Real-time striker control! Dribble forward using WASD or arrow keys.
   - Goalkeeper rushes off the line to narrow the shooting angle.
   - Execute close-range finishes, feints, and chipped shots.

---

## Visual Baseline & Diorama Architecture

### 1. Floating Voxel Stadium Island
* **Module Unit**: 2.4 m voxel slab ($2.4\,\text{m} \times 2.4\,\text{m}$ footprint) with terraced stone rim and banded soil strata.
* **Underbelly & Environment**: Inverted bedrock stalactites tapering into the sky, waterfall flowing over the south rim into the void with animated pixel mist particles, and hovering satellite rocks.
* **2048 px Painted Ground Canvas**:
  - Dynamically drawn on offscreen canvas.
  - Regulation pitch ($105\,\text{m} \times 68\,\text{m}$ diorama equivalent): touchlines, halfway line, center circle ($9.15\,\text{m}$), penalty boxes, goal areas, penalty spots, and corner arcs.
  - Clubhouse plaza flagstone pavers, running track run-off apron, team technical areas/dugouts, and landscaped garden beds.
* **Surface Variants (Physics & Texture)**:
  - **Grass**: Classic striped turf, balanced grip, medium bounce ($e = 0.58$).
  - **Clay**: Terracotta court with red clay run-off, low skidding bounce ($e = 0.44$), higher spin grip.
  - **Hard**: US Open style two-tone blue court, snappy true bounce ($e = 0.78$), fast roll.
  - **Carpet**: High-speed indoor synthetic turf ($e = 0.65$).

### 2. Doll’s-House Lifts
All three stadium structures can lift independently on hydraulic pistons:
* **Stands Lift**: Sideline spectator stands with tiered crowd voxels rise $9.6\,\text{m}$ on 4 corner hydraulic cylinders.
* **Clubhouse Lift**: Pavilion upper story and hipped roof lift up to reveal the clubhouse interior.
* **Goals Lift**: Goal frame, crossbar, and 3D net rise on dual hydraulic lifters.
* Toggle individually in the side dock or hit `L` to cycle all lifts.

### 3. Stadium Facilities
* **Clubhouse**: Timber siding, veranda pillars, working analog clock with ticking hour and minute hands.
* **Jumbotron Video Screen**: Real-time canvas animation on the clubhouse roof displaying live score, animated equalizer bars, and match graphics.
* **LED Sponsor Boards**: Animated scrolling banners along the touchlines and end runs.
* **Floodlight Masts**: 4 corner lattice towers with active spotlight cones for night fixtures.

### 4. Post-Processing Pipeline
* **Low-Res Render Target**: Downsampled offscreen `THREE.WebGLRenderTarget` with `THREE.NearestFilter` and `DepthTexture`.
* **Pixel Size Slider**: Adjustable from 1 px to 6 px (default 2 px).
* **Depth Outlines**: Real-time 8-neighbor Sobel convolution filter operating on the linear depth buffer to draw stylized ink outlines.
* **90-Colour OKLab Snap + Bayer 4×4 Dither**: Perceptually uniform color quantization using calibrated HiveKey Arena sports colors.

---

## Physics & Goalkeeper AI

* **Sub-Stepped Physics Loop**: 8 sub-steps per frame (zero tunneling through posts, crossbar, net, or ground).
* **Ball Flight**: Gravity, aerodynamic drag ($F_d \propto v^2$), and Magnus effect ($F_m \propto \boldsymbol{\omega} \times \mathbf{v}$) for realistic bending free kicks.
* **Goal Posts**: Rigid cylinder capsule collision tests with metallic ringing audio and elastic deflection.
* **Net**: Inelastic damping absorbs the ball so it settles naturally in the back of the net.
* **Goalkeeper AI Tiers**:
  * **Rookie**: $0.35\,\text{s}$ reaction delay, modest dive speed ($4.2\,\text{m/s}$), higher anticipation error.
  * **Pro**: $0.24\,\text{s}$ reaction, $5.4\,\text{m/s}$ dive, clean catching under $13\,\text{m/s}$.
  * **Elite**: $0.16\,\text{s}$ reaction, $6.4\,\text{m/s}$ explosive dive, sharp angle closing.

---

## Synthesizer Audio (Web Audio API)

Zero external audio files—everything generated procedurally via Web Audio nodes:
* **Referee Whistle**: Double sine wave chirps with frequency modulation.
* **Ball Kick**: Low-pass 808-style punch sweep ($160\,\text{Hz} \to 45\,\text{Hz}$).
* **Post Clang**: Multi-frequency metallic resonant bell chord ($840\,\text{Hz}, 1310\,\text{Hz}, 2140\,\text{Hz}$).
* **Net Swish**: Bandpass-filtered white noise burst.
* **Crowd Cheer & Gasp**: Filtered pink noise with rise and fall envelopes.

---

## Controls

| Action | Desktop Keys | Mobile Touch |
| :--- | :--- | :--- |
| **Aim** (Penalties / FK) | Arrow Keys / `W` `A` `S` `D` / Click Goal | D-Pad (▲ ◀ ▶ ▼) / Tap Goal |
| **Move / Dribble** (1v1) | Arrow Keys / `W` `A` `S` `D` | D-Pad (▲ ◀ ▶ ▼) |
| **Shoot / Power** | Hold `Space`, release in sweet spot | Hold `SHOOT`, release in sweet spot |
| **Curl (Bend)** | `Q` (Inside bend) / `E` (Outside bend) | `CURL` Button |
| **Camera View** | `C` (TV Follow / Island 850m / Close-up) | `CAM` Button |
| **Pause** | `P` | Menu Panel |
| **New Challenge** | `N` | Menu Panel Button |
| **Format** | `1` (Penalties) / `2` (Free Kicks) / `3` (1v1) | Menu Panel |
| **Doll's-House Lift**| `L` (Toggle all) | Menu Panel Checkboxes |
| **Sound Toggle** | `M` | Menu Panel Button |

---

## Live Deployment & GitHub Repo

* **Live Demo**: [https://hive-style-lock.vercel.app](https://hive-style-lock.vercel.app)
* **GitHub**: [https://github.com/cornishlikeadam/hive-style-lock](https://github.com/cornishlikeadam/hive-style-lock)

---

## Local Development

```bash
# Clone the repository
git clone https://github.com/cornishlikeadam/hive-style-lock.git
cd hive-style-lock

# Run any static web server
npx serve .
# or
python3 -m http.server 8080
```
Open `http://localhost:8080` in any web browser.
