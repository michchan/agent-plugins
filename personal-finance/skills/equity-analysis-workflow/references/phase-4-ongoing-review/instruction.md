# Phase 4 — Ongoing Review

## Rules (READ FIRST)

### Objective

Once a position is open (folder moves to `/Holding/`), shift to a monitoring cadence. Select the review type that matches the current situation.

### Review Type Map

Policy: select the review type that matches the trigger.

| Review Type | Trigger | Skill(s) |
|---|---|---|
| **Pre-Earnings** | Earnings date within 1–2 weeks | `equity-research:earnings-preview` |
| **Post-Earnings** | Company has reported results this period | In this order: `equity-research:earnings` → `equity-research:model-update` → `equity-research:thesis-tracker` |
| **Between Earnings** | Competitor M&A/major expansion; or peer NTM multiple spread widens/narrows >20% in EV/NTM Rev; or NRR/gross retention moves >5 pp | `equity-research:morning-note` or `equity-research:catalyst-calendar` |
| **Annual Review** | 12 months since initiation or last annual review | `equity-research:thesis-tracker` |

Between-earnings triggers do not replace post-earnings or annual review procedures.

---

## Tasks

1. Identify the review type: ask user; suggest based on "Review Type Map" triggers; confirm.
2. Confirm additional options with user if applicable:
   - **Post-Earnings**: run all steps sequentially or step-by-step with pauses?
   - **Between Earnings**: which skill option to run?
3. Invoke the skill(s) in the order specified by the Review Type Map, with the following custom rules:
   - Follow data requirements from the skill; collect and compile data following the "Data Collection & Compilation" rules in `equity-analysis-workflow/SKILL.md`.
   - Respect the "Analysis & Output" rules in `equity-analysis-workflow/SKILL.md`.
