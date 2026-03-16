# Data Fetch Protocol — Phase 2 / Step 4: Full Initiating Coverage Report

| Data | Source | Prompt |
|---|---|---|
| Step 1 company research | Current session; fallback: data file | — |
| Step 2 financial model | Current session; fallback: data file | — |
| Step 3 DCF valuation | Current session; fallback: data file | — |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Consensus estimates | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: NTM EPS and revenue consensus. Table format."` |
