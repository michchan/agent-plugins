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

## Rules (MUST READ FIRST‼️)

Read the following sections before start working on the tasks.

### Portfolio Philosophy

Before any analysis, classify the equity. The type determines what you're optimizing for and
which metrics matter most.

| Type | Goal | Nature |
|------|------|--------|
| **Defensive** | Cash parking with yield above bonds | Low volatility, high income, defensive sector |
| **Core** | Stable, long-term wealth accumulation | Medium volatility, strong moat, sustainable growth, slightly outperforms benchmark |
| **Satellite** | Substantial outperformance, concentrated bet | High volatility, exploding growth, disruptive, may be unprofitable |

Confirm the equity type with the user before starting Phase 2 or later. Phase 1 (Screening) is type-agnostic — equity type is not yet determined.

### Folder Structure

**Always confirm equity type and lifecycle stage with the user before creating any files.**
**Read** `references/folder-structure.md` for the full tree and lifecycle transition rules.

**Ignore** any `/_archived/` folder.

### Data Handling

These rules apply to every phase and step.

#### Locating reference files

Each phase instruction file (`instruction.md`) contains a **Detailed Instruction Map** table.
That table maps each step to a subdirectory (e.g. `step-1-company-research/`).
Each subdirectory contains three files:

| File | When to read |
|---|---|
| `data-requirements.md` | When you need to know what data fields are required, or what the cache TTL / refresh policy is |
| `data-file-template.md` | When you need to read or write the data cache file; also use as the structure reference when the user provides data from an external source |
| `data-fetch-protocol.md` | When you need to fetch data from external sources; always follow the field list in `data-requirements.md` and write output in the shape of `data-file-template.md` |

#### Pre-fetch confirmation (QUESTION BEFORE DATA FETCHING ‼️)

Before fetching any data, ask the user to confirm the fetch.
Offer two options:

1. **Auto-fetch** — before fetching, check whether a cache file already exists at the path defined in `references/folder-structure.md`. If it exists, read it and compare the `Fetched:` date against the TTL in `data-requirements.md`. If the cache is still fresh, reuse it and skip the fetch. If stale or missing, proceed with fetching.
2. **Manual prompt** — compose a fetch prompt following the structure in `references/manual-data-prompt-template.md`, using `data-requirements.md` for fields/sources and `data-file-template.md` for the expected output structure. Return the prompt in a code block so the user can copy-paste it into their own tools.

**Skill invocation is unconditional.** Choosing Manual prompt does NOT mean skipping sub-skill invocation. It just controls how data is collected.

**Timing in "all at once" mode.** When Q5 = "all at once", there is no per-step pause. The phase instruction must surface this question during scope confirmation (before execution begins). If the phase instruction does not have an explicit Q6 or equivalent, ask it immediately after Q5, before emitting the confirmation line.

#### Post-fetch: write the cache file

After fetching data (whether via Auto-fetch or Manual prompt), **always write the result to a cache file** before proceeding to analysis:

1. Use `data-file-template.md` as the file structure — fill every section with the fetched data
2. Determine the file path from `references/folder-structure.md` (e.g. `{YYYY-MM-DD}-top-down-{SECTOR}.md` under `/Equity-analyses/Screening/Data/` for a Phase 1 top-down screen)
3. Write the file using the Write tool — do not skip this step, even for one-off screens

This cache file is the single source of truth for downstream analysis and cross-step dependencies.

#### Cross-step data dependencies

Some fields in a step's data file depend on cached output from a previous step (for token efficiency).
If the expected previous-step cache file is not found:
- Do **not** silently skip or blindly re-fetch
- Ask the user: was the previous step intentionally skipped, or should you re-fetch the missing data?
- Proceed only after the user confirms

#### Fetch resilience

- Give each individual fetch task a reasonable timeout; do not wait indefinitely
- If a fetch times out or fails, do **not** retry silently — surface the failure to the user
- Ask the user whether to: retry, fall back to an alternative source listed in `data-fetch-protocol.md`, or proceed with partial data

### Skill Invocation

Whenever a phase instruction file lists a skill to run — shown as `/namespace:name` — invoke it using the **Skill tool** with `skill: "namespace:name"` (drop the leading `/`). You are the orchestrator; do not ask the user to type the slash command themselves.

---

## Tasks

Follow the procedures below to complete the task.

### 1. Identify the phase

Identify the phase that matches the user's intent.

| Phase | Purpose | Instruction file |
|-------|---------|-----------------|
| 1 — Screening & Idea Generation | Top of funnel. Start here when you don't have a specific name yet. | `references/phase-1-screening/instruction.md` |
| 2 — Deep Dive (Initiation) | Sequential workflow that builds conviction on a specific stock. | `references/phase-2-deep-dive/instruction.md` |
| 3 — Thesis Documentation | Lock the investment thesis in writing before buying. | `references/phase-3-thesis/instruction.md` |
| 4 — Ongoing Review | Monitoring cadence for open positions (pre/post-earnings, between, annual). | `references/phase-4-ongoing-review/instruction.md` |

**Rhythm at a Glance**

```
QUARTERLY
  Pre-earnings   →  Phase 4 (pre-earnings)
  Post-earnings  →  Phase 4 (post-earnings: earnings → model update → thesis update)

ONGOING / AD-HOC
  New idea       →  Phase 1 → Phase 2 → Phase 3

ANNUAL
  Full review    →  Phase 4 (annual review)
```

### 2. Execute the phase

Follow these steps in order:

1. **Read the phase instruction file** identified in Task 1 before doing anything else.
2. **Collect data** following Rules > Data Handling.
3. **Invoke delegated skills** per Rules > Skill Invocation.
