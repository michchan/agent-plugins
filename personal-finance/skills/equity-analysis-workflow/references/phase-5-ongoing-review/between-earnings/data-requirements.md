# Data Requirements — Phase 5 / Between Earnings

Input fields for `equity-research:morning-note` or `equity-research:catalysts`.

## Morning Note (`equity-research:morning-note`)

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Recent news headlines | Key company-specific news since last review | "CEO interview on Bloomberg; new product announcement" | 1 day |
| Macro developments | Relevant macro changes | "Fed hold; sector rotation out of growth" | 1 day |
| Competitor announcements | Competitor earnings, product launches, M&A | "Salesforce Q3 beat; raised guidance" | 1 month |
| Price / volume data | Recent price action and volume trends | "+8% over past month on above-avg volume" | 1 day |
| Current stock price | For context | "$142.50" | 1 day |

## Catalyst Calendar (`equity-research:catalysts`)

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Upcoming earnings dates | Next earnings date for holdings | "2025-05-07, AMC" | 1 week |
| Expected catalysts | Product launches, regulatory decisions, investor days | "Investor day: 2025-04-22" | 1 week |
| Macro events | FOMC meetings, CPI prints, other macro dates | "FOMC: 2025-05-06–07" | 1 month |
