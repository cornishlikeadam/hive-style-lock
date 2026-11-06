# Hive Style Lock // Reference Scene

> Visual baseline reference scene for all **HiveKey Arena Sports** game titles and environments. Built with **three.js r128** from cdnjs in a minimal single-file HTML5 architecture.

[![Vercel Deployment](https://img.shields.io/badge/Vercel-Live_Demo-black?logo=vercel)](https://hive-style-lock.vercel.app)
[![Three.js](https://img.shields.io/badge/three.js-r128-black?logo=three.js)](https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js)
[![Color Space](https://img.shields.io/badge/OKLab-90--Color_Palette-2ea043)](#90-colour-oklab-quantization)
[![Projection](https://img.shields.io/badge/Camera-Orthographic_Isometric_(~850m)-39b2de)](#camera-specification)

---

## Architecture & Visual Baseline Specification

### 1. Floating Voxel Island
* **Module Unit**: 2.4 m columns ($2.4\,\text{m} \times 2.4\,\text{m}$ footprint).
* **Watertight Manifold Geometry**: Every column top, bottom cap, and inter-column vertical cliff step is procedurally synthesized into a single continuous solid mesh with `THREE.DoubleSide` material, ensuring zero see-through holes, gaps, or light leaks.
* **Surface Strata**:
  * Central sports turf ($2.4\,\text{m}$ checkerboard mowing pattern) with regulation arena chalk markings.
  * Clubhouse terrace apron in weathered flagstone pavers.
  * Red court clay spectator terrace and hazard-striped test stand plinth.
  * Exposed basalt and amber strata cliffs tapering into an inverted floating stalactite bedrock underside.

### 2. Orthographic Isometric Camera
* **Distance**: $\approx 850\,\text{m}$ ($\|\mathbf{p}\| = 850.0\,\text{m}$ to scene origin).
* **Far Plane**: $1700\,\text{m}$ ($[1, 1700]\,\text{m}$ frustum depth).
* **True Isometric Angles**: Azimuth $45^\circ$, Elevation $\theta = \arctan(1 / \sqrt{2}) \approx 35.264^\circ$.
* **Controls**: Smooth OrbitControls with one-click **Isometric Lock** reset button.

### 3. Low-Resolution Render Target & Pixelation
* **Offscreen Buffer**: `THREE.WebGLRenderTarget` rendered with `THREE.NearestFilter` and hardware `THREE.DepthTexture`.
* **Pixel Size Slider**: Default **2 px** (adjustable from 1 px to 8 px in real time), scaling the internal render target resolution while outputting crisp, unfiltered texels to the viewport.

### 4. Depth Outlines
* **Edge Detection**: Real-time 8-neighbor Sobel convolution filter operating directly on linear orthographic depth buffer samples.
* **Styling**: Configurable ink threshold and blend strength, generating crisp silhouette boundaries between voxel tiers, structures, and background void.

### 5. 90-Colour OKLab Snap + Bayer Dithering
* **Perceptually Uniform Color Quantization**:
  * Colors are converted $\text{sRGB} \to \text{Linear RGB} \to \text{OKLab} (L, a, b)$.
  * 4×4 unrolled Bayer matrix dither is evaluated in low-res fragment space and added to the perceptual $(L, a, b)$ coordinates.
  * The fragment snaps to the nearest color in the calibrated **90-color HiveKey Arena Sports palette** by minimizing Euclidean perceptual distance $\Delta E_{\text{OKLab}}$.
  * Result is converted back $\text{OKLab} \to \text{Linear RGB} \to \text{sRGB}$ with zero color banding.

### 6. Doll's-House Lift on Test Stand
* Mechanical architectural cutaway on an elevated $8.4\,\text{m} \times 8.4\,\text{m}$ test stand plinth.
* 4 corner hydraulic cylinders with sliding chrome piston rods.
* The upper observation canopy and roof deck lift up to $12\,\text{m}$ into the air via interactive slider or auto-hover oscillation, revealing a fully furnished interior (tactical strategy whiteboard, team benches, holographic trophy pedestal).

### 7. Clubhouse Box with Working Clock
* Modular voxel pavilion ($12.0\,\text{m} \times 8.4\,\text{m} \times 5.2\,\text{m}$) with timber siding, white structural columns, veranda porch overhang, and mullioned windows.
* Front gable clock pediment with circular dial, gold bezel, 12 hour tick marks, and animated hour/minute hands that tick in real time.
* Warm incandescent interior point lighting and window emissive glow that illuminate during dusk and night cycles.

### 8. Dynamic Day / Dusk / Night Lighting
* **Day**: High-intensity warm sunlight ($1.4$), soft sky blue ambient, crisp azure background void.
* **Dusk**: Fiery low-angle amber sun ($0.95$), rich violet ambient, incandescent clubhouse lantern glow, warming stadium floodlights.
* **Night**: Cool moonlight ($0.32$), deep midnight slate sky, bright high-mast corner floodlight beams casting dramatic stadium lighting across the turf.

---

## Interactive Controls (HUD)

| Control | Range / Options | Description |
| :--- | :--- | :--- |
| **Pixel Size** | `1` to `8 px` (Default: `2`) | Dynamic downsampling factor for the render target |
| **Depth Outlines** | `ON / OFF`, Threshold `0.1 - 1.5`, Strength `0.1 - 1.0` | 8-neighbor Sobel edge detector on depth |
| **90-Color OKLab Snap** | `ON / OFF` | Snaps fragments to nearest HiveKey 90-color palette entry |
| **Bayer 4×4 Dither** | `ON / OFF`, Weight `0.0 - 2.0` | Micro-pattern dither in OKLab perceptual space |
| **Doll's-House Lift** | `0` to `12 m`, `Closed`, `Fully Lifted`, `Hover Auto` | Hydraulic extension of test stand observation roof |
| **Lighting Time** | `Day`, `Dusk`, `Night`, or `0:00 - 24:00` slider | Solar angle, sky color, floodlights, and window glow |
| **Isometric Lock** | Click button | Snaps camera back to $\approx 850\,\text{m}$ isometric framing |
| **Palette Inspector** | Click button | Opens interactive swatch viewer for all 90 calibrated colors |

---

## Local Development

```bash
# Clone the repository
git clone https://github.com/cornishlikeadam/hive-style-lock.git
cd hive-style-lock

# Serve locally using any static file server
npx serve .
# or
python3 -m http.server 8080
```

Open `http://localhost:8080` in any modern web browser.

---

## License
MIT. Baseline reference for the HiveKey Arena sports ecosystem.
