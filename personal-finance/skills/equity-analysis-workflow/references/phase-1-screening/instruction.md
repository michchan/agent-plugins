# Phase 1 — Screening & Idea Generation

## Rules (READ FIRST)

### Objective

The top of the funnel. Start here when user don't have a specific name yet.

### Subtask Map

Policy: run either one of the tasks.

| Task | Description | Skill to invoke | Specification path |
|---|---|---|---|
| **Top-down** (macro → sector → names) | Sector overview, then drill into names | `equity-research:sector-overview` | `top-down/` |
| **Bottom-up** (criteria → names) | Screen with user's criteria | `equity-research:idea-generation` | `bottom-up/` |
| **Event-driven** (catalyst → entry point) | Upcoming events across watchlist or sector | `equity-research:catalyst-calendar` |`event-driven/` |

---

## Tasks

1. Select the approach from the "Subtask Map".
2. Find and read the corresponding standard specification files.
3. Collect and compile data following the specification and with respect to the "Data Collection & Compilation" rules.
4. Invoke the delegated skill to analyze and output the report with respect to the "Analysis & Output" rules.