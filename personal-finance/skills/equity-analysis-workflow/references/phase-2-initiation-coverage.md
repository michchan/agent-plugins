# Phase 2 — Initiation Coverage

## Rules (READ FIRST)

### Objective

For any stock that clears screening, this phase builds conviction. It runs as a **sequential workflow**.

### Subtask Map

The following specifications will be used according to "Tasks" instructions.

| Step | Task |
|---|---|
| 1 | Company Research |
| 2 | Financial Modeling |
| 3 | Valuation Analysis |
| 4 | Chart Generation |
| 5 | Report Assembly |

### Pre-execution Checks

Ask in order; wait for each answer before asking the next:

1. **Equity type** (skip if context is "update") — Defensive / Core / Satellite

2. **Lifecycle stage** (skip if context is "update") — Watchlist / Screening / Holding

3. **Folder check** — Before presenting step 4, check if `/{Type}/{Stage}/{TICKER}/Initiation/` has any `*-initiation-report/` subfolders; surface the most recent name/date and cache freshness per TTL.

4. **Report and data mode**:
   - 1. New report, reuse data *(recommended when an initiation folder exists but is dated before today)*
   - 2. Update existing report, reuse data *(recommended when the most recent folder is dated today)*
   - 3. Update existing report, fresh data
   - 4. New report, fresh data *(clean slate)*

5. **Scope** for modes 1 & 4 (new report):
   - 1. Full report — Steps 1→2→3→4→5 *(default)*
   - 2. Skip Valuation Analaysis — Steps 1→2→4→5; no valuation analysis or comps; Step 4 uses consensus only
   - 3. Skip financial model — Steps 1→3→4→5; no `.xlsx`; Step 3 uses consensus estimates only
   - 4. Research & thesis only — Steps 1→5; narrative only; no Excel, no valuation, no charts

   For modes 2 & 3 (update): 1. Full re-run *(default)*, or 2. Selective — name the step(s) to re-run.

6. **Execution cadence** — Step-by-step (**default**, pause after each) or All at once.

7. **Data collection mode** — Ask only when at least one fetch will occur: always for modes 3–4; for modes 1–2 only if any relevant caches are stale or missing. See `equity-analysis-workflow/SKILL.md` › Data Collection & Compilation.

8. **Confirmation** — Emit one line then proceed immediately:
   > Running: [step list with data handling per step]. Data collection: [mode]. Writing into `/{TICKER}/Initiation/{YYYY-MM-DD}-initiation-report/`.

---

## Tasks

1. Run "Rules > Pre-execution Checks".

2. For each step in scope, find and read the corresponding detailed specification from "Rules > Subtask Map".

3. Load `equity-research:initiating-coverage` skill, with passed custom rules:
   - mention the corresponding task to do (e.g. `Task 1`)
   - follow data requirements from the skill, collect and compile data following the "Data Collection & Compilation" rules in `equity-analysis-workflow/SKILL.md`
   - respect "Analysis & Output" rules in `equity-analysis-workflow/SKILL.md`
   - respect rules in this file (e.g. generate a prompt and wait for user to collect data for "Manual prompt" data mode).

   Example prompt:
   ```
   Use `equity-research:initiating-coverage` skill, Do Task 4 for {Exchange:Ticker}, with following instructions: {Your generated extra instructions}
   ```

   The result should go in either way:
   1. If "auto fetch" data mode is selected by user, it goes straight from data collection to the result/output.
   2. If "manual prompt" data mode is selected by user, it first returns a "prompt" for user to collect the data and return to you. Then it uses the returned data to achieve the result/output.

4. Repeat steps 2–4 for each remaining step in scope.
