# Data Fetch Protocol — Phase 2 / Step 3: DCF Valuation

| Data | Source | Prompt |
|---|---|---|
| Step 2 financial model (forward projections) | Current session | — |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Consensus EPS/revenue estimates | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS and revenue estimates for current and next fiscal year. Table only."` |
| Historical income statement (4 years) | Current session (Steps 1/2 output) | — |
| Historical cash flow (4 years) | Current session (Steps 1/2 output) | — |
| Balance sheet (debt, cash) | Current session (Steps 1/2 output) | — |
| Key metrics / KPIs | Current session (Step 1 output) | — |
