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

A personal investing skill that wraps Anthropic's `equity-research:*` and `financial-analysis:*` skills with a workflow of opinionated preferences and addons.

---

## Rules (MUST READ FIRST‼️)

Read the following sections before start working on the tasks.

### Required plugins

The following plugins are required to be enabled:

- Marketplace `anthropics/financial-services-plugins`
  - `equity-research`
  - `financial-analysis`

### Investor style

This is a buy-and-hold, core-satellite style investor, with **2–10+ year horizon**.

### Portfolio Philosophy

Before any analysis, classify the equity. The type determines what you're optimizing for and
which metrics matter most.

| Type | Goal | Nature |
|------|------|--------|
| **Defensive** | Cash parking with yield above bonds | Low volatility, high income, defensive sector |
| **Core** | Stable, long-term wealth accumulation | Medium volatility, strong moat, sustainable growth, slightly outperforms benchmark |
| **Satellite** | Substantial outperformance, concentrated bet | High volatility, exploding growth, disruptive, may be unprofitable |

Confirm the equity type with the user before starting Phase 2 or later. Phase 1 (Screening) is type-agnostic — equity type is not yet determined.

---

### File Structure

**Always confirm equity type and lifecycle stage with the user before creating any files.**
**Read** `references/file-structure.md` for the full tree and lifecycle transition rules.

**Ignore** any `/_archived/` folder.

**Confirm the THEME name with the user, when it comes to creating watchlist items.

### Phase Specification Structure

#### Phase instruction entry point

Each phase contains an `instruction.md` file which is the entry point of the phase.

#### Phase subtask map and standard specification files

Each phase can contain a single task or multiple subtasks. There could be an instruction or mapping table which guides you how to find the corresponding path of task/subtask specification.

In either cases (of single task or multiple subtasks), there will be certain specification files for the task, depending on the needs. Here is a list of standard specification files you might find in the subtask:

| File | When to read (if not specifically instructed) |
|---|---|
| `subtask-instruction.md` | When it exists: read for step-specific instructions, including content preferences (additional sections, analysis focus) and format preferences (output template, layout, style). |
| `data-requirements.md` | When it exists: read for field definitions, TTL / refresh policy, fetch sources, and fetch prompts. Write cache file output following `references/data-cache-file-instruction.md`. |

*IMPORTANT NOTE:* depending on each subtask, the use of each file can be instructed to use in another way different from above use cases. Use this table as a baseline and follow the specific instructions (if any).

---

### Data Collection & Compilation

These rules apply to every phase and step.

#### Pre-fetch confirmation (QUESTION BEFORE DATA COLLECTION ‼️)

Before collecting any data, ask the user to confirm the method to collect.
Offer two options:

1. **Auto-fetch** — before fetching, check whether a cache file already exists at the path defined in `references/file-structure.md`. If it exists, read it and compare the `Fetched:` date against the TTL in the data requirements. If the cache is still fresh, reuse it and skip the fetch. If stale or missing, proceed with fetching.
   
2. **Manual prompt** — compose a fetch prompt following the structure in `references/manual-data-prompt-template.md`, using the data requirements for fields/sources and `references/data-cache-file-instruction.md` for the expected output structure. Return the prompt in a code block so the user can copy-paste it into their own tools.

**Skill invocation is unconditional.** Choosing Manual prompt does NOT mean skipping sub-skill invocation. It just controls how data is collected.

**Timing in "all at once" mode.** When Q5 = "all at once", there is no per-step pause. The phase instruction must surface this question during scope confirmation (before execution begins). If the phase instruction does not have an explicit Q6 or equivalent, ask it immediately after Q5, before emitting the confirmation line.

#### Post-fetch: write the cache file

After fetching data (whether via Auto-fetch or Manual prompt), **always write the result to a cache file** before proceeding to analysis:

1. Derive file structure from the data requirements following `references/data-cache-file-instruction.md`
2. Determine the file path from `references/file-structure.md` (e.g. `{YYYY-MM-DD}-top-down-{SECTOR}.md` under `/Equity-analyses/Screening/Data/` for a Phase 1 top-down screen)
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
- Ask the user whether to: retry, fall back to an alternative source listed in the data requirements, or proceed with partial data

---

### Analysis & Output

#### Skill Invocation

Whenever a phase instruction file lists a skill to run — shown as `/namespace:name` — invoke it using the **Skill tool** with `skill: "namespace:name"` (drop the leading `/`). You are the orchestrator; do not ask the user to type the slash command themselves.

‼️ IMPORTANT: When you attempt to invoke the any of the skill and it is not found, ABORT the process and **ASK USER TO INSTALL AND ENABLE IT****. Refer to "Required plugins" section above for list of required plugins.

#### Preferred Output format (IMPORTANT)

Unless user has specified, **use MARKDOWN (`.md`) format** for each output which is designed to be Word document (`.docx`) or PDF (`.pdf`) by its delegated skill. This intentionally OVERRIDES the original instructions in the delegated skills. This rule does NOT apply to spreadsheet files (e.g. Excel - `.xlsx`).

The followings must be noted:
- KEEP any spreadsheet file in its own format.
- SKIP any header/footer instruction
- SKIP any technical instruction about docx or pdf construction
- Consider any adaption required to output in markdown

#### Output Scripts storage and discovery

##### Save rule

After any step that produces a binary output (e.g. `.xlsx`, `.pptx`, `.docx`), save the generation script to the `Scripts/` folder adjacent to `Data/` using the naming convention in `references/file-structure.md`. Do **not** save scripts for markdown outputs — those are directly re-editable.

##### Discovery rule

Before starting any step where the user's intent is a formatting or structural update (not a data refresh), check the `Scripts/` folder first:

1. **Script found** → present the "script-only update" path: modify only the relevant section of the script, re-run it, and skip data re-fetch entirely.
2. **No script found** → generate the output normally and save the script as part of that run.

##### Trigger signals for the script-only path

Route to the script-only path when the user says things like:
- "update formatting", "fix the chart", "change the layout", "tweak the template", "small update to [output file]"

And **all** of the following are true:
- No new earnings data has been released
- No thesis change has been requested
- No data staleness concern has been raised

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

**Reference: Rhythm at a Glance**

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

**Follow the phase instruction file** identified in Task 1, with following considerations in mind (IMPORTANT):
- **When you collect/compile data**: read through and follow "Rules > Data Collection & Compilation".
- **When you invoke delegated skill(s) to analyze and output**: read through and follow "Rules > Analysis & Output".
- Override any **file structure** instruction from the delegated skill, by the "File Structure" rules.
