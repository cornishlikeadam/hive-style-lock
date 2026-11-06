# Hive Stick Challenge (lacrosse)

Single-file HiveKey Arena sport built on the **Hive Style Lock** look. Lives at `/lacrosse` on the Vercel site; nothing outside this folder is touched, so it can ship alongside the other sports (soccer, etc.).

- **File:** [`index.html`](./index.html), three.js r128 from cdnjs, everything else inline, no assets
- **Run:** open the file, or `python3 -m http.server` from the repo root and visit `/lacrosse/`
- **URL params:** `?drill=match|shoot|pass|duel`, `?mode=drills` (open the drills menu), `?surface=turf|grass`, `?tod=day|dusk|night`, `?post=1` (Style Lock post-process on)
- **Rendering:** direct render by default (stable). The Style Lock pixel post-process is one checkbox in the dock (or `?post=1`).

## Match mode (default): 6v6 field lacrosse

The page opens straight into a match with all 12 players on the field. Pick **Match** or **Drills** from the dock (Mode section) or the Menu.

- **Teams:** Hive (amber: you + 4 AI field players + keeper) vs Rivals (crimson: 5 AI + keeper). You control one attacker.
- **Format:** first to 3 goals or 90 s. A tie at the buzzer goes to sudden death. After every goal, a face-off at centre with a 3-2-1 countdown.
- **Ball:** carried in the stick pocket (cradle), passed, shot, bounced, picked up off the ground (scoop), intercepted in the air.
- **AI:** carriers shoot inside ~17 m when the lane is clear, pass to the most open teammate, or dodge; defenders mark goal-side, the nearest one presses and telegraphs a stick check (0.3 s wind-up), keepers read shots with a reaction delay and a probabilistic save.
- **You:** `Click/Space` shoots (hold to charge). With no ball, `Click/Space` is a check. `F` or right-click passes to the teammate nearest the cursor. `Shift` dodges (beats a check).
- **Camera:** Broadcast (default, follows the ball carrier, leans toward the attack), Iso Lock (Style Lock angle) or Overview.
- **HUD:** on-canvas scoreboard (score + clock) and an in-world LED scoreboard behind the goal.

## Drills (secondary)

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

## SCAD Bee Olympics theme

SCAD yellow (`#FFD100`) and black across the island, stands, clubhouse and UI, and the 90-colour palette now leans yellow/black. Hive is yellow with black details, the Drones are black with yellow accents, keepers are yellow with black details, and the ball is black and yellow.

- **Intro:** a 5 s full-screen intro (pixel bees with faint trails, "HIVEKEY ARENA" then "SCAD BEE OLYMPICS" with a scan-line / chromatic shimmer) plays on the first load only. Click or press any key to skip. The game loads underneath and the match starts as it fades. `?intro=1` replays it, `?intro=0` skips it; reduced-motion users skip it.
- **Branding:** a holographic bee + "Bee Olympics" logo in the corner, and the LED boards rotate "HiveKey Arena - Bee Olympics" messages.
- **Environment:** honeycomb panels on the stands and clubhouse, yellow/black flags, tiny voxel bees and light motes in the air, warm-gold floodlights at night.
