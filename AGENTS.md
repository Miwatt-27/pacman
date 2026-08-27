# Pac-Man

## Structure

- This is a dependency-free static app. Open `src/index.html` through a static HTTP server for browser verification; the repository defines no build, lint, typecheck, or test commands.
- `src/index.html` loads classic scripts in dependency order: `maze.js` -> `game.js` -> `render.js` -> `main.js`. They communicate through `window` globals, so preserve that order or replace all affected global consumers together.
- `maze.js` owns the immutable 28x31 tile map and spawn constants. `createGame()` copies `MAZE` into `game.grid`; mutate only `game.grid` during a game so restarts work.
- Tile values are `0` empty, `1` wall, `2` dot, and `3` ghost-pen door. Pac-Man cannot cross doors; ghosts can. The tunnel is `TUNNEL_ROW` and wrapping is handled in `game.js`.
- Rendering derives canvas dimensions from `TILE` (20) and the maze. Keep `src/index.html` canvas dimensions aligned with the 28x31 maze (`560x620`) if either changes.

## Workflow

- This repository uses spec-driven development for larger features. Use the local `/spec` skill to define a spec in `specs/`; `/spec-impl` implements only an approved spec and creates a `spec-NN-slug` branch by default. Read `.agents/skills/spec*/SKILL.md` when using either workflow.
