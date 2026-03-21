# Changelog

All notable changes to the `personal-finance` plugin will be documented here.

## [0.3.1] - 2026-03-21

### Changed

- `equity-analysis-workflow` `folder-structure.md`: Updated script naming convention from `.py` suffix to `.{ext}` placeholder to clarify that scripts can be in any format (Python, shell, etc.), not exclusively Python; updated examples and cross-references

## [0.3.0] - 2026-03-21

### Added

- `equity-analysis-workflow` Phase 2 Step 2 (Financial Model) `data-requirements.md` and `data-file-template.md`: Added **Quality & Capital Efficiency Ratios** section with return-on-equity, return-on-assets, return-on-invested-capital, asset turnover, and inventory turnover metrics
- `equity-analysis-workflow` Phase 2 Step 1 (Company Research) `additional-sections.md`: Added two new output sections — company history/events/acquisitions (trailing 20 years) and major past price actions (trailing 10 years)
- `equity-analysis-workflow` Phase 2 Step 1 (Company Research) `data-requirements.md`, `data-file-template.md`, `data-fetch-protocol.md`: Extended with fields for the two new company research sections
- `equity-research:initiating-coverage` `SKILL.md`: Added `additional-sections.md` to the reference file lookup table

### Changed

- `equity-analysis-workflow`: Swapped step order — **Financial Model is now Step 1, Company Research is Step 2** so that company research can reuse already-fetched historical financial data instead of re-fetching it; updated all step references, folder names, and cross-step source citations
- `equity-analysis-workflow` Phase 2 Step 2 (Company Research) `data-fetch-protocol.md`: Added fallback fetch instructions for when the financial model step is skipped
- `equity-analysis-workflow` Phase 2 Q4=5 "Research and thesis only" scope: Updated to run steps 1→2→5 (Financial Model → Company Research → Report) so financial data is always available for the narrative
- `equity-analysis-workflow` Phase 2 Step 2 (Financial Model) `data-requirements.md` and `data-file-template.md`: Expanded Income Statement, Balance Sheet, and Cash Flow Statement field lists; added EBITDA, margins, EPS, Revenue Growth %, OpEx detail (R&D/S&M/G&A)
- `equity-analysis-workflow` Phase 2 Step 2 (Financial Model) `data-fetch-protocol.md`: Replaced inline formula table with a cross-reference to `data-requirements.md`
- `equity-analysis-workflow` `references/folder-structure.md`: Hidden system folders from the displayed folder structure
- `equity-analysis-workflow` Phase 2 Step 5 (Report Generation) `output-preferences.md`: Refined output preference wordings

## [0.2.6] - 2026-03-21

### Changed

- `equity-analysis-workflow` Phase 2 Step 2 (Financial Model) `data-requirements.md`: Added **Time Span by Equity Type** table (Growth → 5 years, Core → 8 years, Defensive → 12 years) as the single source of truth for trailing-year span; updated IS, BS, and CF field rows to reference it by name instead of hardcoded counts
- `equity-analysis-workflow` Phase 2 Step 2 (Financial Model) `data-file-template.md`: Expanded IS, BS, and CF tables to 12 rows each (`FY{YEAR}` through `FY{YEAR-11}`) to cover the maximum span; added soft-reference note pointing to `data-requirements.md` › Time Span by Equity Type
- `equity-analysis-workflow` Phase 2 Step 2 (Financial Model) `data-fetch-protocol.md`: Updated IS, BS, and CF rows to soft-reference the time span table; added **Manual Prompt Batching** section with a `ceil(N/4)` batching algorithm for spans exceeding 5 years under Manual prompt mode

## [0.2.5] - 2026-03-19

### Added

- `equity-analysis-workflow` `folder-structure.md`: Added `Scripts/` directory adjacent to `Data/` at both the Screening level and the Ticker level — stores generation scripts for binary outputs (`.xlsx`, `.pptx`, `.docx`) using a `{YYYY-MM-DD}-{script-action-name}-{output-file-name}.py` naming convention
- `equity-analysis-workflow` `folder-structure.md`: Added Scripts rules section — naming convention, most-recent-file discovery rule
- `equity-analysis-workflow` `SKILL.md`: Added **Scripts** rule section with save rule (persist script after each binary output), discovery rule (check Scripts/ before formatting-intent steps), and trigger signals for the script-only update path

## [0.2.4] - 2026-03-19

### Added

- `output-preferences.md` for Phase 2 Step 5 (report generation): specifies SF Pro font, bullet-heavy writing style, and a requirement to visualize historical/comparable figures
- Reference to `output-preferences.md` in the skill's reference file lookup table in `SKILL.md`

### Changed

- Minor wording cleanup in `SKILL.md`: removed hardcoded example subdirectory path to keep the instruction generic

## [0.2.3] - 2026-03-19

### Fixed

- `equity-analysis-workflow` Phase 2 instruction: Added Q6 (data collection mode) to scope confirmation — asked before execution begins when at least one fetch will occur, fixing a gap where pre-fetch confirmation was silently skipped in "all at once" mode (Q5)
- `equity-analysis-workflow` `SKILL.md`: Added timing note to pre-fetch confirmation section clarifying that "all at once" mode requires Q6 (or equivalent) to be surfaced during scope confirmation, not mid-execution

## [0.2.2] - 2026-03-19

### Changed

- `equity-analysis-workflow` `SKILL.md`: Added visual emphasis markers to "Rules" section header and pre-fetch confirmation header to improve agent compliance
- `equity-analysis-workflow` Phase 2 instruction: Added explicit rule to respect `SKILL.md` for any questions before starting
- `equity-analysis-workflow` Phase 2 Step 3 (DCF) `data-requirements.md`: Clarified peer comparable note to cover manual data prompts in addition to live fetches

## [0.2.1] - 2026-03-19

### Changed

- `equity-analysis-workflow` Phase 2 Step 3 (DCF): Added 4-level peer data resolution protocol to `data-fetch-protocol.md` — before fetching from Yahoo Finance, the agent checks (1) subject's own peer data cache, (2) other tickers' peer data files, (3) peer's own financial model. Reduces redundant fetches when peers overlap across tickers in the same sector.
- `equity-analysis-workflow` Phase 2 Step 3 (DCF): Added transparency summary table showing per-peer, per-field data source before DCF runs.
- `equity-analysis-workflow` Phase 2 Step 3 (DCF): `data-requirements.md` notes the cache resolution protocol with a soft reference to `data-fetch-protocol.md`.

## [0.2.0] - 2026-03-17

### Changed

- `equity-analysis-workflow`: Absorbed Phase 3 (Comparison) into Phase 2 as Step 4 — workflow is now 4 phases: Screening → Deep Dive → Thesis → Ongoing Review
- `equity-analysis-workflow` Phase 2: Now 5 steps — Company Research → Financial Model → DCF → Competitive Analysis → Report Generation
- `equity-analysis-workflow` Phase 2: Added pre-execution scope confirmation with 14-row branching table (folder check, report/data mode, scope, cadence)
- `equity-analysis-workflow` Phase 2 Step 3 (DCF): Added peer comparable data section (7 fields, `{YYYY-MM-DD}-peer-data.md`)
- `equity-analysis-workflow`: Renamed/renumbered phase commands — `equity:phase-3-compare` removed; `equity:phase-4-thesis` → `equity:phase-3-thesis`; `equity:phase-5-review` → `equity:phase-4-review`
- `equity-analysis-workflow` `folder-structure.md`: Updated for date-prefixed Data/ files and `{YYYY-MM-DD}-initiation-report/` subfolders
- `equity-analysis-workflow` `SKILL.md`: Updated 4-phase table and rhythm diagram

### Fixed

- `equity-analysis-workflow`: Extended cache TTLs for slow-moving data across 14 `data-requirements.md` files — consensus estimates, peer metrics, peer margins, macro indicators, screening multiples, event dates, and macro developments updated from 1 day to 3–7 days

## [0.1.5] - 2026-03-16

### Fixed

- `equity-analysis-workflow` `folder-structure.md`: Update `/Initiation/` and `/Data/` step annotations to match Phase 2 refactor — remove `competitive-analysis.md` (Step 1b) and `comps.xlsx` (Step 4), rename Step 1a → Step 1, renumber Step 5 → Step 4
- `equity-analysis-workflow` `SKILL.md`: Update step subdirectory example `step-1a-company-research/` → `step-1-company-research/`

## [0.1.4] - 2026-03-16

### Changed

- `equity-analysis-workflow` Phase 2: Remove overlap with Phase 3 — delete `step-1b-competitive-context/` and `step-4-comps/` sub-steps (competitive analysis and comps now live exclusively in Phase 3)
- `equity-analysis-workflow` Phase 2: Steps 1a and 5 renumbered — `step-1a-company-research/` → `step-1-company-research/`, `step-5-full-report/` → `step-4-full-report/`
- `equity-analysis-workflow` Phase 2: `equity-research:initiating-coverage` now invoked only once (Step 4 full report); Steps 1 and 2 are data-collection only
- `equity-analysis-workflow` Phase 2: All `data-fetch-protocol.md` files updated — prior-step output sources now note `; fallback: data file` for cross-session use

## [0.1.3] - 2026-03-16

### Changed

- `equity-analysis-workflow`: Standardize date-prefixed filenames — move `{YYYY-MM-DD}` and `{YEAR}` to the front of all file names in the folder structure reference
- `equity-analysis-workflow`: Move `/_archived/` from `/Data/` to the root of the ticker folder

## [0.1.2] - 2026-03-16

### Changed

- **Top-down screening references**: Added 5 new data fields to `data-requirements.md`, `data-file-template.md`, and `data-fetch-protocol.md` to close gaps identified across two consecutive sector screens (cybersecurity, financial services). New fields: Market Size & TAM, Competitive Landscape, Peer Revenue Snapshot, Regulatory / Structural Risks, Recent M&A / Corporate Events. Updated Analyst Consensus field to include top stock picks by name.

## [0.1.1] - 2026-03-15

### Changed

- **`equity-analysis-workflow` SKILL.md**: Restructured into `## Rules` + `## Tasks` sections. Pre-fetch confirmation and other data handling rules are now in `## Rules` (read before any task), preventing the agent from skipping them. Phase table and Rhythm at a Glance moved to `## Tasks`. No content changes — prose preserved verbatim.

## [0.1.0] - 2026-03-15

Initial release of the `personal-finance` plugin.

### Added

- **Plugin**: `personal-finance` — wraps Anthropic's `equity-research:*` and `financial-analysis:*` skills with a personal buy-and-hold investor lens and core-satellite portfolio philosophy.
- **Skill**: `equity-analysis-workflow` — 5-phase workflow (Screening → Deep Dive → Comparison → Thesis → Ongoing Review) for researching, valuing, and monitoring equity positions.
- **Commands**: `equity:phase-1-screen` through `equity:phase-5-review` — phase-level slash commands for direct invocation of each workflow phase.
- **References**: Per-phase instruction files and per-step data requirement, data fetch protocol, and data file template documents covering all workflow phases and sub-steps.
- **Data handling**: Cache read-before-fetch and write-after-fetch protocol to minimize redundant web requests.
- **Folder structure**: Defined lifecycle-aware folder layout for persisting research artifacts, including `_archived/` conventions for stale data.
- **Manual data prompt template**: Reference template for providing data manually when live fetching is not possible.
