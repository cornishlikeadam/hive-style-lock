# Hive Stick Challenge (lacrosse)

Single-file HiveKey Arena sport built on the **Hive Style Lock** look. Lives at `/lacrosse` on the Vercel site; nothing outside this folder is touched, so it can ship alongside the other sports (soccer, etc.).

- **File:** [`index.html`](./index.html), three.js r128 from cdnjs, everything else inline, no assets
- **Run:** open the file, or `python3 -m http.server` from the repo root and visit `/lacrosse/`
- **URL params:** `?drill=shoot|pass|duel`, `?surface=turf|grass`, `?tod=day|dusk|night`

## Drills

| Drill | Time | Clock | Rules |
|---|---|---|---|
| Shooting Accuracy | 60 s | 8 s | Six spots round the crease. Shot from the lit ring scores x2, corner pockets score 3. |
| Passing Relay | 45 s | 7 s | Three runners on elliptical routes. Lead the pass; completions return the ball. 3-streak bonus. |
| 1v1 Dodge & Shoot | 40 s | 12 s | AI defender jockeys goal-side with a reaction delay and telegraphed stick checks. Dodge (Shift) during the wind-up to beat him (+1), then beat the keeper. |

## Controls

| Input | Action |
|---|---|
| `WASD` | Run (screen-relative, follows view rotation) |
| Mouse / arrow keys | Aim (shots: point on the goal mouth; passes: point on the field) |
| Click / `Space` | Hold to charge, release to shoot / pass. Mid power is the most accurate; running adds error. |
| `Shift` | Dodge |
| `Q` / `E` | Rotate view 90 degrees |
| `R` / `P` | Restart / pause |

## Look (matches Hive Style Lock)

- Floating voxel island, 2.4 m columns, `DoubleSide` watertight mesh
- Orthographic isometric camera at 850 m, far 1700 (camera zoom handles the follow view)
- Low-res render target with Pixel size slider (default 2), depth outlines, 90-colour OKLab snap + Bayer 4x4 dither
- Doll's-house lifts on the clubhouse (working clock) and the stands (instanced crowd)
- Day / dusk / night, floodlights, LED boards, in-world scoreboard

## Physics notes

- Field is 100.8 x 55.2 m (42 x 23 modules). Ball, sticks and players are drawn oversized for diorama readability.
- Surface variants change bounce and roll: turf (restitution 0.62, roll decel 1.2 m/s^2) vs grass (0.40, 3.4 m/s^2) and repaint the field.
- Stick is box-rigged; the ball is parented to the stick pocket each frame during the cradle, then released at the peak of the swing.
- Pipes are capsule colliders; the net bulges where the ball hits it.
- Bee Stamp preview on the result screen is a local SHA-256 of the result, not an on-chain artifact.
