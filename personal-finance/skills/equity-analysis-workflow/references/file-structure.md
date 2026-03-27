# File Structure

**Always ask the user to confirm equity type and lifecycle stage before creating any files.**
This ensures outputs land in the correct folder.

## Folder Skeleton

```
/Equity-analyses/
  /Screening/
    /.data/
    /.scripts/
    /.prompts/
  /Watchlist/
    /{THEME}/
      /{TICKER}/
  /Defensive/
    /{TICKER}/
    /Closed/
      /{TICKER}/
  /Core/
    /{TICKER}/
    /Closed/
      /{TICKER}/
  /Satellite/
    /{TICKER}/
    /Closed/
      /{TICKER}/
```

## Path Descriptions

### `/Equity-analyses/`

Root folder for all equity analysis work.

### `/Screening/`

Phase 1 outputs. Equity type is not yet determined at this stage.

| Path | Description |
|------|-------------|
| `.data/{YYYY-MM-DD}-top-down-{SECTOR}.data.md` | Phase 1 top-down raw data cache |
| `.data/{YYYY-MM-DD}-bottom-up-{CRITERIA}.data.md` | Phase 1 bottom-up raw data cache |
| `.data/{YYYY-MM-DD}-events.data.md` | Phase 1 event-driven raw data cache |
| `.scripts/` | Generation scripts for Screening binary outputs |
| `.prompts/` | Saved fetch instructions (auto and manual) |
| `_archived/` | Ignored or superseded screening cache files |
| `{YYYY-MM-DD}-top-down-{SECTOR}-report.md` | Phase 1 top-down polished screening report |
| `{YYYY-MM-DD}-bottom-up-{CRITERIA}-report.md` | Phase 1 bottom-up polished screening report |
| `{YYYY-MM-DD}-events-report.md` | Phase 1 event-driven polished report |

### `/{Stage-or-Type}/[Closed/]{TICKER}/` — Stock folder layout

Shared layout used by `/Watchlist/{THEME}/{TICKER}/` and `/{Type}/[Closed/]{TICKER}/`.

#### Data files (`.data/`)

Inputs to skills. Never overwrite — always create a new dated file.

| File | Phase | Description |
|------|-------|-------------|
| `{YYYY-MM-DD}-{TICKER}-company-research.data.md` | Phase 2 Step 1 | Company research cache |
| `{YYYY-MM-DD}-{TICKER}-financial-model.data.md` | Phase 2 Step 2 | Financial model cache |
| `{YYYY-MM-DD}-{TICKER}-peer-data.data.md` | Phase 2 Step 3 | Peer data for DCF comps |
| `{YEAR}-Q{N}-{TICKER}-pre-earnings.data.md` | Phase 4 | Pre-earnings data (per event, archived) |
| `{YEAR}-Q{N}-{TICKER}-earnings.data.md` | Phase 4 | Post-earnings data (per event, archived) |
| `{YEAR}-Q{N}-{TICKER}-between-earnings.data.md` | Phase 4 | Between-earnings data (per event, archived) |
| `{YEAR}-{TICKER}-annual-review.data.md` | Phase 4 | Annual review data (per year, archived) |

#### Scripts and prompts

| Path | Description |
|------|-------------|
| `.scripts/`| Generation scripts for this ticker's binary outputs |
| `.prompts/` | Saved fetch instructions (auto and manual) |

#### Initiation report (`{YYYY-MM-DD}-initiation-report/`)

One subfolder per run — never overwrite a prior run (Phase 2).

| File | Phase | Description |
|------|-------|-------------|
| `{Ticker}-company-research.md` | Phase 2 Step 1 | Company research |
| `{Ticker}-financial-model.xlsx` | Phase 2 Step 2 | Financial model |
| `{Ticker}-valuation-analysis.md` | Phase 2 Step 3 | Valuation analysis |
| `{Ticker}-initiation-report.md` | Phase 2 Step 5 | Full initiation report |
| `charts/` | Phase 2 Step 4 | Charts folder |

#### Top-level stock files

| File | Phase | Description |
|------|-------|-------------|
| `{YYYY-MM-DD}-thesis-v1.md` | Phase 3 | Investment thesis; increment version on major updates |
| `{YYYY}-Q{N}-earnings-preview.md` | Phase 4 | Pre-earnings report |
| `{YYYY}-Q{N}-earnings-update.md` | Phase 4 | Post-earnings report |
| `_archived/` | — | Ignored or superseded files |

---

## `_archived/` folders

An `_archived/` folder may appear at any level — inside a stage/type folder (e.g. `/Screening/_archived/`, `/Watchlist/_archived/`) or inside a ticker folder. Move files here when they are superseded or no longer active. Always ignore `_archived/` when reading or discovering files.

## File management

- Do NOT create/keep empty folders.

## File naming convention

All files in `.data/`, `.scripts/`, and `.prompts/` follow the same pattern:

```
{YYYY-MM-DD}-{descriptive-name}.{type}.{ext}
```

| Type | Pattern | Example |
|------|---------|---------|
| Data cache | `{YYYY-MM-DD}-{name}.data.md` | `2026-03-25-company-research.data.md` |
| Script | `{YYYY-MM-DD}-{TICKER}-{output-name}.{action}.script.{ext}` | `2026-03-25-dcf-model.create.script.py` |
| Prompt | `{YYYY-MM-DD}-{TICKER}-{phase}-{step}-fetch.prompt.md` | `2026-03-25-phase-2-step-1-fetch.prompt.md` |

## File discovery rule

For any file type, sort by `YYYY-MM-DD` prefix and take the most recent file matching the name pattern.

## Cache file rules

- Never overwrite a data cache file — always create a new dated file.
- Never write into an existing initiation subfolder unless the user selects "Update existing report" in the Phase 2 scope confirmation (Q3 = 2 or 3).

## Lifecycle transitions

- **Screening → Watchlist**: After Phase 1, when a ticker is worth monitoring. Create the ticker folder under `/Watchlist/`.
- **Watchlist → Initiated**: After Phase 2 initiation + Phase 3 thesis. Move folder to `/Initiated/`; assign equity type (Defensive/Core/Satellite) at this point.
- **Initiated → /{Type}/**: After buying. Move folder to the appropriate type folder (e.g. `/Defensive/{TICKER}/`); no file changes needed.
- **/{Type}/ → /{Type}/Closed/**: After selling. Move folder into `Closed/`; add a closing note to the thesis file with exit rationale and date.
