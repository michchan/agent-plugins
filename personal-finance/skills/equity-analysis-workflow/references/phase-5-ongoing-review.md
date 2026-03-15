# Phase 5 — Ongoing Review

Once a position is open (folder moves to `/Holding/`), shift to monitoring cadence.

## Pre-Earnings
Invoke skill `equity-research:earnings-preview` — model bull/base/bear scenarios. Define what would
constitute a beat, miss, or thesis-confirming quarter.

## Post-Earnings
1. Invoke skill `equity-research:earnings` — beat/miss analysis, thesis check
2. Invoke skill `equity-research:model-update` — update actuals, revise forward estimates
3. Invoke skill `equity-research:thesis` — update or reaffirm; never let it go stale

## Between Earnings (lightweight)
- Invoke skill `equity-research:morning-note` — macro + portfolio-level developments
- Invoke skill `equity-research:catalysts` — upcoming events across full portfolio

## Annual Review
Invoke skill `equity-research:thesis` — reaffirm or close each position
