# Data Requirements — Phase 5 / Post-Earnings Step 1: Earnings Analysis

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Reported EPS | Actual EPS vs. consensus | "$0.68 vs. $0.62 consensus (+$0.06 beat)" | Permanent |
| Reported revenue | Actual revenue vs. consensus | "$318M vs. $312M consensus (+$6M beat)" | Permanent |
| Segment results | Revenue and margin by segment | "CRM: $192M (+21% YoY); Analytics: $79M (+18% YoY)" | Permanent |
| Key metric actuals | KPI results for the quarter | "ARR: $1.31B (+24% YoY); NRR: 119%" | Permanent |
| Guidance update | Updated forward guidance | "Q1 2025 guidance: Rev $325–335M, EPS $0.65–0.68" | 1 quarter |
| Prior consensus estimates | What was expected before results | "$0.62 EPS, $312M revenue" | Permanent |
| Prior actuals (for YoY) | Same quarter last year | "Q4 2023: EPS $0.44, Rev $256M" | Permanent |
| Analyst estimate revisions | Post-earnings consensus changes | "FY2025 EPS raised from $2.45 to $2.65" | 3 days |
| Current stock price | Post-earnings price reaction | "$158.00 (+11% on day)" | 1 day |

## Fetch Protocol

| Data | Source | Prompt |
|---|---|---|
| Reported EPS vs. consensus | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: reported EPS, consensus EPS, beat/miss amount. One line each."` |
| Reported revenue vs. consensus | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: reported revenue, consensus revenue, beat/miss. One line each."` |
| IR press release | Company IR page (earnings press release URL) | `"Extract: segment results, key metrics, and updated guidance. Under 400 words. Bullet points."` |
| Updated guidance | Same IR press release | Included in above prompt |
| Analyst estimate revisions | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS and revenue estimates post-earnings update. Table format."` |
| Post-earnings stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
