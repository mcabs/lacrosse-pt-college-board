# Data notes — men's lacrosse + physical therapy college list

## Coverage summary

**80 schools** (as of the LaxNumbers verification pass below; 84 originally). Built as the intersection of every
US men's varsity lacrosse program (D1/D2/D3/NAIA) against the CAPTE-accredited DPT program list and a
separately-verified list of 3+3/direct-entry freshman DPT programs.

| Division | Lacrosse programs researched | Schools with a PT pathway (included) |
|---|---|---|
| D1 | 77 | 22 |
| D2 | 83 (80 currently active — see below) | 17 |
| D3 | 241 (234 currently active — see below) | 38 |
| NAIA | 33 (28 currently active — see below) | 3 |
| **Total** | **434** | **80** |

By PT type:
- **3+3-direct-entry** (guaranteed/reserved freshman-entry DPT seat): **31 schools**
- **dpt-on-campus** (accredited DPT exists on campus, not freshman-guaranteed): **49 schools**
- **pre-pt**: 0 schools tagged. See "Scope limitation" below — this category was not exhaustively researched.

## LaxNumbers.com verification pass (post-launch correction)

After initial publication, the full dataset was cross-checked against **laxnumbers.com**'s live 2026 season
rankings — a current, actively-maintained source of which programs actually fielded a team and played games this
season, as opposed to Wikipedia/NCSA lists which can lag real-world program changes by a year or more.

**D1 (77 schools): perfect match.** Every school in the dataset's D1 list corresponds exactly to LaxNumbers'
77-team 2026 ranking. No changes needed.

**D2: LaxNumbers currently ranks 80 active teams** (not 83). Three schools in the original source list do not
appear because they have not started competing yet, not because of a research error:
- **Barry University** — adding men's lacrosse starting **spring 2027** (not yet playing). Was never in the
  final 84-school PT dataset (no PT-program match), so no removal was needed.
- **Ferrum College** — reclassifying D3→D2; unclear current-season status. Also never in the final dataset.
- **Nova Southeastern University** — men's lacrosse was announced years ago but has been delayed repeatedly and
  **still has not launched**; NSU's own athletics site lists no men's lacrosse team (women's only). **This one
  WAS in the dataset** (tagged 3+3-direct-entry) and has been **removed**.

**D3: LaxNumbers currently ranks 234 active teams** (not 241). Of the dataset's 39 D3 schools, 38 were confirmed
still actively fielding a team. One was not:
- **Mount St. Joseph University (OH)** — no 2025 or 2026 schedule exists on the school's own athletics site; the
  most recent listed season was 2024. Program appears discontinued. **Removed** from the dataset.

**NAIA: LaxNumbers currently ranks only 28 active teams** (not 33). Of the dataset's 5 NAIA schools, 3 were
confirmed active (Clarke, St. Ambrose, Cumberlands). Two were not:
- **Concordia University Ann Arbor (MI)** — confirmed via multiple news sources: the school **discontinued all
  intercollegiate athletics** after the 2024-25 season and cut its academic programs from 53 to just 9
  (healthcare-only). No longer a viable target for an athlete — men's lacrosse no longer exists here. **Removed.**
- **University of Saint Mary (KS)** — the school itself is not closing, but men's lacrosse is no longer listed
  among its current athletic offerings. **Removed.**

**Net result: 4 schools removed** (nova-southeastern, mount-st-joseph, concordia-ann-arbor, saint-mary-ks),
bringing the dataset from 84 to **80 schools**. This is a good example of why the app's data should be treated
as a snapshot, not gospel — programs get cut on short notice, especially at smaller/financially-stressed schools.
If your son gets serious about a smaller private school on this list, it's always worth a quick check that the
program is still running before investing recruiting effort.

## Stats coverage (of the 80 included schools)

- **avg_sat**: verified for ~55, unverified/null for the rest (mostly test-optional/test-blind small schools
  with too few SAT submitters to report, e.g. Misericordia, Concordia Wisconsin, Plymouth State)
- **avg_gpa**: verified for ~36 — many schools genuinely do not publish an average incoming HS GPA figure in
  their Common Data Set; this is a real reporting gap in higher-ed data, not a research shortfall
- **tuition**: verified for 79 of 80 (Indianapolis has no clean published sticker-tuition figure)
- **city, state, region, public/private, division**: 100% complete for all 80 schools
- All fields marked "unverified" are `null` in the data — no numbers were fabricated or estimated as precise
  figures. A few SAT figures are explicitly noted by the research as derived midpoints of a percentile range
  rather than a single reported average; those are flagged unverified even when a range did exist.

## How the list was built

1. Full men's lacrosse rosters pulled from Wikipedia (D1, D2) and NCSA Sports' compiled list (D3, since no
   single current Wikipedia page lists D3 lacrosse), plus the current NAIA member list.
2. Full CAPTE-accredited DPT list (272 institutions) compiled primarily from the PTCAS Program Directory
   (APTA's centralized application service), cross-checked against PTCAS's non-participating-programs list.
   CAPTE's own site/PDF were not machine-readable this session.
3. A 3+3/direct-entry freshman DPT list (55 confirmed schools) built via targeted search and verified against
   each school's own admissions-page language for genuine "freshman applies, seat is guaranteed or
   conditionally guaranteed" pathways — schools with only a competitive/holistic-review accelerated track
   (e.g. Elon, Chapman, Slippery Rock) were intentionally NOT tagged 3+3, and are excluded from this list
   unless they also have a standalone DPT program (in which case they're tagged `dpt-on-campus`).
4. Every lacrosse school (434 total) was checked by name against both PT lists. Matches became the 84-school
   dataset (later corrected to 80 — see the LaxNumbers verification pass above); misses were excluded (not
   logged individually per-school — see scope limitation below).
5. City, public/private, region, and stats were researched per school by parallel research passes, each
   citing source URLs (stored in `source_urls` per school — 1 URL kept per school for spot-checking, though
   most schools had 2-3 sources cross-referenced during research).

## Known gaps / things worth a manual double-check

- **Lenoir-Rhyne University (D2, NC)** is commonly cited as having a PT program alongside lacrosse, but did
  not appear in our CAPTE-derived source list (which is ~high-confidence but self-reported as not
  100%-guaranteed-complete by the research agent). Worth verifying directly at lenoir-rhyne.edu if of interest.
- **Le Moyne College (D1, NY)** and **Detroit Mercy (D1, MI)** are Jesuit/health-sciences-oriented schools that
  were checked but not found on the PT source lists — also worth a manual check if your son is interested,
  since well-known health-sciences schools are exactly the kind our source lists could plausibly miss.
- **LIU (id: `liu`)**: the lacrosse team plays out of the Post/Brookville campus; the DPT program is on LIU's
  Brooklyn campus. Same university, different physical campus — worth clarifying with LIU directly what this
  means practically for a student-athlete.
- **High Point University** has an accelerated freshman PT pathway that the school describes as "holistic
  review" rather than a guarantee — tagged conservatively as `dpt-on-campus` rather than `3+3-direct-entry`.
  Worth asking admissions directly, since in practice it may function close to guaranteed for strong applicants.
- The SUNY Upstate 3+3 partner network reportedly has more partner colleges beyond the 4 confirmed here
  (SUNY Brockport, Cortland, Geneseo, and Marist independently) — SUNY Upstate's own partner page blocked
  automated access. Worth a direct look at upstate.edu/chp/programs/physical-therapy if pursuing this network.

## Scope limitations (by design, for this v1 pass — flagged per PLAN.md guardrails)

- **`pre-pt` category not populated.** The plan allows a third PT-pathway type for schools with a strong
  pre-PT/exercise-science path but no DPT program on campus. Identifying these reliably would require
  individually researching each of the ~350 lacrosse schools that didn't match the DPT/3+3 lists — not done in
  this pass. If useful, this is a natural "second run" scope expansion.
- **Individual exclusion log not kept per-school.** PLAN.md asked for a log of every lacrosse school checked
  and excluded for lacking a PT pathway. Given the scale (434 schools), this was tracked as "matched against
  full CAPTE (272) and 3+3 (55) lists, non-matches excluded" rather than a school-by-school written log. The
  full source lists are preserved in `research_raw.md` if you want to audit any specific exclusion.
- **Website field** (school homepage URL) was not populated in this pass — `source_urls` contains working
  research links per school, but a clean homepage link wasn't separately collected. Can be added via the app's
  edit feature or a follow-up pass.
- **3+3 list confidence**: high but not guaranteed exhaustive — the research agent flagged medium confidence
  on completeness given the scale of PT programs nationally (~270+). A handful of additional direct-entry
  programs may exist that didn't surface via search.

## "Show all lacrosse schools" toggle — the no-PT-match pool (added after launch)

The app now has a second tier of data behind an off-by-default toggle: **every other men's lacrosse program in
the country**, not just the 80 with a confirmed PT pathway. Rationale: a general pre-med/pre-health track at any
school can still lead to PT school later (via a standard post-bacc DPT application), so a family may want the
full lacrosse landscape as a backup/comparison view, not just the PT-filtered shortlist.

**Coverage: 339 additional schools** (419 total with the original 80), tagged `pt_type: "none"`. Source: the
same live LaxNumbers 2026 rosters used for the correction pass above (D1: 77, D2: 80, D3: 234, NAIA: 28 =
419 currently-active programs), so — unlike the original Wikipedia/NCSA-sourced universe — this pool is already
current and doesn't carry the "discontinued program" risk described earlier in this document.

**What's researched for these 339 schools:**
- Division, state, region: 100% complete, sourced directly from the verified-active rosters.
- Public/private status: researched for all 339 (parallel batch classification, cross-checked for tricky cases
  like same-named public/private pairs — e.g. Alfred University (private) vs. Alfred State (public), Bridgewater
  College VA (private) vs. Bridgewater State MA (public)).
- **Not researched: city, conference, SAT, GPA, tuition, enrollment, acceptance rate.** These display as "—" in
  the app. This is a deliberate scope cut — full stats research for 339 more schools would roughly quadruple the
  research already done for the 80 PT-matched schools. If your son narrows in on specific schools from this
  expanded list, the app's **Edit** button lets you fill in real numbers as you find them, and that data persists
  in the browser.
- PT status for these 339 is genuinely **"not confirmed found"**, not **"confirmed absent"** — the original PT
  program research (CAPTE list + 3+3 list) was thorough but not treated as 100% exhaustive (see "3+3 list
  confidence" above). A school showing "No PT Match" could still turn out to have a program; it just didn't
  surface in this project's research.

## Files in this folder

- `schools.json` — the 80-school PT-matched dataset
- `schools_all.json` — the full 419-school dataset (80 PT-matched + 339 no-PT-match), embedded into the app
- `research_raw.md` — raw lacrosse rosters (D1/D2/D3/NAIA) and PT program lists, kept for audit
- `schools_base.json` — intermediate: 84 schools with division/conference/state/pt_type only (pre-stats, pre-correction)
- `stats_*.json` — intermediate: per-batch stats research before final merge into schools.json
- `laxnumbers_*.txt` — verified-active 2026 rosters pulled from laxnumbers.com, used for both the correction
  pass and the expanded no-PT-match pool
- `nopt_pool.json`, `pp_batch*.json` — intermediate: the 339-school expansion and its public/private research
