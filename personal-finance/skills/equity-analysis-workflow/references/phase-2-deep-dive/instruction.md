# Phase 2 — Deep Dive (Initiation)

## Rules (READ FIRST)

### Objective

For any stock that clears screening, this phase builds conviction. It runs as a **sequential workflow**.

### Task Map

| Step | Task | Type | Instruction |
|---|---|---|---|
| 1 | Financial Model | Data collection & compilation only | Collect data according to specification. |
| 2 | Company Research | Data collection & compilation only | Collect data according to specification. |
| 3 | Valuation (DCF) | Data collection & compilation + analysis | Collect data according to specification, then invoke skill `financial-analysis:dcf`. |
| 4 | Competitive Analysis | Data collection & compilation + analysis | Collect data according to specification, then invoke skill `financial-analysis:competitive-analysis`. |
| 5 | Report Generation | Data collection & compilation + analysis | Collect data according to specification, then invoke skill `equity-research:initiating-coverage`. |

### Detailed Specification Map

| Step | Task | Detailed specification |
|---|---|---|
| 1 | Financial Model | `step-1-financial-model/` |
| 2 | Company Research | `step-2-company-research/` |
| 3 | DCF | `step-3-dcf/` |
| 4 | Competitive Analysis | `step-4-competitive-analysis/` |
| 5 | Report Generation | `step-5-report-generation/` |

### Pre-execution Checks

| Step | Title | When to ask |
|---|---|---|
| 1 | Equity type | Always, unless context is "update" |
| 2 | Lifecycle stage | Always, unless context is "update" |
| 3 | Pre-question folder check | Always — run before presenting step 4 |
| 4 | Report and data mode | Always |
| 5 | Scope | Always |
| 6 | Execution cadence | Always |
| 7 | Data collection mode | Only when at least one fetch will occur |
| 8 | Confirmation | Always — after step 7 (or step 6 if step 7 is skipped) |

#### 1. Equity type

Ask if context is not "update":

- Defensive / Core / Satellite

This determines the folder path for all outputs.

#### 2. Lifecycle stage

Ask if context is not "update":

- Watchlist (not yet held), Screening (still evaluating) or Holding already

This determines the folder path for all outputs.

#### 3. Pre-question folder check

Before presenting step 4, check:
- Whether `/{Type}/{Stage}/{TICKER}/Initiation/` contains any `*-initiation-report/` subfolders
- If yes: the most recent one's name and date
- Which `Data/` cache files exist and whether each is within TTL (compare `Fetched:` date in the file against today's date)

Surface as a one-line summary, for example:
> Found: `/CRWD/Initiation/2026-03-16-initiation-report/`. Data caches: `2026-03-16-company-research.md` (1 day old ✓ within 1yr TTL), `2026-03-16-peer-data.md` (1 day old ✗ exceeds 1d TTL).

If no initiation folder exists, say so and note that options 2 and 3 in step 4 behave identically to 1 and 4 respectively.

#### 4. Report and data mode

Present options; wait for answer before showing step 5:

1. **New report, reuse data** — create new `{today}-initiation-report/`; reuse Data/ caches within TTL per step *(recommended when an initiation folder exists but today is a different date)*
2. **Update existing report, reuse data** — write into the most recent existing folder; reuse Data/ caches within TTL *(recommended when the most recent folder is already dated today)*
3. **Update existing report, fresh data** — write into most recent folder; re-fetch all data regardless of TTL
4. **New report, fresh data** — create new folder and re-fetch all data *(use only when a clean slate is explicitly needed)*

#### 5. Scope

**For mode 1 or 4 (new report context):**

1. Full report — all steps *(default if user replies without selecting)*
2. Skip DCF and valuation — Steps 1–2 → Step 4 → Step 5; no `dcf-model.xlsx`
3. Skip competitive analysis — Steps 1–3 → Step 5; no `competitive-analysis.pptx`; Step 5 omits comp sections
4. Skip financial model — all steps but no Excel outputs (`financial-model.xlsx`, `dcf-model.xlsx`)
5. Research and thesis only — Steps 1–2 → Step 5 (narrative only); no Excel, no DCF, no comps. Step 1 fetches data only — no Excel output generated.

Options are independently combinable except option 5, which supersedes all others.

**For mode 2 or 3 (update context):**

1. Full report — re-run all steps *(default)*
2. Selective — name the step(s) to re-run; all others reuse existing outputs as-is. Valid options: Step 1, Step 2, Step 3, Step 4, Step 5, or any combination.

**Branching table:**

| Mode | Scope | Folder | Data caches | Steps run | Outputs reused vs. generated | Report sections |
|---|---|---|---|---|---|---|
| 1 (new, reuse) | 1 (full) | New `{today}-initiation-report/` | Check TTL per step; reuse if fresh | 1→2→3→4→5 | All generated fresh | All |
| 1 (new, reuse) | 2 (skip DCF) | New folder | Check TTL steps 1, 2, 4 | 1→2→4→5 | No dcf-model.xlsx | Omit valuation section |
| 1 (new, reuse) | 3 (skip comp) | New folder | Check TTL steps 1, 2, 3 | 1→2→3→5 | No competitive-analysis.pptx | Omit positioning map, dim scoring, TAM split |
| 1 (new, reuse) | 4 (skip fin model) | New folder | Check TTL steps 1, 3, 4 | 1→2→3→4→5 | No .xlsx outputs | All narrative; no Excel |
| 1 (new, reuse) | 5 (research + thesis) | New folder | Check TTL steps 1, 2 | 1→2→5 | No Excel, no DCF, no comps | Steps 1–2 + Step 5 thesis narrative only |
| 2 (update, reuse) | 1 (full) | Most recent existing folder | Check TTL per step | 1→2→3→4→5 | Overwrite changed files | All |
| 2 (update, reuse) | 2 (selective) | Most recent existing folder | Re-fetch for selected steps only | Named steps only | Unselected steps: reuse existing outputs | As applicable |
| 3 (update, fresh) | 1 (full) | Most recent existing folder | Re-fetch all | 1→2→3→4→5 | All overwritten | All |
| 3 (update, fresh) | 2 (selective) | Most recent existing folder | Re-fetch for selected steps only | Named steps only | Unselected steps: reuse existing outputs | As applicable |
| 4 (new, fresh) | 1 (full) | New `{today}-initiation-report/` | Re-fetch all | 1→2→3→4→5 | All generated fresh | All |
| 4 (new, fresh) | 2 (skip DCF) | New folder | Re-fetch steps 1, 2, 4 | 1→2→4→5 | No dcf-model.xlsx | Omit valuation |
| 4 (new, fresh) | 3 (skip comp) | New folder | Re-fetch steps 1, 2, 3 | 1→2→3→5 | No competitive-analysis.pptx | Omit comp sections |
| 4 (new, fresh) | 4 (skip fin model) | New folder | Re-fetch steps 1, 3, 4 | 1→2→3→4→5 | No .xlsx | All narrative |
| 4 (new, fresh) | 5 (research + thesis) | New folder | Re-fetch steps 1, 2 | 1→2→5 | No Excel, no DCF, no comps | Steps 1–2 + Step 5 narrative |

#### 6. Execution cadence

- **Step-by-step** — pause for review after each step before proceeding to the next
- **All at once** — run all selected steps without pausing *(default)*

#### 7. Data collection mode

Ask only when at least one fetch will occur:

- **Mode 3 or 4**: always ask (fresh data required for all relevant steps).
- **Mode 1 or 2**: ask only if the pre-question folder check found any stale or missing cache files for the steps that will run. If ALL relevant caches are fresh, skip — no fetch will occur.

When applicable, ask:

> How should data be collected?
> See SKILL.md › Data Handling › Pre-fetch confirmation for the options.

Wait for the user's answer before emitting the confirmation line.

#### 8. Confirmation

Emit one line and proceed immediately:

> Running: [step list with data handling per step]. Data collection: [Data fetch mode, Cache mode]. Writing into `/{TICKER}/Initiation/{YYYY-MM-DD}-initiation-report/`.

MUST respect [SKILL.md](../../SKILL.md) for any other question required before starting.

---

## Tasks

1. Run "Rules > Pre-execution Checks".
2. According to user-selected scope, find tasks in "## Rules (READ FIRST)"
3. Run tasks in the corresponding order. For each tasks:
   1. Find and read the corresponding detailed specification from "Rules > Detailed specification"
   2. Follow the **"Instruction" in "Task Map"** for the corresponding task.