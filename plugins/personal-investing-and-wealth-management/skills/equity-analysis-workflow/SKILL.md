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

| Type | Goal | Nature | Key Evaluation Criteria |
|------|------|--------|------------------------|
| **Defensive** | Cash parking with yield above bonds | Low volatility, high income, defensive sector | Dividend yield >3%, beta <0.8, payout ratio sustainability, balance sheet strength. Sectors: utilities, consumer staples, healthcare |
| **Core** | Stable, long-term wealth accumulation | Medium volatility, strong moat, sustainable growth, slightly outperforms benchmark | Moat durability (brand/switching costs/network), 5-year FCF CAGR, valuation vs. intrinsic value. Revenue growth 8–15% |
| **Satellite** | Substantial outperformance, concentrated bet | High volatility, exploding growth, disruptive, may be unprofitable | TAM size and penetration rate, growth durability, unit economics trajectory, path to profitability. Revenue growth >20% or early-stage |

**Classification quick check — ask yourself:**
- Dividend yield >3% and beta <0.8? → Defensive
- Consistent profitable growth, strong FCF, durable competitive advantage? → Core
- Revenue growth >20%, large TAM, disruptive model, early-stage? → Satellite

If unsure, default to Core and revisit after the deep dive.

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
  Portfolio      →  wealth-management:rebalance + equity-research:catalysts

ANNUAL
  Tax review     →  wealth-management:tlh
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

## Phase 1 — Screening & Idea Generation

The top of the funnel. Start here when you don't have a specific name yet.

### Entry Points

**Top-down** (macro → sector → names)
```
/equity-research:sector
```
Get a sector overview first. Identify where you want exposure, then drill into individual names.
Good for building Defensive or Core positions where sector health matters.

**Bottom-up** (criteria → names)
```
/equity-research:screen
```
Run a screen with your criteria. For Defensive: dividend yield, payout ratio, beta, debt/equity.
For Core: FCF yield, ROIC, revenue growth consistency. For Satellite: revenue growth rate, TAM estimates.

**Event-driven** (catalyst → entry point)
```
/equity-research:catalysts
```
Check the catalyst calendar for upcoming events across your watchlist or a sector. Useful for
identifying asymmetric entry points before earnings, product launches, or regulatory decisions.

### Output
Save screening outputs to `/Equity-analyses/{Type}/Screening/`.

---

## Phase 2 — Deep Dive (Initiation)

For any stock that clears screening, this phase builds conviction. It runs as a **sequential workflow**
with a mandatory data-fetch pre-step to minimize token usage.

**Before starting: confirm with the user:**
1. Equity type (Defensive / Core / Satellite)
2. Lifecycle stage (Watchlist — not yet held, or Screening — still evaluating)

This determines the folder path for all outputs.

### Modified Initiation Workflow

| Step | Action | Token optimization |
|------|--------|--------------------|
| **0. Data Fetch** (mandatory pre-step) | Read `references/data-fetch-protocol.md`, fetch from EDGAR + targeted sources, save to `{TICKER}-data.md` | Front-loads all data in one pass |
| **1. Company Research** | `/equity-research:initiating-coverage` Task 1 | Read `{TICKER}-data.md` — do not re-fetch |
| **1b. Competitive Context** (optional, recommended for Core/Satellite) | `/financial-analysis:competitive-analysis` | Read `{TICKER}-data.md` for competitor list |
| **2. Financial Model** | `/equity-research:initiating-coverage` Task 2 | Read `{TICKER}-data.md` for historical financials |
| **3. Valuation (DCF)** | `/financial-analysis:dcf` | Read `{TICKER}-data.md` + Task 2 model output |
| **4. Peer Comparison** | `/financial-analysis:comps` | Read `{TICKER}-data.md` for peer list |
| **5. Full Report** | `/equity-research:initiating-coverage` Task 5 | Read all prior task outputs |

### Step 0 — Data Fetch (detailed instructions)

1. Read `references/data-fetch-protocol.md` in full before fetching anything.
2. Fetch EDGAR filing index for `{TICKER}` to get the latest 10-K URL.
3. Fetch the 10-K with the financial statements prompt from the protocol.
4. Fetch the 10-K with the business description prompt.
5. Fetch the 10-K with the risk factors prompt.
6. If KPIs are not in the 10-K, fetch the company IR page with the key metrics prompt.
7. Fetch Yahoo Finance only for: current stock price, 52-week range, consensus EPS estimates.
8. Assemble all data into `{TICKER}-data.md` using the structure in `references/data-fetch-protocol.md`.

### Equity-Type Emphasis in Phase 2

| Type | Emphasize in Tasks 1–5 |
|------|----------------------|
| Defensive | Dividend history and payout ratio sustainability; debt maturity profile; regulatory moat |
| Core | Moat sources and durability; FCF conversion; reinvestment rate and ROIC vs. WACC |
| Satellite | TAM sizing and penetration assumption; unit economics (CAC/LTV or gross margin trajectory); path to FCF positivity |

---

## Phase 3 — Comparison & Relative Value

After the deep dive, validate the stock against peers before committing capital.

```
/financial-analysis:comps
```
Build EV/EBITDA, P/E, EV/Revenue, EV/FCF vs. the peer group. Answer: are you paying a premium,
at parity, or getting a discount? Is the premium/discount justified?

```
/financial-analysis:competitive-analysis
```
Positioning, moat durability, competitive threats. Especially important for Satellite positions
where you're making a differentiated bet against consensus.

**Key question by type:**
- Defensive: Is the dividend yield above peers? Is the balance sheet stronger?
- Core: Is the FCF yield at a discount to intrinsic value? Does ROIC exceed peers?
- Satellite: Is the growth rate and TAM opportunity better than peers at this valuation?

---

## Phase 4 — Thesis Documentation

Before buying, lock the thesis in writing. This is your anchor for every future review.

```
/equity-research:thesis
```

**Fields to fill carefully for personal investing context:**

- **Equity type**: Defensive / Core / Satellite (from your classification)
- **Variant perception**: What do you believe that the market is underpricing?
- **Key assumptions**: 3–5 specific, falsifiable assumptions the thesis rests on
- **Invalidation criteria**: What specific events or data points would make you sell?
  (Be explicit — e.g. "FCF margin falls below 15% for 2 consecutive quarters" not "fundamentals deteriorate")
- **Position sizing rationale**: Why this size given the type? (Defensive: income weight; Core: conviction weight; Satellite: capped at risk budget)
- **Price target and horizon**: Intrinsic value estimate + time to realize

Save to `/Equity-analyses/{Type}/Watchlist/{TICKER}/Thesis/thesis-v1-{YYYY-MM}.md`.

---

## Phase 5 — Ongoing Review

Once a position is open (folder moves to `/Holding/`), shift to monitoring cadence.

### Pre-Earnings
```
/equity-research:earnings-preview
```
Model bull/base/bear scenarios. Define what would constitute a beat, miss, or thesis-confirming quarter.

### Post-Earnings
```
/equity-research:earnings       ← beat/miss analysis, thesis check
/equity-research:model-update   ← update actuals, revise forward estimates
/equity-research:thesis         ← update or reaffirm; never let it go stale
```

### Between Earnings (lightweight)
```
/equity-research:morning-note   ← macro + portfolio-level developments
/equity-research:catalysts      ← upcoming events across full portfolio
```

### Annual Review
```
/equity-research:thesis         ← reaffirm or close each position
wealth-management:tlh           ← tax-loss harvesting opportunities
wealth-management:rebalance     ← drift check, rebalancing trades
```

---

## Folder Structure

**Always ask the user to confirm equity type and lifecycle stage before creating any files.**
This ensures outputs land in the correct folder.

```
/Equity-analyses/
  /Defensive/
    /Screening/        ← Phase 1 screening outputs
    /Watchlist/        ← initiated, not yet held
    /Holding/          ← current positions
    /Closed/           ← exited positions
  /Core/
    /Screening/
    /Watchlist/
    /Holding/
    /Closed/
  /Satellite/
    /Screening/
    /Watchlist/
    /Holding/
    /Closed/

  /{Type}/{Stage}/{TICKER}/
    {TICKER}-data.md                       ← Phase 2 data cache (Step 0 output)
    /Initiation/
      company-research.md                  ← Phase 2 Task 1
      competitive-analysis.md              ← Phase 2 Task 1b (optional)
      financial-model.xlsx                 ← Phase 2 Task 2
      dcf-model.xlsx                       ← Phase 2 Task 3
      comps.xlsx                           ← Phase 2 Task 4
      initiation-report.docx               ← Phase 2 Task 5
    /Thesis/
      thesis-v1-{YYYY-MM}.md               ← Phase 4 (increment version on major updates)
    /Reviews/
      {YYYY}-Q{N}-earnings-preview.md      ← Phase 5 pre-earnings
      {YYYY}-Q{N}-earnings-update.md       ← Phase 5 post-earnings
```

### Lifecycle transitions
- **Screening → Watchlist**: After Phase 2 initiation + Phase 4 thesis. Stock clears your bar but you haven't bought yet.
- **Watchlist → Holding**: After buying. Move the folder; no file changes needed.
- **Holding → Closed**: After selling. Move the folder; add a closing note to the thesis file with exit rationale and date.
