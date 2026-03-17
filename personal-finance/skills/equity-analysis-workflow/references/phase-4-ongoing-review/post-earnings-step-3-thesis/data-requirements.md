# Data Requirements — Phase 5 / Post-Earnings Step 3: Thesis Update

Input fields needed to invoke `equity-research:thesis` for a post-earnings thesis update.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Current thesis | Existing thesis document | _(saved Phase 4 output)_ | Saved |
| Earnings analysis | Beat/miss summary, key takeaways | _(Step 1 output)_ | Current session |
| Updated model | Revised estimates post-earnings | _(Step 2 output)_ | Current session |
| Updated thesis status | Still intact / weakened / strengthened | "Strengthened — ARR beat confirms growth re-acceleration" | Manual |
| Price target delta | Change in price target based on updated model | "Raised from $165 to $178" | 1 quarter |
| Position sizing review triggers | Has anything crossed a threshold to resize? | "NRR held at 119% — no trigger" | Manual |
| Current stock price | For updated upside/downside calculation | "$158.00" | 1 day |
