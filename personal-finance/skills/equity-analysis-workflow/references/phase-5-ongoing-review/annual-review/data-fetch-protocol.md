# Data Fetch Protocol — Phase 5 / Annual Review

| Data | Source | Prompt |
|---|---|---|
| Full-year income statement | Latest 10-K via EDGAR | `"Extract: full-year revenue, gross profit, operating income, net income, FCF for the most recent fiscal year and prior year. Table format."` |
| Balance sheet | Same 10-K | `"Extract: total assets, total debt, cash and equivalents, shareholders equity. Most recent year-end only. Table format."` |
| Cash flow | Same 10-K | `"Extract: operating cash flow, capex, free cash flow for the most recent fiscal year. Table format."` |
| Risk factors | Same 10-K | `"List top 10 risk factors as bullet points. One sentence each."` |
| Business description changes | Same 10-K | `"Extract: any material changes to business segments, products, or strategy. Under 200 words. If no change from prior year, say 'No material change'."` |
| Consensus NTM estimates | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: NTM EPS and revenue consensus. Table format."` |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Phase 4 thesis document | Saved output | — |
| Phase 2 financial model | Saved output | — |
| Phase 3 comps output | Saved output | — |
