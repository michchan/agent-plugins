# Data Requirements — Phase 5 / Post-Earnings Step 3: Thesis Update

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Current thesis | Existing thesis document | _(saved Phase 4 output)_ | Saved |
| Earnings analysis | Beat/miss summary, key takeaways | _(Step 1 output)_ | Current session |
| Updated model | Revised estimates post-earnings | _(Step 2 output)_ | Current session |
| Updated thesis status | Still intact / weakened / strengthened | "Strengthened — ARR beat confirms growth re-acceleration" | Manual |
| Price target delta | Change in price target based on updated model | "Raised from $165 to $178" | 1 quarter |
| Position sizing review triggers | Has anything crossed a threshold to resize? | "NRR held at 119% — no trigger" | Manual |
| Current stock price | For updated upside/downside calculation | "$158.00" | 1 day |

## Fetch Protocol

| Data | Source | Prompt |
|---|---|---|
| Step 1 earnings analysis (beat/miss, key takeaways) | Current session | — |
| Step 2 updated model and revised estimates | Current session | — |
| Phase 4 thesis document | Saved output | — |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
