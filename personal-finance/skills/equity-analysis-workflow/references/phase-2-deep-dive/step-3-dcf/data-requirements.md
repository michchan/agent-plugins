# Data Requirements — Phase 2 / Step 3: DCF Valuation

Input fields needed to invoke `financial-analysis:dcf`. Historical data comes from Step 1 output; projections from Step 2.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Historical income statement (4 years) | Revenue, EBIT, net income as baseline | "FY2024 Rev: $1.1B, EBIT: $95M" | 1 year |
| Historical cash flow (4 years) | FCF history for growth rate calibration | "FY2024 FCF: $180M, FY2023: $140M" | 1 year |
| Balance sheet (debt, cash) | For net debt / enterprise value bridge | "Debt: $200M, Cash: $450M → Net cash: $250M" | 1 year |
| Financial model projections | Forward revenue, EBIT, FCF projections | _(from Step 2 output)_ | Current session |
| Key metrics / KPIs | For sanity-checking growth assumptions | "NRR: 118% → supports 20%+ ARR growth" | 1 quarter |
| Consensus EPS / revenue estimates | NTM and N+1 | "NTM EPS: $2.45; NTM Rev: $1.28B" | 1 day |
| Current stock price | For implied return calculation | "$142.50" | 1 day |
