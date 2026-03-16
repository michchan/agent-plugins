# Data Fetch Protocol — Phase 2 / Step 2: Financial Model

| Data | Source | Prompt |
|---|---|---|
| Consensus EPS estimates (NTM, N+1) | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS estimates for current fiscal year and next fiscal year. Revenue estimates too if shown. Table format only."` |
| Consensus revenue estimates | Same as above | Included in above prompt |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Income statement (4 years) | Current session (Step 1 output); fallback: data file | — |
| Balance sheet (2 years) | Current session (Step 1 output); fallback: data file | — |
| Cash flow summary (4 years) | Current session (Step 1 output); fallback: data file | — |
| Key metrics / KPIs | Current session (Step 1 output); fallback: data file | — |
