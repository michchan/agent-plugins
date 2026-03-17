# Data Fetch Protocol — Phase 2 / Step 5: Report Generation

| Data | Source | Prompt |
|---|---|---|
| Step 1 company research | Current session; fallback: data file | — |
| Step 2 financial model | Current session; fallback: data file | — |
| Step 3 DCF valuation | Current session; fallback: data file | — |
| Step 4 competitive analysis | Current session; fallback: competitive-analysis.pptx in initiation folder | — |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Consensus estimates | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: NTM EPS and revenue consensus. Table format."` |
