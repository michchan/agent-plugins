# Phase 2 — Deep Dive (Initiation)

## Rules (READ FIRST)

### Objective

For any stock that clears screening, this phase builds conviction. It runs as a **sequential workflow**.

### Subtask Map

Policy: run steps sequentially; skip steps not in scope.

| Step | Task | Skill | Specification path |
|---|---|---|---|
| 1 | Financial Data Collection | — | `step-1-financial-data/` |
| 2 | Company Research | — | `step-2-company-research/` |
| 3 | Financial Modeling | — | `step-3-financial-model/` |
| 4 | DCF Valuation | `financial-analysis:dcf` | `step-4-dcf/` |
| 5 | Competitive Analysis | `financial-analysis:competitive-analysis` | `step-5-competitive-analysis/` |
| 6 | Report Generation | `equity-research:initiating-coverage` | `step-6-report-generation/` |

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
   - 1. Full report — all steps *(default)*
   - 2. Skip DCF — Steps 1–3 → 5 → 6; no `dcf-model.xlsx`
   - 3. Skip competitive analysis — Steps 1–4 → 6; no `competitive-analysis.pptx`; Step 6 omits comp sections
   - 4. Skip financial model — Steps 1–2 → 4 → 5 → 6; no Excel outputs; Step 4 uses consensus only
   - 5. Research & thesis only — Steps 1–2 → 6; narrative only; no Excel, no DCF, no comps

   For modes 2 & 3 (update): 1. Full re-run *(default)*, or 2. Selective — name the step(s) to re-run.
6. **Execution cadence** — Step-by-step (pause after each) or All at once *(default)*
7. **Data collection mode** — Ask only when at least one fetch will occur: always for modes 3–4; for modes 1–2 only if any relevant caches are stale or missing. See `equity-analysis-workflow/SKILL.md` › Data Collection & Compilation.
8. **Confirmation** — Emit one line then proceed immediately:
   > Running: [step list with data handling per step]. Data collection: [mode]. Writing into `/{TICKER}/Initiation/{YYYY-MM-DD}-initiation-report/`.

---

## Tasks

1. Run "Rules > Pre-execution Checks".
2. For each step in scope, find and read the corresponding detailed specification from "Rules > Subtask Map".
3. Collect and compile data following the specification and the "Data Collection & Compilation" rules in `equity-analysis-workflow/SKILL.md`.
4. Invoke the skill (if any) for the step with respect to the "Analysis & Output" rules in `equity-analysis-workflow/SKILL.md`.
5. Repeat steps 2–4 for each remaining step in scope.
