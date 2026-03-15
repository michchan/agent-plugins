# Phase 5 — Ongoing Review

Once a position is open (folder moves to `/Holding/`), shift to monitoring cadence.

Ask the user which review type applies before proceeding:

- **Pre-Earnings**: Invoke skill `equity-research:earnings-preview`
- **Post-Earnings**: three steps in sequence — ask to run step by step or all at once:
  1. Invoke skill `equity-research:earnings` — beat/miss analysis, thesis check
  2. Invoke skill `equity-research:model-update` — update actuals, revise forward estimates
  3. Invoke skill `equity-research:thesis` — update or reaffirm
- **Between Earnings** (lightweight): two independent options — ask which to run:
  - Invoke skill `equity-research:morning-note` — macro + portfolio-level developments
  - Invoke skill `equity-research:catalysts` — upcoming events across full portfolio
- **Annual Review**: Invoke skill `equity-research:thesis` — reaffirm or close each position

## Detailed Instruction Map

| Task | Instructions |
|---|---|
| Pre-Earnings | `pre-earnings/` |
| Post-Earnings Step 1: Earnings Analysis | `post-earnings-step-1-earnings/` |
| Post-Earnings Step 2: Model Update | `post-earnings-step-2-model-update/` |
| Post-Earnings Step 3: Thesis Update | `post-earnings-step-3-thesis/` |
| Between Earnings | `between-earnings/` |
| Annual Review | `annual-review/` |
