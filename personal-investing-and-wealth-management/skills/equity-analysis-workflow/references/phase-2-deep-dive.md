# Phase 2 — Deep Dive (Initiation)

For any stock that clears screening, this phase builds conviction. It runs as a **sequential workflow**
with a mandatory data-fetch pre-step to minimize token usage.

**Before starting: confirm with the user:**
1. Equity type (Defensive / Core / Satellite)
2. Lifecycle stage (Watchlist — not yet held, or Screening — still evaluating)

This determines the folder path for all outputs.

## Modified Initiation Workflow

| Step | Action | Token optimization |
|------|--------|--------------------|
| **0. Data Fetch** (mandatory pre-step) | Read `references/data-fetch-protocol.md`, fetch from EDGAR + targeted sources, save to `{TICKER}-data.md` | Front-loads all data in one pass |
| **1. Company Research** | `/equity-research:initiating-coverage` Task 1 | Read `{TICKER}-data.md` — do not re-fetch |
| **1b. Competitive Context** (optional, recommended for Core/Satellite) | `/financial-analysis:competitive-analysis` | Read `{TICKER}-data.md` for competitor list |
| **2. Financial Model** | `/equity-research:initiating-coverage` Task 2 | Read `{TICKER}-data.md` for historical financials |
| **3. Valuation (DCF)** | `/financial-analysis:dcf` | Read `{TICKER}-data.md` + Task 2 model output |
| **4. Peer Comparison** | `/financial-analysis:comps` | Read `{TICKER}-data.md` for peer list |
| **5. Full Report** | `/equity-research:initiating-coverage` Task 5 | Read all prior task outputs |

## Step 0 — Data Fetch (detailed instructions)

1. Read `references/data-fetch-protocol.md` in full before fetching anything.
2. Fetch EDGAR filing index for `{TICKER}` to get the latest 10-K URL.
3. Fetch the 10-K with the financial statements prompt from the protocol.
4. Fetch the 10-K with the business description prompt.
5. Fetch the 10-K with the risk factors prompt.
6. If KPIs are not in the 10-K, fetch the company IR page with the key metrics prompt.
7. Fetch Yahoo Finance only for: current stock price, 52-week range, consensus EPS estimates.
8. Assemble all data into `{TICKER}-data.md` using the structure in `references/data-fetch-protocol.md`.

## Equity-Type Emphasis in Phase 2

| Type | Emphasize in Tasks 1–5 |
|------|----------------------|
| Defensive | Dividend history and payout ratio sustainability; debt maturity profile; regulatory moat |
| Core | Moat sources and durability; FCF conversion; reinvestment rate and ROIC vs. WACC |
| Satellite | TAM sizing and penetration assumption; unit economics (CAC/LTV or gross margin trajectory); path to FCF positivity |
