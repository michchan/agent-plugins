# Changelog

All notable changes to the `personal-finance` plugin will be documented here.

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
