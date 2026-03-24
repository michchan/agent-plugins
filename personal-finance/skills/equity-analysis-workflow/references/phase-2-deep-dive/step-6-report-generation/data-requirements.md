# Data Requirements — Phase 2 / Step 6: Report Generation

Input fields needed to invoke `equity-research:initiating-coverage` for final report assembly.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Financial data | Historical financial statements and ratio analysis | _(Step 1 output)_ | Current session |
| Financial model | Forward projections and key assumptions | _(Step 3 output)_ | Current session |
| Company research | Business overview, qualitative thesis | _(Step 2 output)_ | Current session |
| DCF valuation | Intrinsic value, price target | _(Step 4 output)_ | Current session |
| Competitive analysis | Positioning map, dimension scoring, TAM split | _(Step 5 output)_ | Current session |
| Current stock price | For price target upside/downside | "$142.50" | 1 day |
| Consensus estimates | For premium/discount to consensus | "NTM EPS: $2.45, NTM Rev: $1.28B" | 3 days |
