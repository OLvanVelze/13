## Purpose

This file gives concise, repo-specific guidance for AI coding agents working on the TUD JupyterBook portfolio for TN13015.

## Big picture
- This repository is a JupyterBook site (source root: repository root) that builds into `_build/html` using `myst build --html`.
- Content lives under `Content/` (student labs and notebooks). Course pages and config live in the repository root (`index.md`, `intro.md`, `myst.yml`, `toc.yml`, `plugins.yml`).

## Build & deploy (what actually runs in CI)
- CI uses `.github/workflows/deploy.yml` which installs `mystmd` (npm) and runs `myst build --html`.
- Local quick commands:
  - Install Python deps: `pip install -r requirements.txt` and optionally `pip install -r Content/Github/requirements.txt` for lab notebooks.
  - Install MyST CLI (if using the same step as CI): `npm install -g mystmd` then `myst build --html`.
  - Alternative: `pip install -U jupyter-book` then `jupyter-book build .` (produces `_build/html`).

## Where to change content
- Page content and examples: `index.md`, `intro.md`, `README.md`.
- Notebooks: `Content/PySim/` (e.g. `5_druktemp.ipynb`) and `Content/Labs/`.
- Styling: `css/custom.css` and `css/TUD_stylesheet.css`.
- Figures and static assets: `Figures/`.

## Code / notebook conventions to preserve
- Many notebooks include exercise placeholders like `#your code/answer`. Preserve those when editing intended student content.
- Notebook cells in this repo include `metadata.id` values; do not remove or rename these IDs when editing programmatically — some tooling/assignments expect stable cell ids.
- Example pattern: `Content/PySim/5_druktemp.ipynb` defines global constants at the top (`BOX_SIZE_0`, `N`, `DT`, `RADIUS`) used across cells; prefer editing those constants rather than changing logic in later cells.
- Example code pattern: simulation helper functions (e.g., `ParticleClass`, `handle_walls`, `take_time_step`) appear inside notebooks; when refactoring, keep function names and signatures stable or update all references within the notebook.

## Tests & quality
- There are no automated unit tests in the repo. Use `myst build --html` or `jupyter-book build .` to validate that pages render and that `Content/` notebooks execute as expected.

## Common pitfalls and patterns
- Do not modify `.github/workflows/deploy.yml` unless you understand GitHub Pages permissions (the workflow writes Pages artifacts and uses `pages: write`).
- Notebooks may rely on `requirements.txt` and `Content/Github/requirements.txt` for package versions — installing these is required to run code cells locally.
- Many notebooks use global variables (e.g. `impulse_outward`, `pressure`) — prefer minimal, targeted changes to avoid breaking later dependent cells.

## Helpful file references (examples)
- Main docs/config: `myst.yml`, `toc.yml`, `index.md`
- Notebooks: `Content/PySim/5_druktemp.ipynb`, `Content/Labs/*.ipynb`
- Styles and assets: `css/custom.css`, `Figures/`

## If you change notebooks programmatically
- Preserve `metadata.id` and language metadata in every cell (`metadata.language`).
- Keep exercise markers `#your code/answer` intact unless updating the pedagogical content.

## When in doubt
- Run `myst build --html`; check `_build/html` locally. Push to `main` to trigger the same CI deploy used by the project.

---
Please review: what else would you like the agent to highlight (tests, contributor workflow, or specific notebooks to treat carefully)?
