# Phase 4 — Ongoing Review

## Rules (READ FIRST)

### Objective

Once a position is open (folder moves to `/Holding/`), shift to a monitoring cadence. Select the review type that matches the current situation.

### Review Type Map

| Review Type | Description | Skill(s) |
|---|---|---|
| **Pre-Earnings** | Preview upcoming earnings with scenarios | `equity-research:earnings-preview` |
| **Post-Earnings** | Beat/miss analysis → model update → thesis reaffirmation (sequential) | `equity-research:earnings` → `equity-research:model-update` → `equity-research:thesis` |
| **Between Earnings** | Lightweight monitoring; two independent options — ask which to run | `equity-research:morning-note` or `equity-research:catalysts` |
| **Annual Review** | Reaffirm or close each position | `equity-research:thesis` |

### Review Type Triggers

Use these to determine the appropriate review type when initiating Phase 4:

| Review Type | Trigger |
|---|---|
| **Pre-Earnings** | Earnings date is within the upcoming 1–2 weeks |
| **Post-Earnings** | Company has reported results this period |
| **Annual Review** | 12 months have passed since initiation or last annual review |
| **Between Earnings** (competitive focus) | Named competitor announces M&A or major product expansion (any such announcement) |
| **Between Earnings** (valuation focus) | Peer group NTM multiple spread widens or narrows >20% in EV/NTM Rev since initiation |
| **Between Earnings** (fundamental focus) | NRR or gross retention moves >5 percentage points since initiation |

Between-earnings triggers do not replace post-earnings or annual review procedures.

### Detailed Specification Map

| Review Type | Detailed specification |
|---|---|
| Pre-Earnings | `pre-earnings/` |
| Post-Earnings Step 1: Earnings Analysis | `post-earnings-step-1-earnings/` |
| Post-Earnings Step 2: Model Update | `post-earnings-step-2-model-update/` |
| Post-Earnings Step 3: Thesis Update | `post-earnings-step-3-thesis/` |
| Between Earnings | `between-earnings/` |
| Annual Review | `annual-review/` |

## Tasks

1. Ask the user which review type applies (Pre-Earnings, Post-Earnings, Between Earnings, or Annual Review). If user hasn't provided initially, suggest the review type according to "Review Type Triggers", then confirm with user.
2. Confirm with user if necessary:
    - For **Post-Earnings**: confirm whether to run all steps sequentially or step-by-step with pauses.
    - For **Between Earnings**: confirm which option to run.
3. Find and read the detailed specification(s) from "Rules > Detailed Specification Map".
4. Collect and compile data as instructed in the spec.
5. Invoke the skill(s) in the order specified by the Review Type Map.
