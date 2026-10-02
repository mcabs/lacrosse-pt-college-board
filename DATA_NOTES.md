# Data notes — men's lacrosse + physical therapy college list

## Coverage summary

**417 schools total**: **80** with a confirmed PT pathway (the app's default view) + **337** with no confirmed
PT match (visible via the "Show all lacrosse schools" toggle). The 80 were built as the intersection of every US
men's varsity lacrosse program (D1/D2/D3/NAIA) against the CAPTE-accredited DPT program list and a
separately-verified list of 3+3/direct-entry freshman DPT programs; the 337 are every other currently-active
men's lacrosse program nationally, added later at the user's request with full stats research (see below).

Every one of the 417 schools is also tagged for **Catholic affiliation** (see dedicated section below).

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

The app has a second tier of data behind an off-by-default toggle: **every other men's lacrosse program in
the country**, not just the 80 with a confirmed PT pathway. Rationale: a general pre-med/pre-health track at any
school can still lead to PT school later (via a standard post-bacc DPT application), so a family may want the
full lacrosse landscape as a backup/comparison view, not just the PT-filtered shortlist.

**Coverage: 337 additional schools** (417 total with the original 80), tagged `pt_type: "none"`. Source: the
same live LaxNumbers 2026 rosters used for the correction pass above (D1: 77, D2: 80, D3: 234, NAIA: 28 = 419
currently-active programs, minus 2 removed for closures — see below), so — unlike the original Wikipedia/NCSA-
sourced universe — this pool is already current and doesn't carry the "discontinued program" risk described
earlier in this document.

**Full stats research was done for all 337** (not just backbone data — a follow-up pass after the user flagged
that well-known schools like Michigan shouldn't show blank stats when the data is genuinely easy to find):
- Division, state, region, public/private, city: essentially 100% complete.
- **avg_sat: 283 of 337 (84%)** verified/found. The remaining ~16% are mostly genuinely test-optional/test-blind
  small schools with too few SAT submitters to report a meaningful figure — not a research gap.
- **avg_gpa: 50 of 337 (15%)** — consistent with the PT-matched 80, most schools simply don't publish an
  average incoming HS GPA.
- **tuition: 322 of 337 (96%)** verified/found.
- A small number of schools (~10-12) went through a secondary research pass after their original batch's
  sub-agent didn't fully complete; those were filled in directly with a mix of confirmed aggregator data and,
  for a handful of public/service-academy schools, well-established facts (e.g. US Merchant Marine Academy and
  US Coast Guard Academy have $0 tuition — federal service academies). A few schools (Transylvania University,
  SUNY Maritime, Eastern University PA, Farmingdale State, Penn College) could not be confirmed this session and
  are left fully null/unverified rather than guessed.
- PT status for these 337 is genuinely **"not confirmed found"**, not **"confirmed absent"** — the original PT
  program research (CAPTE list + 3+3 list) was thorough but not treated as 100% exhaustive (see "3+3 list
  confidence" above). A school showing "No PT Match" could still turn out to have a program; it just didn't
  surface in this project's research.

### Two more closures caught during this research pass

- **Anna Maria College (MA, D3)** — permanently closed after the Spring 2026 semester (announced April 2026,
  closed May 2026, filed Chapter 11 in June 2026). Removed from the dataset entirely.
- **Siena Heights University (MI, NAIA)** — reportedly closing at the end of the 2025-26 academic year per its
  Wikipedia page. Removed from the dataset entirely.

Both were caught incidentally while researching stats, not through a dedicated closure-check pass — a reminder
that this dataset is a snapshot and smaller private schools in particular can change status with little notice.

## Catholic affiliation tagging (added after launch)

Every one of the 417 schools was individually researched and tagged `catholic: true/false`, with a short
`catholic_note` naming the founding order/diocese where applicable. **Result: 81 of 417 schools are
Catholic-affiliated.** Shown in the app as a ✝ badge on cards/table rows, filterable via "Religious affiliation"
in the filter panel, and included in CSV exports and the side-by-side compare view.

**This was deliberately not done by name pattern** — guessing from "Saint ___" or "Mount St. ___" in a school's
name would have been wrong in both directions:
- **False positives avoided**: St. Lawrence University (historically Universalist/nonsectarian), Hobart
  (Episcopal), Mount St. Mary's College at Maryland is actually a *public* honors college despite the name.
- **Secularized-but-Catholic-founded schools correctly excluded** (per the "still maintains Catholic identity"
  standard used, not just historical founding): Marist University (Marist Brothers founding, but the Archdiocese
  of New York has publicly stated it's no longer Catholic), Manhattanville College (Religious of the Sacred
  Heart, secularized 1969-71), Nazareth University (removed from the Official Catholic Directory in 2003),
  Stevenson University MD (Sisters of Notre Dame de Namur founding, independent since 1967), Lynn University FL
  (founded as Marymount College by a Catholic order, later secularized).
- **Non-obvious true positives caught**: Villanova (Augustinian), Fairfield (Jesuit), Manhattan College, Canisius,
  Iona, Le Moyne, Mercyhurst, Lewis University IL, John Carroll — none have "Catholic," "Saint," or an obviously
  religious word in the name, but are all genuinely Catholic-affiliated today.
- A few schools carry real nuance even among the 81 counted `true`: e.g. Walsh University and Wheeling University
  both lost their original founding order's direct sponsorship (Walsh's Brothers of Christian Instruction
  withdrew in 2021; Wheeling dropped "Jesuit" from its name) but both remain explicitly Catholic institutions
  under new sponsorship — kept as `true` with a note explaining the change.

Research was done via 8 parallel batches (~52 schools each), each explicitly instructed to verify rather than
pattern-match, with cross-checks against Wikipedia and each school's own "about/mission" pages for ambiguous
cases. High confidence overall, but as with the rest of this dataset, treat it as a strong starting point rather
than a canonical religious-directory-grade classification — a handful of schools with genuinely ambiguous or
recently-changed status could be mis-tagged.

## Merit aid tagging (added after launch)

Every one of the 417 schools was researched and tagged `merit_aid: true/false`, with a short `merit_aid_note`
describing the program where known (e.g. "automatic scholarships for 3.5+ GPA/1200+ SAT" or "need-based aid
only"). Shown in the app as a green "$ Merit Aid" badge or a muted "Need-Based Only" badge, filterable via
"Merit aid" in the filter panel, and included in the compare view and CSV export.

**Result: 379 of 417 schools (91%) offer merit aid; 38 (9%) are need-based-aid-only.** The distinction that
matters here isn't selectivity in general — it's a specific, well-documented institutional policy choice:

- **The need-based-only list is almost entirely two groups**: the Ivy League + peer-tier schools (Princeton,
  Harvard, Yale, Brown, Columbia-tier, Cornell, Penn, Dartmouth, Duke, Georgetown, MIT, Johns Hopkins, Notre
  Dame) and the most selective liberal arts colleges (Amherst, Williams, Swarthmore, Bowdoin, Middlebury,
  Colby, Haverford, Vassar, Oberlin, Kenyon, Colorado College, Connecticut College, Trinity, Hamilton, Bates,
  Wesleyan CT, Holy Cross), plus the federal service academies (Army, Navy, Air Force, Coast Guard, Merchant
  Marine — tuition-free via military service commitment rather than any scholarship model).
- **Non-obvious need-based-only catches**: UNC Chapel Hill (its own aid office is need-based only — the
  well-known Morehead-Cain and Robertson programs are separate, externally-funded, ~1-2%-acceptance programs,
  not general UNC merit aid), University of Virginia (same pattern — Jefferson Scholars is an independent
  foundation), University of Michigan (need-based aid is the general policy; only a small number of narrow
  departmental awards exist outside it), and Hamilton College (eliminated merit scholarships in 2008).
- **Non-obvious merit-aid catches** (schools you might assume are need-based-only given their selectivity, but
  actually run a real merit program): Washington & Lee (the Johnson Scholarship covers full tuition+room+board+
  stipend for ~10% of each class, explicitly merit-based, alongside otherwise need-based aid), Bucknell and
  College of the Holy Cross (both meet-full-need schools, but each awards a small number of genuine non-need
  merit scholarships), Dickinson and Gettysburg (merit-generous despite selective-LAC profiles).
- The remaining ~370 schools — nearly every mid-tier and smaller private college, plus most public
  universities — confirmed real merit scholarship programs, usually automatic tiers keyed to GPA/SAT/ACT and
  awarded regardless of financial need. This is standard practice at tuition-discounting institutions and was
  the expected pattern; research batches devoted more individual verification effort to the ambiguous/elite
  cases above and to smaller regional schools with less name recognition, while confirming the broad pattern
  for schools clearly in the "everyone offers merit aid here" category.

As with GPA/tuition figures elsewhere in this dataset, some individual `merit_aid_note` amounts (specific dollar
figures, GPA thresholds) came from aggregator sites rather than each school's own current-year page and can
change year to year — treat them as directional, and verify current figures directly with the school before
relying on them for a financial decision.

## D1 NCAA RPI ranking (added after launch)

All **77 D1 schools** (across both the PT-matched 22 and the no-PT-match 55) now carry `rpi_rank_2026` and
`rpi_record_2026`, sourced directly from the NCAA's own [D1 men's lacrosse RPI rankings page](https://www.ncaa.com/rankings/lacrosse-men/d1/ncaa-mens-lacrosse-rpi),
current through games May 25, 2026 — the final ranking of the just-completed spring 2026 season. All 77 matched
cleanly by school name (verified programmatically, not eyeballed) with no ambiguous cases.

This is **D1-only** — the NCAA doesn't publish an RPI for D2, D3, or NAIA men's lacrosse, so those divisions have
no `rpi_rank_2026` field and show no RPI badge. Shown in the app as a "RPI #N" badge next to the division badge
(hover for the season record), sortable via "D1 RPI rank: best to worst" in the sort dropdown or by clicking the
"D1 RPI" table column header, and included in the compare view and CSV export.

Note this is a **snapshot of the completed 2026 season** — it will not update automatically as the 2027 season
progresses. If you want current in-season rankings later, the source page will have them; ask for a refresh and
this section can be re-run the same way.

## Forbes rank, 10-year salary, and U.S. News rank (added after launch)

Source: `forbes_top_500_colleges_2027.xlsx`, supplied by the user (Forbes America's Top Colleges 2027, 500 rows).
Three columns were incorporated: **Rank** -> `forbes_rank`, **Median 10-Year Salary** -> `forbes_salary_10yr`, and
**US News 2027 Rank** -> `us_news_rank` (+ `us_news_tie` true when the file says "T-N"). The file's other columns
(grant aid, median debt, financial grade, type) were not used.

- **Coverage: 168 of 417 schools** appear in the Forbes top 500 (including 26 of the 80 PT-matched schools). The rest
  simply aren't in that list, so they show a blank, not a low score.
- **US News from the spreadsheet was superseded**: that column only had 48 values (28 for our schools), so the U.S. News
  rank now comes from the live U.S. News site instead (next section). The 28 values in the spreadsheet all agree
  with the live site.
- **Matching**: normalized name + state first (138 schools), then every remaining dataset school was reviewed
  against the full Forbes list by hand. 30 were mapped explicitly (e.g. Penn, Michigan, Maryland, MIT, RPI, RIT,
  UMBC, NJIT, VMI, Penn State, the SUNY campuses). One automatic match was wrong and corrected
  (Connecticut College had matched University of Connecticut). No two schools share a Forbes rank.
- **Judgment call**: "Hobart" is mapped to Forbes' combined entry "Hobart and William Smith Colleges".
  Fairleigh Dickinson University is in Forbes but not mapped, because this dataset only has the FDU-Florham campus.
  The service academies, LIU, and most small D2/D3/NAIA schools are not in the Forbes list.
- UI: Forbes and US News badges on each card, a 10-yr salary stat line, three sortable table columns, three sort-dropdown
  options, compare-view rows, and CSV columns (`forbes_rank`, `us_news_rank`, `us_news_tie`, `forbes_salary_10yr`).

## U.S. News 2027 rank, all categories (added after launch)

Source: the U.S. News Best Colleges 2027 ranking pages (National Universities, National Liberal Arts Colleges,
Regional Universities North/South/Midwest/West, Regional Colleges North/South/Midwest/West), read in the user's own
Chrome. Fields: `us_news_rank`, `us_news_tie` (true = tied rank), `us_news_category`. Per-category match files are
`usnews_2027_*.json` (school id -> rank/tie/category).

- **Coverage: 397 of 417 schools.** The other 20 (e.g. SCAD, Emerson, Southern New Hampshire, FDU-Florham, Thomas, Castleton,
  Life University, Missouri Baptist) did not appear in any ranked list, so they show no U.S. News badge.
- **Ranks are only comparable within a category.** A #8 in Regional Colleges North is not a #8 National University. The badge
  names the category, and the "US News rank" sort groups National Universities first, then Liberal Arts, then the regional
  lists, ranking within each group.
- **Matching**: normalized name + state, with ambiguous cases (Boston University vs. Boston College, Michigan, Rutgers) resolved
  by hand and name variants (Penn State, UMass campuses, service academies, SUNY campuses, RPI/RIT/NJIT, Sewanee,
  Hobart and William Smith, etc.) mapped explicitly. A recurring false match (Connecticut College vs. University of
  Connecticut) was caught and excluded.
- **Loading note**: U.S. News serves 10-20 schools per "Load More" and slows badly past ~250 cards, so the National
  Universities list was loaded in two passes (A-Z and Z-A) to cover the long tail of low-ranked schools (ranks up to ~376).
- Ranks are a snapshot of the 2027 edition as published (with the September 22, 2026 correction noted on the page).

## Files in this folder

- `schools.json` — the 80-school PT-matched dataset
- `schools_all.json` — the full 417-school dataset (80 PT-matched + 337 no-PT-match), embedded into the app
- `research_raw.md` — raw lacrosse rosters (D1/D2/D3/NAIA) and PT program lists, kept for audit
- `schools_base.json` — intermediate: 84 schools with division/conference/state/pt_type only (pre-stats, pre-correction)
- `stats_*.json` — intermediate: original per-batch stats research for the 80 PT-matched schools
- `laxnumbers_*.txt` — verified-active 2026 rosters pulled from laxnumbers.com, used for both the correction
  pass and the expanded no-PT-match pool
- `nopt_pool.json` — the 337-school no-PT-match dataset (public/private + full stats)
- `pp_batch*.json` — intermediate: public/private classification research for the 337-school pool
- `stat_result_*.json` — intermediate: full stats research (SAT/GPA/tuition/enrollment/acceptance) for the
  337-school pool, per research batch
- `catholic_batch_*.txt`, `catholic_result_*.json` — intermediate: Catholic-affiliation research batches for
  all 417 schools
- `merit_batch_*.txt`, `merit_result_*.json` — intermediate: merit-aid research batches for all 417 schools
- `ncaa_d1_rpi_2026.txt` — raw scrape of the NCAA's final 2026 D1 men's lacrosse RPI rankings (77 schools)
- `forbes_top_500_colleges_2027.xlsx` — the Forbes 2027 top-500 spreadsheet (source for Forbes rank, 10-yr salary, US News rank)
- `usnews_2027_*.json` — per-category U.S. News 2027 rank matches (school id -> rank, tie, category); 397 schools total
