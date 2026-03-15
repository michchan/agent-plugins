# Changelog

All notable changes to the `personal-finance` plugin will be documented here.

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
