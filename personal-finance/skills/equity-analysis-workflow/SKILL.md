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

---

### Data Collection & Compilation

These rules apply to every phase and step.

#### Pre-fetch confirmation (QUESTION BEFORE DATA COLLECTION ‼️)

Before collecting any data, ask the user to confirm the method to collect.
Offer two options:

1. **Auto-fetch** — before fetching, check whether a cache file already exists at the path defined in `references/file-structure.md`. If it exists, read it and compare the `Fetched:` date against the TTL  of each piece of data. If the cache is still fresh, reuse it and skip the fetch. If stale or missing, proceed with fetching.
   
2. **Manual prompt** — compose a fetch prompt following the instruction in `references/manual-data-prompt.md`, using the data requirements for fields/sources and `references/data-cache-file-instruction.md` for the expected output structure. Return the prompt in a code block so the user can copy-paste it into their own tools.

#### Cache data TTL rules

Whenever looking up cache data, you must respect the "time-to-live" (TTL) for each type of data. If the current time has passed the TTL of the piece of data, you must acquire fresh data instead.

Read `references/data-ttl-guide.md` for TTL tiers, field-level lookup tables, and partial-staleness handling rules. Apply that guide whenever evaluating cache freshness.

**_If you are not sure, always confirm with user._**

#### Self-cache data lookup

If the user confirms to reuse data when appropriate, always lookup self cache data for partially/fully reuse.

#### Cross-step data dependencies

Some fields in a step depend on cached output from a previous step (for token efficiency).
If the expected previous-step cache file is not found:
- Do **not** silently skip or blindly re-fetch
- Ask the user: was the previous step intentionally skipped, or should you re-fetch the missing data?
- Proceed only after the user confirms

#### Related data lookup

Always actively lookup peers' data to save data fetching effort by reusing cached data. For example, to find related cached data, you can:
- lookup peers' data folders 
- lookup the screening data folder

#### Fetch resilience (Auto-fetch mode)

- Give each individual fetch task a reasonable timeout; do not wait indefinitely
- If a fetch times out or fails, do **not** retry silently — surface the failure to the user
- Ask the user whether to: retry, fall back to an alternative source listed in the data requirements, or proceed with partial data

#### Data validation

Always validate the data integrity as a professional financial data analyst, to scan and detect any data discrepancy by:
- **comparing** with related data in **other steps** of the same phase
- **comparing** with related data **with peers'** data
- **comparing** with related data in a related screening (for example, same sector)
- always **confirming** with user about any question/suspicion of invalid data

#### Post-fetch/prompt: save the fetch instruction

After every data fetch — regardless of mode — **always save a record to the `.prompts/` folder** before proceeding:

- **Auto-fetch**: write the data-requirements fields and sources used (ticker, phase, step, field list, resolved source URLs) as a markdown file
- **Manual prompt**: write the raw composed prompt text (without the surrounding code-block fences)

In both cases:
1. Derive the save path from `references/file-structure.md` (`.prompts/` lives adjacent to `Data/` and `Scripts/` at each scope level)
2. Name the file: `{YYYY-MM-DD}-{phase}-{step}-fetch.prompt.md`
3. Write the file using the Write tool

**Skill invocation is unconditional.** Choosing Manual prompt does NOT mean skipping sub-skill invocation. It just controls how data is collected.

**Timing in "all at once" mode.** When Q5 = "all at once", there is no per-step pause. The phase instruction must surface this question during scope confirmation (before execution begins). If the phase instruction does not have an explicit Q6 or equivalent, ask it immediately after Q5, before emitting the confirmation line.

#### Post-fetch: write the cache file

After fetching data (whether via Auto-fetch or Manual prompt), **always write the result to a cache file** before proceeding to analysis:

1. Derive file structure from the data requirements following `references/data-cache-file-instruction.md`
2. Determine the file path from `references/file-structure.md` (e.g. `{YYYY-MM-DD}-top-down-{SECTOR}.data.md` under `/Equity-analyses/Screening/.data/` for a Phase 1 top-down screen)
3. Write the file using the Write tool — do not skip this step, even for one-off screens

This cache file is the single source of truth for downstream analysis and cross-step dependencies.

---

### Analysis & Output

#### Skill Invocation

Whenever a phase instruction file lists a skill to run — shown as `/namespace:name` — invoke it using the **Skill tool** with `skill: "namespace:name"` (drop the leading `/`). You are the orchestrator; do not ask the user to type the slash command themselves.

‼️ IMPORTANT: When you attempt to invoke the any of the skill and it is not found, ABORT the process and **ASK USER TO INSTALL AND ENABLE IT****. Refer to "Required plugins" section above for list of required plugins.

#### Mid-workflow re-entry

When the user resumes a workflow mid-way (e.g. "complete step 5", "continue from
step 3", "previous steps are done"), the following rules apply without exception:

##### Existing output files are inputs, not the workflow spec

Files produced by prior steps (reports, models, charts, data caches) tell you
what was already done. They do not contain the step specifications, output format
rules, file naming conventions, or quality checks for the remaining steps.
Always invoke the required skill(s) before reading any prior output.

##### Skill invocation is unconditional

The phrase "previous steps are complete" does not reduce or remove the obligation
to invoke the skill. Invoke first, then read prior outputs as source material.

##### Recognize the shortcut signal

If you find yourself reasoning "I can see what's needed from the existing files
so I'll skip the skill invocation" — that reasoning is the signal to stop and
invoke the skill before proceeding. If you are not sure, always CONFIRM with user.

##### Cross-step context still requires skill invocation

Even when prior outputs provide rich context (financial data, charts, research
docs), the skill defines how to interpret and use that context for the remaining
steps. Context richness is not a substitute for workflow specification.

#### Preferred Output format (IMPORTANT)

Unless user has specified, **use MARKDOWN (`.md`) format** for each output which is designed to be Word document (`.docx`) or PDF (`.pdf`) by its delegated skill. This intentionally OVERRIDES the original instructions in the delegated skills. This rule does NOT apply to spreadsheet files (e.g. Excel - `.xlsx`).

The followings must be noted:
- KEEP any spreadsheet file in its own format.
- SKIP any header/footer instruction
- SKIP any technical instruction about docx or pdf construction
- Consider any adaption required to output in markdown

#### Preferred report content formatting

When you write any report (excluding spreadsheet) output, the following must be noted:
- Do NOT prepend any page number to a heading. See following examples:
  - ❌ Wrong - "PAGE 1 — INVESTMENT SUMMARY"
  - ✅ Correct - "Section 1 - INVESTMENT SUMMARY"
- Use arabic numbers over romantic numbers:
  - ❌ Wrong - "SECTION II — COMPANY 101
  - ✅ Correct - "SECTION 2 — COMPANY 101
- Always include a table of content with clickable links to sections. It must include ALL the headings and sub-headings in a nested format.

#### Report section structure consistency

Before writing any report, scan existing reports of the same type in the same scope folder (per `references/file-structure.md`). For each match, extract top-level and second-level headings only — skip full content. Ignore `_archived/` folders.

- **Two or more found:** use the heading structure that appears in the majority as the standard.
- **One found:** treat it as the provisional standard.
- **None found:** note this explicitly and proceed freely — the new report's structure becomes the first baseline.

Surface the derived structure to the user as a brief outline and confirm before writing.

You may deviate from the standard only when content genuinely warrants it (e.g. a section irrelevant to a Defensive stock). Any deviation must be minimal, confirmed with the user, and noted in an HTML comment directly below the document title:

```
<!-- Structure note: omitted "X" — reason -->
```

**Do not treat** heading-label differences with the same semantic role as structural deviations.

#### Output Scripts storage and discovery

##### Save rule

After any step that produces a binary output (e.g. `.xlsx`, `.pptx`, `.docx`), save the generation script to the `Scripts/` folder adjacent to `Data/` using the naming convention in `references/file-structure.md`. Do **not** save scripts for markdown outputs — those are directly re-editable.

##### Use scripts for updating tasks

When you are asked to update an existing result that is not plain text/markdown file (e.g. docx, spreadsheet or image), you should find the corresponding script to update and re-generate the result.

#### Prevent stale data and outputs

When you are asked to update some existing **"numbers"**, make sure that is sync across all data, scripts and outputs.

#### Context window management

##### Warning upon 50% of context usage

After you finished the current task, if the current session already used more than 50% of context usage, raise this warning to the user and suggest starting the next task in another session, with a suggested prompt in codeblock for user to copy.

##### Auto-compact before next step

In a multi-step workflow, when the user has confirmed to proceed to next step after a step is completed, auto-compact the session before actually proceeding to next step.

---

## Tasks

Follow the procedures below to complete the task.

### 1. Identify the phase

Identify the phase that matches the user's intent.

| Phase | Purpose | Instruction file |
|-------|---------|-----------------|
| 1 — Screening & Idea Generation | Top of funnel. Start here when you don't have a specific name yet. | `references/phase-1-screening.md` |
| 2 — Initiation Coverage | Sequential workflow that builds conviction on a specific stock. | `references/phase-2-initiation-coverage.md` |
| 3 — Thesis Documentation | Lock the investment thesis in writing before buying. | `references/phase-3-thesis.md` |
| 4 — Ongoing Review | Monitoring cadence for open positions (pre/post-earnings, between, annual). | `references/phase-4-ongoing-review.md` |

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
