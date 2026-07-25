# Lacrosse + PT College Board

An interactive tool for narrowing down college targets for a men's lacrosse recruit who's also interested in
physical therapy as a career.

**Live app:** see GitHub Pages URL for this repo (Settings → Pages), or open `index.html` directly in a browser —
it's a single self-contained file, no server or build step needed.

## What it does

- 80 schools with men's varsity lacrosse (D1/D2/D3/NAIA) **and** a real physical therapy pathway — either a
  guaranteed freshman-entry 3+3 DPT program, or an accredited DPT program on campus.
- A "Show all lacrosse schools" toggle expands to all 419 currently-active men's lacrosse programs nationally,
  including ones with no confirmed PT match (backbone info only — division/location/public-private).
- Filter by division, PT pathway, public/private, region, SAT/GPA/tuition range.
- Sort, card/table view, star a shortlist, tag schools Reach/Target/Likely with notes, compare up to 4
  side-by-side, export to CSV/JSON. All progress saves in the browser via localStorage.

## Files

- `index.html` / `app.html` — the app (identical; `index.html` exists so GitHub Pages serves it at the root URL)
- `schools.json` — the 80-school PT-matched dataset
- `schools_all.json` — the full 419-school dataset embedded in the app
- `DATA_NOTES.md` — full research methodology, data-quality notes, and known gaps
- `PLAN.md` — the original build plan
- `research_raw.md`, `laxnumbers_*.txt`, `stats_*.json`, `pp_batch*.json`, `nopt_pool*.json`, `schools_base.json` —
  intermediate research artifacts kept for audit (see DATA_NOTES.md for what each covers)

## Updating the data

Edit `schools.json` and/or `schools_all.json`, then re-embed into `app.html`/`index.html` (the data is a JS
array assigned to `SCHOOLS_BASE` near the top of the `<script>` block) and commit. Or use the app's own
"+ Add school" / Edit buttons — those changes save locally in the browser, not back to this repo.
