# Data Requirements — Phase 2 / Step 5: Report Generation

Input fields needed to invoke `equity-research:initiating-coverage` for final report assembly.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Company research | Business overview, qualitative thesis | _(Step 1 output)_ | Current session |
| Financial model | 3-statement projections | _(Step 2 output)_ | Current session |
| DCF valuation | Intrinsic value, price target | _(Step 3 output)_ | Current session |
| Competitive analysis | Positioning map, dimension scoring, TAM split | _(Step 4 output)_ | Current session |
| Current stock price | For price target upside/downside | "$142.50" | 1 day |
| Consensus estimates | For premium/discount to consensus | "NTM EPS: $2.45, NTM Rev: $1.28B" | 3 days |
