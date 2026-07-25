# PLAN — Men's Lacrosse + Physical Therapy College Finder App

> **Purpose of this file:** A self-contained execution plan so a fresh session (e.g. on Sonnet) can build this
> without re-deriving context. Read this top to bottom, then execute Phase 1 → Phase 2 → Phase 3 in order.

---

## 0. Context & Goal

Build an **interactive app** to help a high-school student-athlete narrow down and organize target colleges
for **men's lacrosse** where he can also pursue a career as a **physical therapist (PT)**.

The user is the student's parent. The deliverable is an interactive, filterable/sortable/shortlist-able tool.
There is **no old list to recover** — a prior claude.ai web chat supposedly had one, but that is not accessible
from Claude Code sessions. Build the dataset fresh via research.

### Scope decisions already made with the user (do NOT re-ask)
- **Sport:** Men's varsity lacrosse only.
- **Divisions:** ALL of NCAA D1, NCAA D2, NCAA D3, and NAIA. Tag each school with its division.
- **PT requirement:** School must have a real PT pathway. **Differentiate the type** (see PT_TYPE field). All three
  types are worth including, but the type must be labeled so the student can see the difference.
- **Geography:** All US. No location limit. (Location is still a displayed/filterable field.)
- **Data honesty:** Backbone facts (division, location, public/private, PT program + type) must be researched and
  accurate. Academic/cost stats (SAT, GPA, tuition) must be REAL — pull verifiable numbers. **Never fabricate a
  precise stat.** If a number can't be verified, leave it null and set its confidence flag to "unverified".

---

## 1. The core filter logic (READ THIS FIRST — it defines the whole list)

The target list = **intersection of two sets**:
1. Schools with a **men's varsity lacrosse team** (D1/D2/D3/NAIA), AND
2. Schools with a **physical therapy pathway**.

PT is the *constraining* filter (~250 US schools have an accredited DPT program vs ~450+ with men's lacrosse),
so the intersection is roughly **80–150 schools**. Build the list by cross-referencing, PT-first where possible.

### PT_TYPE (the differentiator) — assign exactly one primary type per school:
- **`3+3-direct-entry`** — Best fit. Guaranteed/reserved-seat bachelor's→DPT track entered as a freshman
  (a.k.a. "direct admit DPT", "3+3", "3+4", "freshman entry DPT"). Finish undergrad + DPT in ~6 years.
- **`dpt-on-campus`** — School has an accredited standalone DPT (grad) program on campus, but NOT guaranteed
  from freshman year. Undergrad would apply later, but at least the program exists on the same campus.
- **`pre-pt`** — No DPT on campus, but a strong pre-PT / exercise science / kinesiology / health-science
  undergrad that prepares for applying to DPT programs elsewhere. (Include only if it's a genuinely notable
  pre-PT path — do not pad the list with every school that has a biology major.)

(Optional secondary flag `has_3plus3` boolean is redundant with type; skip.)

---

## 2. Data schema — one record per school

Store the dataset as **`schools.json`** in this folder (array of objects). Fields:

| field            | type            | notes |
|------------------|-----------------|-------|
| `id`             | string          | slug, e.g. "sacred-heart" |
| `name`           | string          | official school name |
| `division`       | enum            | `D1` \| `D2` \| `D3` \| `NAIA` |
| `conference`     | string \| null  | lacrosse conference (nice-to-have) |
| `city`           | string          | |
| `state`          | string          | 2-letter abbrev |
| `region`         | enum            | `Northeast` \| `Mid-Atlantic` \| `South` \| `Midwest` \| `West` (derive from state) |
| `public_private` | enum            | `Public` \| `Private` (this is the "state school" flag) |
| `pt_type`        | enum            | `3+3-direct-entry` \| `dpt-on-campus` \| `pre-pt` (see §1) |
| `pt_notes`       | string \| null  | short note, e.g. "3+3 DPT, 3.2 GPA to hold seat" |
| `avg_sat`        | number \| null  | mid-50% midpoint or reported average (total, 1600 scale) |
| `avg_gpa`        | number \| null  | avg incoming HS GPA if published |
| `tuition_in`     | number \| null  | annual in-state tuition & fees (public); for private = sticker tuition |
| `tuition_out`    | number \| null  | annual out-of-state tuition & fees (public only; null for private) |
| `enrollment`     | number \| null  | undergrad enrollment (nice-to-have; helps "big vs small" feel) |
| `acceptance`     | number \| null  | acceptance rate % (nice-to-have) |
| `confidence`     | object          | per-field confidence: `{ sat: "verified"\|"unverified", gpa: ..., tuition: ... }` |
| `source_urls`    | string[]        | URLs used, for spot-checking |
| `website`        | string \| null  | school athletics or admissions URL |

Keep `schools.json` as the single source of truth. Phase 2 embeds it into the artifact.

---

## 3. Phase 1 — Research & build `schools.json`

**Goal: FULL COMPLETENESS.** This is not a sample/demo dataset — the user's son will actually use this to pick
target schools, so the list must cover the **entire intersection**: every school in the US with a men's varsity
lacrosse program (D1, D2, D3, or NAIA) that also has some form of PT pathway (`3+3-direct-entry`,
`dpt-on-campus`, or `pre-pt`). Do not stop early or cap the list at a round number. Do not settle for a
"representative sample" — go through the full source lists systematically, division by division, and check
every single lacrosse school against the PT lists. Expect the final count to land roughly in the 100–180 range,
but let the actual research determine the number — don't force it to match this estimate.

Stats (SAT/GPA/tuition) are allowed to be null+unverified when genuinely not published or not found after a
real attempt — but the CATEGORICAL fields (division, location, public/private, pt_type) must be complete for
every school in the list. Do not leave a school out of the list just because its SAT/GPA/tuition wasn't found.

### Method (do it in this order)
1. **Get the complete lacrosse universe per division — every school, not a subset.**
   - NCAA D1 men's lacrosse: Wikipedia "List of NCAA Division I men's lacrosse programs" (~75-76 schools).
   - NCAA D2 men's lacrosse: Wikipedia "List of NCAA Division II men's lacrosse programs" (~90-100 schools).
   - NCAA D3 men's lacrosse: Wikipedia "List of NCAA Division III men's lacrosse programs" (~240-250 schools,
     the largest list — don't skip or truncate it).
   - NAIA men's lacrosse: current NAIA men's lacrosse member list (~45-60 schools; check the NAIA or USA
     Lacrosse site, membership changes yearly so get a current source).
   Capture school name + division + conference for the FULL list from each source before moving on — this is
   the master roster you'll check every school against in step 3.
2. **Get the DPT universe.** CAPTE (Commission on Accreditation in Physical Therapy Education) publicly lists
   ALL accredited DPT programs (and candidate/developing programs) at `capteonline.org` — pull the full
   directory, not a partial list. Also specifically search out "3+3 DPT programs list" / "direct entry DPT
   programs" / "guaranteed admission DPT" to build the 3+3 subset — several university and PT-association pages
   maintain compiled lists of these; pull more than one source and merge them.
3. **Intersect systematically.** Go through the full lacrosse master roster from step 1 (all ~450-500 schools
   across 4 divisions) and check each one against the CAPTE list and the 3+3 list. Tag `pt_type`:
   - On the 3+3 list → `3+3-direct-entry`
   - On CAPTE DPT list but not 3+3 → `dpt-on-campus`
   - Neither, but has a genuinely notable pre-PT / exercise-science / kinesiology / athletic-training
     undergrad path (check the school's own site for this — don't guess) → `pre-pt`
   - No PT pathway found at all → exclude from schools.json, but log the school name in DATA_NOTES.md under
     "checked, excluded — no PT pathway found" so it's clear it wasn't missed, just filtered out.
   This step is the core of the work — treat it as a full pass over every lacrosse school, not spot-checking
   the schools you already suspect will match.
4. **Fill backbone fields** (city, state, region, public_private) for every included school — should be quick
   and 100% complete, no nulls here.
5. **Fill stats** (avg_sat, avg_gpa, tuition, enrollment, acceptance) from each school's Common Data Set,
   admissions page, or a reputable aggregator (e.g. the school's own CDS PDF, niche.com, collegesimply,
   petersons). Attempt every school — mark `confidence` per field as "verified" or "unverified". Only leave a
   stat null if a genuine attempt turned up nothing (e.g. very small school with no published CDS). **Do not
   guess numbers.**
6. Record `source_urls` as you go, per school.

### Efficient execution for full coverage (important for a large list on a token budget)
- Building the full ~450-500 school lacrosse roster and the CAPTE/3+3 lists is best done as a small number of
  broad list-page fetches (Wikipedia pages, CAPTE directory, NAIA roster), not one search per school.
- The stats-filling step (5) is the part that scales with school count. If running as an agent with access to
  parallel sub-agents, consider splitting the final included-school list into batches (e.g. by division or
  region) and researching stats for each batch as a separate parallel task, then merging results into one
  `schools.json`. If sub-agents aren't available, work through the list in batches sequentially and save
  progress to `schools.json` incrementally (don't hold the whole dataset only in memory until the very end —
  write/update the file as batches complete, so partial progress survives an interruption).
- It's fine (expected) for this phase to be the most time/token-intensive part of the whole plan. Budget for it.

### Known candidates as a starting cross-check (NOT the list itself — do not stop here)
> Use these only to sanity-check your systematic pass in step 3 catches known cases — the real list comes from
> the full intersection, not this seed set: Sacred Heart, Marist, Mercyhurst, Le Moyne, Gannon, Misericordia,
> Utica, Springfield College, Ithaca, Saint Joseph's (Philadelphia, post-USciences merger), Duquesne,
> Slippery Rock, East Stroudsburg, Adelphi, Dominican (NY), Nazareth, Clarkson, Stockton, Wingate,
> Lenoir-Rhyne, Belmont Abbey, Limestone, Florida Southern, Colorado Mesa. If your systematic pass over the
> full lacrosse roster doesn't turn these up (where still accurate), that's a signal a source list was
> incomplete — go back and recheck.

**Phase 1 output:** `schools.json` written to this folder with the FULL intersection dataset (not a sample),
plus `DATA_NOTES.md` listing: total count by division, stats coverage (% verified vs unverified per field),
and the list of lacrosse schools that were checked and excluded for having no PT pathway.

---

## 4. Phase 2 — Build the interactive app (Artifact)

Build a **self-contained single-file HTML artifact** (inline CSS + JS, no external requests — Artifact CSP
blocks them). Embed `schools.json` as a JS `const SCHOOLS = [...]` at the top so the file is standalone.
Before writing, load the `artifact-design` skill for design calibration.

### Must-have features
1. **Card/table view of all schools** with the key fields visible: name, division badge, location,
   public/private, PT type badge, SAT, GPA, tuition.
2. **Filters** (multi-select, combine with AND):
   - Division (D1/D2/D3/NAIA)
   - PT type (3+3 / DPT on campus / pre-PT)
   - Public vs Private
   - Region / state
   - SAT range slider, GPA range slider, tuition range slider (respect null = "unknown", don't filter those out silently — show an "include unknown" toggle)
3. **Sort** by any numeric column (SAT, GPA, tuition, enrollment) asc/desc.
4. **Search box** (by name).
5. **Shortlist / favorite** — star a school; a "My List" view shows only starred. Persist to `localStorage`.
6. **Status/tier tagging per school** — let the student mark each as e.g. Reach / Target / Likely, and
   a free-text note. Persist to `localStorage`.
7. **Compare view** — select 2–4 schools → side-by-side table.
8. **Export** — button to download the current (filtered or shortlist) set as CSV, and export the user's
   stars/tiers/notes as JSON so progress isn't lost if localStorage clears.
9. **Data-confidence indicator** — visually mark unverified stats (e.g. a small "~" or muted styling + tooltip)
   so the family knows which numbers to double-check.
10. **Add / edit school** — a form to add a school or edit any cell (including fixing a stat the family finds
    is out of date), persisted to localStorage and merged over the embedded base data, so the tool stays
    accurate over the course of the recruiting process without needing a rebuild.

### Design notes
- Theme-aware (light/dark), responsive, wide tables scroll inside their own container (page never scrolls
  horizontally). Division and PT-type as color-coded badges. Keep it clean and scannable — this is a decision
  tool, not a brochure.
- Set a `<title>`, favicon emoji (🥍 or 🎓), and a one-line description on publish.

**Phase 2 output:** the artifact file (e.g. `app.html`) in this folder, published via the Artifact tool.

---

## 5. Phase 3 — Handoff

- Tell the user: coverage (how many schools, by division), what's verified vs unverified, and how to use the
  shortlist/tier/notes + export features.
- Remind them the numbers are a starting point for a shortlist, not admissions gospel — verify final targets
  on each school's official site.
- Offer next steps: expand the dataset, add women's programs (if a sibling), add roster-size / coach-contact
  fields, or add scholarship/cost-of-attendance detail.

---

## 6. Guardrails / gotchas
- **Never invent SAT/GPA/tuition.** Null + "unverified" is always better than a made-up number.
- Some "PT programs" are grad-only with no undergrad feeder — still fine as `dpt-on-campus`, but note it.
- Watch for closed/merged schools (e.g. University of the Sciences merged into Saint Joseph's, Philadelphia).
- NAIA men's lacrosse is small and changes yearly — verify current membership.
- Division can differ by sport; use the school's **men's lacrosse** division, not its overall NCAA division.
- Artifacts must be fully self-contained (no CDN/fonts/remote images).

---

## 7. Execution checklist
- [ ] Phase 1: gather FULL lacrosse program lists (D1 ~75, D2 ~90-100, D3 ~240-250, NAIA ~45-60) — no truncation
- [ ] Phase 1: gather full DPT list (CAPTE) + full 3+3 direct-entry list (merge multiple sources)
- [ ] Phase 1: systematically intersect EVERY lacrosse school against PT lists, tag pt_type, log exclusions
- [ ] Phase 1: fill backbone fields (100% complete, no nulls) for every included school
- [ ] Phase 1: fill stats w/ confidence flags + source_urls for every included school (attempt all, null only if genuinely unpublished)
- [ ] Phase 1: write complete schools.json + DATA_NOTES.md (counts, coverage %, exclusion log)
- [ ] Phase 2: load artifact-design skill
- [ ] Phase 2: build app.html with all must-have features incl. add/edit school, embed full data
- [ ] Phase 2: publish artifact
- [ ] Phase 3: summarize full coverage + data quality + usage to user
