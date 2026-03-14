## Core-Satellite Investment Workflow

---

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

**`/equity-research:thesis`** — Documents your core belief, key assumptions, variant perception vs. consensus, price target, position sizing rationale (core vs. satellite), and explicit invalidation criteria (what would make you sell).

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

---

### Portfolio Layer — Google Sheets (via Google Drive)

With Google Drive connected, I can read and write directly to your portfolio sheet. The suggested structure is a master sheet with:

- **Holdings tab** — ticker, position size, cost basis, weight, core vs. satellite tag, thesis status
- **Watchlist tab** — screened names waiting for better entry
- **Catalyst tab** — synced from `/equity-research:catalysts`

Then plug in these wealth management skills on a regular cadence:

**`/wealth-management:rebalance`** — Analyzes drift between your actual weights and target allocation (e.g., core 70% / satellite 30%). Generates rebalancing trades.

**`/wealth-management:tlh`** — Scans for tax-loss harvesting opportunities in down positions, especially useful end-of-year.

I can read your sheet, run the analysis, and write results back — or output a summary you paste in yourself.

---

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