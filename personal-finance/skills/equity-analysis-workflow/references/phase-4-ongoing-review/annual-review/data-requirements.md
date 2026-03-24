# Data Requirements — Phase 5 / Annual Review

Data needed to invoke the skill for an annual position review.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Full-year actuals | Revenue, EPS, FCF, key KPIs for the fiscal year | "FY2024: Rev $1.1B (+22% YoY), EPS $2.12, FCF $180M" | 1 year |
| Thesis status assessment | Is the original thesis still intact? | "Intact — ARR and margin targets both met" | Manual |
| Updated valuation inputs | Revised DCF assumptions based on full-year results | "Growth rate revised up to 22%; discount rate unchanged" | 1 year |
| Consensus estimates (NTM) | Updated street expectations for next year | "FY2025 EPS: $2.65, Rev: $1.34B" | 3 days |
| Competitor developments | Has the competitive landscape shifted? | "HubSpot gained market share in SMB segment" | 1 year |
| Position lifecycle decision | Hold / add / reduce / exit | "Hold — thesis intact, position at target size" | Manual |
| Current stock price | For upside/downside recalculation | "$142.50" | 1 day |
| Original thesis | Phase 4 thesis document | _(saved Phase 4 output)_ | Saved |
| Prior model | Phase 2 financial model | _(saved Phase 2 output)_ | Saved |

## Fetch Protocol

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
