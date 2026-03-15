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

## Workflow Map

### The 5 Phases

| Phase | Purpose | Primary skills |
|-------|---------|---------------|
| 1 — Screening & Idea Generation | Top of funnel | `equity-research:screen`, `equity-research:sector`, `equity-research:catalysts` |
| 2 — Deep Dive (Initiation) | Build conviction | `equity-research:initiating-coverage`, `financial-analysis:dcf`, `financial-analysis:comps`, `financial-analysis:competitive-analysis` |
| 3 — Comparison & Relative Value | Sanity-check vs. peers | `financial-analysis:comps`, `financial-analysis:competitive-analysis` |
| 4 — Thesis Documentation | Lock the thesis before buying | `equity-research:thesis` |
| 5 — Ongoing Review | Monitor open positions | `equity-research:earnings-preview`, `equity-research:earnings`, `equity-research:model-update`, `equity-research:thesis`, `equity-research:catalysts` |

### Rhythm at a Glance

```
QUARTERLY
  Pre-earnings   →  equity-research:earnings-preview  (bull/base/bear scenarios)
  Post-earnings  →  equity-research:earnings  →  equity-research:model-update  →  equity-research:thesis (update)

ONGOING / AD-HOC
  New idea       →  screen → sector → [initiate: Phase 2] → thesis

ANNUAL
  Full review    →  equity-research:thesis (reaffirm or close each position)
```

---

## Token Optimization Rules

**These rules apply to every phase. Read them once; inherit them everywhere.**

### Rule 1 — Fetch Once, Pass Forward (highest impact)
When executing Phase 2, **Task 0 (Data Fetch pre-step) must run first** and save all company data
to `{TICKER}-data.md` in the equity folder. Tasks 1–5 **read that file** rather than re-fetching.

> Do not re-fetch a section if its `Fetched:` date is within the threshold in
> `references/data-fetch-protocol.md`. Stock price and consensus estimates are never
> cached — always fetch fresh.

### Rule 2 — Targeted WebFetch Prompts
Every WebFetch call must include a tight `prompt` parameter. Examples:

- Financials: `"Extract: revenue, operating income, net income, FCF, total debt, cash for last 4 fiscal years only. No prose."`
- Business description: `"Extract: business segments, revenue by segment, key products, pricing model, major customers. Under 400 words."`
- Risk factors: `"List top 10 risk factors as bullet points only. No headers, no sub-bullets."`
- Management: `"Extract: CEO name and tenure, CFO name and tenure. Under 150 words."`

### Rule 3 — EDGAR-First for Financials
For any public company, use SEC EDGAR structured endpoints before IR pages or news:

1. EDGAR filing index → get 10-K URL
2. Fetch 10-K with targeted financial prompt
3. Fall back to company IR page only for segment/KPI data not in EDGAR
4. Fall back to Yahoo Finance only for stock price and consensus estimates

See `references/data-fetch-protocol.md` for exact URLs and prompt strings.

---

## Sub-Skill Invocation

Whenever this workflow instructs you to run a skill — shown as `/namespace:name` — invoke it using the **Skill tool** with `skill: "namespace:name"` (drop the leading `/`). You are the orchestrator; do not ask the user to type the slash command themselves.

---

## Phase 1 — Screening & Idea Generation

Top of funnel. Start here when you don't have a specific name yet.
**Read** `references/phase-1-screening.md` before starting this phase.

---

## Phase 2 — Deep Dive (Initiation)

Sequential workflow that builds conviction on a specific stock.
**Read** `references/phase-2-deep-dive.md` before starting this phase.

---

## Phase 3 — Comparison & Relative Value

Validate the stock against peers before committing capital.
**Read** `references/phase-3-comparison.md` before starting this phase.

---

## Phase 4 — Thesis Documentation

Lock the investment thesis in writing before buying.
**Read** `references/phase-4-thesis.md` before starting this phase.

---

## Phase 5 — Ongoing Review

Monitoring cadence for open positions (pre/post-earnings, between, annual).
**Read** `references/phase-5-ongoing-review.md` before starting this phase.

---

## Folder Structure

**Always confirm equity type and lifecycle stage with the user before creating any files.**
**Read** `references/folder-structure.md` for the full tree and lifecycle transition rules.
