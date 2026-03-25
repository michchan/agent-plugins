# Phase 1 — Screening & Idea Generation

## Rules (READ FIRST)

### Objective

The top of the funnel. Start here when the user doesn't have a specific name yet.

### Subtask Map

Policy: run one of the following. If not specified, ask the user before proceeding.

| Approach | Description | Skill to invoke |
|---|---|---|
| **Top-down** (macro → sector → names) | Sector overview, then drill into names | `equity-research:sector-overview` |
| **Bottom-up** (criteria → names) | Screen with user's criteria | `equity-research:idea-generation` |
| **Event-driven** (catalyst → entry point) | Upcoming events across watchlist or sector | `equity-research:catalyst-calendar` |

---

## Tasks

1. Select the approach from the "Subtask Map". If not clear from context, ask the user before proceeding.

2. Load the corresponding skill from the "Subtask Map", with the following custom rules:
   - Follow data requirements from the skill; collect and compile data following the "Data Collection & Compilation" rules in `equity-analysis-workflow/SKILL.md`.
   - Respect the "Analysis & Output" rules in `equity-analysis-workflow/SKILL.md`.
