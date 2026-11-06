# Hive Pitch Challenge (soccer)

`index.html` is a single-file three.js r128 build on the Hive Style Lock look (direct render; the post-process is bypassed while the scene is stabilised).

## Modes

Pick **Match** or **Drills** with the toggle in the top-left (also in the dashboard). Match is the default and starts immediately.

### Match: 5v5 small-sided

- **Teams:** Blue (you + 3 AI outfield + keeper) vs Red (4 AI outfield + keeper). You control the Blue forward. Players are the same voxel humanoids as the drills (head, torso, arms, legs).
- **Format:** first to 2 goals or 90 s. A tie at full time goes to a golden goal. After every goal the conceding team kicks off (3-2-1 countdown) and play continues until the match ends.
- **Ball:** dribbled at the feet, passed along the ground, shot with the existing power meter (sweet spot 62-80%) and curl (Q / E), controlled on contact, and recovered from the touchline / end line.
- **Tackles:** contact steals the ball. A sprint (Shift) while dribbling dodges a tackle; Shift without the ball is a slide tackle.
- **AI:** carriers shoot inside ~26 m with a clear lane, pass to the most open teammate or sprint past a defender; defenders press goal-side and mark; keepers read shots with the dashboard skill level (Rookie / Pro / Elite) and dive or hold.
- **Scoreboard:** HUD at the top, plus the in-stadium jumbotron shows score and clock.
- **Camera:** Broadcast (default) follows the ball carrier; C cycles to the Hive Style Lock island view.

| Input | Action |
|---|---|
| `WASD` / arrows | Run (screen-relative) |
| Mouse | Aim at the goal |
| `Space` / click | Hold to charge, release to shoot |
| `F` / right-click | Pass to the teammate nearest the cursor |
| `Shift` | Sprint (dodges a tackle) / slide tackle |
| `Q` `E` | Curl |
| `C` `P` `N` | Camera / pause / restart match |
| `1 2 3` | Jump to a drill (Penalties / Free Kicks / 1v1 Finish) |

### Drills

The original Penalties, Free Kicks and 1v1 Finish challenges are unchanged.

`?mode=drills` opens straight into the drills.
