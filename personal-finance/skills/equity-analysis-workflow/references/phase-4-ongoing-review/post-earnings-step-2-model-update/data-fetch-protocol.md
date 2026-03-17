# Data Fetch Protocol — Phase 5 / Post-Earnings Step 2: Model Update

| Data | Source | Prompt |
|---|---|---|
| Step 1 earnings analysis (reported EPS, revenue, segment results, guidance) | Current session | — |
| Phase 2 Step 2 financial model (baseline model to update) | Saved output | — |
| Revised consensus estimates (NTM) | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: updated NTM and N+1 EPS and revenue consensus post-earnings. Table format."` |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
