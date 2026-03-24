# Data Requirements — Phase 5 / Post-Earnings Step 2: Model Update

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| New actuals to plug in | Reported EPS, revenue, margins, KPIs for the quarter | _(from Step 1 output)_ | Current session |
| Revised consensus estimates | Updated NTM EPS and revenue post-earnings | "NTM EPS: $2.65 (raised from $2.45)" | 3 days |
| Forward guidance numbers | Management guidance for next quarter and full year | "Q1 guidance: Rev $325–335M, EPS $0.65–0.68" | 1 quarter |
| Prior financial model | Existing model from Phase 2 Step 2 | _(saved Phase 2 output)_ | Saved |
| Historical actuals | Prior quarters' actuals for model baseline | _(from prior session cache or Step 1 output)_ | 1 quarter |
| Current stock price | For per-share model update | "$158.00" | 1 day |

## Fetch Protocol

| Data | Source | Prompt |
|---|---|---|
| Step 1 earnings analysis (reported EPS, revenue, segment results, guidance) | Current session | — |
| Phase 2 Step 2 financial model (baseline model to update) | Saved output | — |
| Revised consensus estimates (NTM) | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: updated NTM and N+1 EPS and revenue consensus post-earnings. Table format."` |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
