# Flip Master — Neon Gym

A self-contained, single-file backflip ragdoll game. Charge a jump, launch off the spring pedestal, tuck mid-air to spin faster, extend to slow down, and stick the landing on the glowing mat — all rendered on an HTML5 canvas with a procedural neon-gym backdrop.

No build step, no dependencies to install, no bundler. Open `index.html` and play.

**[▶ Play it live](#deploying-to-github-pages)** once you've enabled GitHub Pages (steps below), or just double-click `index.html` locally.

---

## Controls

| Action | Input |
|---|---|
| Charge the jump | Hold **Space**, or click/tap and hold |
| Launch | Release Space / click / tap |
| Tuck (spin faster) mid-air | Hold Space / click / tap again |
| Extend (slow rotation, prep landing) | Release |
| Reset the current attempt | **Reset** button |
| Advance after a clean landing | **Next Level** button |

A small rotation gauge appears near the top of the screen while airborne — the green arc marks the "upright" window, so you can time your extend precisely.

## How landing works

Land upright (within ~24° of vertical), with low fall speed and low spin, **inside the marked landing zone**, and hold that for a moment to lock in the level. Miss any of those and Flip Man collapses into a ragdoll — dust and sparks fly, and you can reset and try again.

Every level's landing zone is placed by actually simulating the jump physics ahead of time (same formulas as the real launch), so the zone is always reachable within a specific charge-hold window — nothing is placed by guesswork.

## Levels

1. **Warm-Up Mat** — flat floor, no obstacles, wide forgiving window. Learn the flip.
2. **The Pit** — a floor gap you must clear.
3. **High Beam** — a raised beam mid-arc; throw with enough height to clear it.
4. **The Gauntlet** — gap *and* beam together, with a tighter charge window.
5. **Zero-G Arena** — reduced gravity for a longer, floatier flight and a higher beam.

## Tech

- Plain HTML5 Canvas 2D for rendering — no WebGL, no game engine
- [Tailwind CSS](https://tailwindcss.com/) (via CDN) for the HUD overlay
- A small hand-rolled 2D ragdoll rig (stick-figure skeleton with distance-constraint joints) used for:
  - the controlled flip pose while airborne (interpolated between an extended and a tucked template)
  - a Verlet-integrated physics collapse on failed landings
- Zero build tooling — it's a single `index.html` with an inline `<script>`. Nothing to `npm install`.

## Running locally

Just open the file:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html        # Windows
```

Or serve it (recommended if your browser restricts local file access for some APIs):

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`, pick your default branch and the `/ (root)` folder.
4. Save. GitHub will publish `index.html` at `https://<your-username>.github.io/<repo-name>/`.

No build step is required since the game is a static file.

## Project structure

```
.
├── index.html      # the entire game — markup, styles, and game logic
├── LICENSE
└── README.md
```

## License

MIT — see [LICENSE](./LICENSE).
