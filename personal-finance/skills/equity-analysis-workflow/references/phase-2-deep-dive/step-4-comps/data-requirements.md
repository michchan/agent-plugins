# Data Requirements — Phase 2 / Step 4: Peer Comparison (Comps)

Input fields needed to invoke `financial-analysis:comps`.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Competitors / peer list | Starting list of peer tickers | "CRM, HUBS, ZEN" | 1 year |
| Subject company financials | LTM and historical income statement, balance sheet, cash flow | "FY2024 Rev: $1.1B, EBIT: $95M, FCF: $180M" | 1 year |
| Subject company KPIs | For relative benchmarking | "NRR: 118%, ARR: $1.2B" | 1 quarter |
| Business description | For peer selection justification | "Mid-market CRM SaaS" | 1 year |
| Current stock price | For subject company | "$142.50" | 1 day |
| Consensus estimates | NTM EPS/revenue for subject and peers | "NTM EPS: $2.45, NTM Rev: $1.28B" | 1 day |
| Step 2 financial model | For forward projections to include in comps | _(from Step 2 output)_ | Current session |
