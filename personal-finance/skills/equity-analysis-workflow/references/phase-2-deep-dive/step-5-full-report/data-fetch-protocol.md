# Data Fetch Protocol — Phase 2 / Step 5: Full Initiating Coverage Report

| Data | Source | Prompt |
|---|---|---|
| Step 1 company research | Current session | — |
| Step 1b competitive context | Current session | — |
| Step 2 financial model | Current session | — |
| Step 3 DCF valuation | Current session | — |
| Step 4 comps analysis | Current session | — |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Consensus estimates | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: NTM EPS and revenue consensus. Table format."` |
