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

## Peer Comparable Data
Required for exit-multiple terminal value calibration in `financial-analysis:dcf`.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Peer tickers | Comparable company list | "PANW, S, FTNT" | 1 year |
| Peer EV | Enterprise value per peer | "$32.5B" | 1 day |
| Peer NTM revenue | NTM revenue consensus per peer | "$4.8B" | 1 day |
| Peer NTM FCF | NTM FCF consensus per peer | "$850M" | 1 day |
| Peer revenue growth (YoY) | LTM or NTM revenue growth per peer | "+22% YoY" | 1 day |
| Peer FCF margin | LTM FCF / LTM revenue per peer | "18%" | 1 day |
| Peer gross margin | LTM gross margin per peer | "72%" | 1 day |
