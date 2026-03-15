---
name: equity-analysis-workflow
description: >
  Personal buy-and-hold investor equity analysis workflow. Triggers when the user wants to:
  research a stock to buy, screen for investment ideas, initiate coverage on a new name,
  write or update an investment thesis, prepare for earnings, review a portfolio position,
  or decide whether a stock fits as Defensive / Core / Satellite. Wraps equity-research:*
  and financial-analysis:* skills with a personal investor lens and token-efficient data fetching.
---

# Equity Analysis Workflow

A personal investing skill for a buy-and-hold, core-satellite style investor (2–10 year horizon).
Wraps Anthropic's `equity-research:*` and `financial-analysis:*` skills with opinionated defaults.

---

## Portfolio Philosophy

Before any analysis, classify the equity. The type determines what you're optimizing for and
which metrics matter most.

| Type | Goal | Nature |
|------|------|--------|
| **Defensive** | Cash parking with yield above bonds | Low volatility, high income, defensive sector |
| **Core** | Stable, long-term wealth accumulation | Medium volatility, strong moat, sustainable growth, slightly outperforms benchmark |
| **Satellite** | Substantial outperformance, concentrated bet | High volatility, exploding growth, disruptive, may be unprofitable |

Confirm the equity type with the user before starting any phase.

---

## Sub-Skill Invocation

Whenever this workflow instructs you to run a skill — shown as `/namespace:name` — invoke it using the **Skill tool** with `skill: "namespace:name"` (drop the leading `/`). You are the orchestrator; do not ask the user to type the slash command themselves.

---

## Folder Structure

**Always confirm equity type and lifecycle stage with the user before creating any files.**
**Read** `references/folder-structure.md` for the full tree and lifecycle transition rules.

---

## Workflow Map

### The 5 Phases

| Phase | Purpose | Instructions |
|-------|---------|-------------|
| 1 — Screening & Idea Generation | Top of funnel | Top of funnel. Start here when you don't have a specific name yet. **Read** `references/phase-1-screening/instruction.md` before starting this phase. |
| 2 — Deep Dive (Initiation) | Build conviction | Sequential workflow that builds conviction on a specific stock. **Read** `references/phase-2-deep-dive/instruction.md` before starting this phase. |
| 3 — Comparison & Relative Value | Sanity-check vs. peers | Validate the stock against peers before committing capital. **Read** `references/phase-3-comparison/instruction.md` before starting this phase. |
| 4 — Thesis Documentation | Lock the thesis before buying | Lock the investment thesis in writing before buying. **Read** `references/phase-4-thesis/instruction.md` before starting this phase. |
| 5 — Ongoing Review | Monitor open positions | Monitoring cadence for open positions (pre/post-earnings, between, annual). **Read** `references/phase-5-ongoing-review/instruction.md` before starting this phase. |

### Rhythm at a Glance

```
QUARTERLY
  Pre-earnings   →  Phase 5 (pre-earnings)
  Post-earnings  →  Phase 5 (post-earnings: earnings → model update → thesis update)

ONGOING / AD-HOC
  New idea       →  Phase 1 → Phase 2 → Phase 3 → Phase 4

ANNUAL
  Full review    →  Phase 5 (annual review)
```

---

## Data Handling

These rules apply to every phase and step.

### Locating reference files

Each phase instruction file (`instruction.md`) contains a **Detailed Instruction Map** table.
That table maps each step to a subdirectory (e.g. `step-1a-company-research/`).
Each subdirectory contains three files:

| File | When to read |
|---|---|
| `data-requirements.md` | When you need to know what data fields are required, or what the cache TTL / refresh policy is |
| `data-file-template.md` | When you need to read or write the data cache file; also use as the structure reference when the user provides data from an external source |
| `data-fetch-protocol.md` | When you need to fetch data from external sources; always follow the field list in `data-requirements.md` and write output in the shape of `data-file-template.md` |

### Pre-fetch confirmation

Before fetching any data, ask the user to confirm the fetch.
Offer two options:

1. **Auto-fetch** — proceed with fetching directly
2. **Manual prompt** — compose a fetch prompt following the structure in `references/manual-data-prompt-template.md`, using `data-requirements.md` for fields/sources and `data-file-template.md` for the expected output structure. Return the prompt in a code block so the user can copy-paste it into their own tools.

### Cross-step data dependencies

Some fields in a step's data file depend on cached output from a previous step (for token efficiency).
If the expected previous-step cache file is not found:
- Do **not** silently skip or blindly re-fetch
- Ask the user: was the previous step intentionally skipped, or should you re-fetch the missing data?
- Proceed only after the user confirms

### Fetch resilience

- Give each individual fetch task a reasonable timeout; do not wait indefinitely
- If a fetch times out or fails, do **not** retry silently — surface the failure to the user
- Ask the user whether to: retry, fall back to an alternative source listed in `data-fetch-protocol.md`, or proceed with partial data
