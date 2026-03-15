# Phase 2 — Deep Dive (Initiation)

For any stock that clears screening, this phase builds conviction. It runs as a **sequential workflow**
with a mandatory data-fetch pre-step to minimize token usage.

**Before starting: confirm with the user:**
1. Equity type (Defensive / Core / Satellite)
2. Lifecycle stage (Watchlist — not yet held, or Screening — still evaluating)
3. Whether to run steps one at a time (pausing for review between each) or all at once

This determines the folder path for all outputs.

## Modified Initiation Workflow

| Step | Action | Token optimization |
|------|--------|--------------------|
| **0. Data Fetch** (mandatory pre-step) | Read `references/phase-2-data-fetch-protocol.md`, fetch from EDGAR + targeted sources, save to `{TICKER}-data.md` | Front-loads all data in one pass |
| **1. Company Research** | Invoke skill `equity-research:initiating-coverage` | Read `{TICKER}-data.md` — do not re-fetch |
| **1b. Competitive Context** (optional, recommended for Core/Satellite) | Invoke skill `financial-analysis:competitive-analysis` | Read `{TICKER}-data.md` for competitor list |
| **2. Financial Model** | Invoke skill `equity-research:initiating-coverage` | Read `{TICKER}-data.md` for historical financials |
| **3. Valuation (DCF)** | Invoke skill `financial-analysis:dcf` | Read `{TICKER}-data.md` + Task 2 model output |
| **4. Peer Comparison** | Invoke skill `financial-analysis:comps` | Read `{TICKER}-data.md` for peer list |
| **5. Full Report** | Invoke skill `equity-research:initiating-coverage` | Read all prior task outputs |

## Fetch Once, Pass Forward

Step 0 front-loads all data in a single pass and saves it to `{TICKER}-data.md`.
Steps 1–5 **read that file** — do not re-fetch data that is already cached.

> Do not re-fetch a section if its `Fetched:` date is within the freshness threshold defined in
> `references/phase-2-data-fetch-protocol.md`. Stock price and consensus estimates are never cached —
> always fetch fresh.

## Step 0 — Data Fetch (detailed instructions)

1. Read `references/phase-2-data-fetch-protocol.md` in full before fetching anything.
2. Fetch EDGAR filing index for `{TICKER}` to get the latest 10-K URL.
3. Fetch the 10-K with the financial statements prompt from the protocol.
4. Fetch the 10-K with the business description prompt.
5. Fetch the 10-K with the risk factors prompt.
6. If KPIs are not in the 10-K, fetch the company IR page with the key metrics prompt.
7. Fetch Yahoo Finance only for: current stock price, 52-week range, consensus EPS estimates.
8. Assemble all data into `{TICKER}-data.md` using the structure in `references/phase-2-data-fetch-protocol.md`.

