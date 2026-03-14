# Requirements

## Persona

I'm a personal, buy-and-hold, mid/long-term or core-satellite style investor. I want to create a skill to encode my preference of equity analysis workflow for my investing.

- Investment horizon: 2-10 years depending on purpose
- Rebalance trigger: quarterly or market-driven

---

## Kind of equities

In my definition, there could be three types of equities in my portfolio:

### 1. Defensive

- Goal: Cash parking to provide liquidity in the future, while earning more yield than just bonds
- Nature: Low volatility and risk, from defensive sector, high income

### 2. Core

- Goal: Achieve stable and long term wealth accumulation
- Nature: Medium volatility and risk, strong moat and business model with sustainable growth, preferably slightly over-performing benchmark

### 3. Satellite

- Goal: Achieve stable and long term wealth accumulation
- Nature: High volatility and risk, strong/exploding growth engine and potential, futuristic, substantially over-performing benchmark

---

## Investing workflow

The following workflow rides on "financial-services-plugins" by anthropics.

### Phase 1 — Screening & Idea Generation

The top of the funnel. Two entry points depending on whether you're starting top-down or bottom-up:

**Top-down** → `/equity-research:sector` — Get a sector overview first, identify where you want exposure, then drill into names.

**Bottom-up** → `/equity-research:screen` — Run a screen with your criteria (valuation, growth, quality factors) to surface candidates.

**Event-driven** → `/equity-research:catalysts` — Check the catalyst calendar for upcoming events that might create entry points across your watchlist.

---

### Phase 2 — Deep Dive (Initiation)

For any stock that clears screening, this is where you build conviction. This is the most intensive phase and runs as a **sequential 5-task workflow**:

| Step | Skill | Output |
|------|-------|--------|
| 1. Company research | `/equity-research:initiate` (Task 1) | Research markdown |
| 2. Financial model | `/equity-research:initiate` (Task 2) | Excel 3-statement model |
| 3. Valuation | `/financial-analysis:dcf` | DCF model + sensitivity table |
| 4. Peer comparison | `/financial-analysis:comps` | Trading comps Excel |
| 5. Full report | `/equity-research:initiate` (Task 5) | Initiating coverage DOCX |

For the competitive context layer, add `/financial-analysis:competitive-analysis` between steps 1 and 2 — it feeds directly into your moat assessment.

---

### Phase 3 — Comparison & Relative Value

After the deep dive, sanity-check the stock against peers before committing:

**`/financial-analysis:comps`** — EV/EBITDA, P/E, EV/Revenue, EV/FCF vs. the peer group. Tells you whether you're getting a bargain or paying up.

**`/financial-analysis:competitive-analysis`** — Positioning, moat durability, threats. Especially important for satellite positions where you're making a differentiated bet.

---

### Phase 4 — Thesis Documentation

Before buying, lock the thesis in writing. This is your anchor for every future decision.

**`/equity-research:thesis`** — Documents your core belief, key assumptions, variant perception vs. consensus, price target, position sizing rationale (defensive vs core vs. satellite), and explicit invalidation criteria (what would make you sell).

This becomes your reference doc every earnings season and every time volatility spikes.

---

### Phase 5 — Ongoing Review (Recurring)

Once a position is open, the workflow shifts to a monitoring cadence:

```
Pre-earnings  →  /equity-research:earnings-preview  (scenario modeling: bull/base/bear)
Post-earnings →  /equity-research:earnings          (beat/miss, thesis check, estimate updates)
Model refresh →  /equity-research:model-update      (update actuals, revise forward estimates)
Thesis update →  /equity-research:thesis            (update or reaffirm — never let it go stale)
Calendar sync →  /equity-research:catalysts         (upcoming events across full portfolio)
```

For lighter-touch monitoring between earnings, `/equity-research:morning-note` covers macro + portfolio-level developments without requiring a full deep dive.

### The Rhythm at a Glance

```
QUARTERLY
  Pre-earnings  →  earnings-preview
  Post-earnings →  earnings + model-update + thesis (update)

ONGOING / AD-HOC
  New idea      →  screen → sector → initiate → dcf → comps → competitive-analysis → thesis
  Portfolio     →  rebalance (drift check) + catalysts (calendar)

ANNUAL
  Tax review    →  tlh
  Full review   →  thesis (reaffirm or close each position)
```

---

## Working folder structure

Folder/files anatomy for the whole workflow.

For each kind of equity:
- `/Screening` contains screening outputs of each instruction.
- `/Watchlist` contains initiated equity that is yet to hold.
- `/Holding` contains owned equity
- `/Closed` contains previously owned equity.

```
/Equity-analayses  
  /Defensive
    /Screening
    /Watchlist
    /Holding
    /Closed
  /Core
    /Screening
    /Watchlist
    /Holding
    /Closed
  /Satellite
    /Screening
    /Watchlist
    /Holding
    /Closed
```

An equity folder:

```
/AAPL
  /Initiation
    company-research.md
    financial-model.xlsx
    dcf-model.xlsx
    comps.xlsx
    competitive-analysis.docx
    initiation-report.docx
  /Thesis
    thesis-v1-2026-03.docx
  /Reviews
    2026-Q1-earnings-preview.docx
```
