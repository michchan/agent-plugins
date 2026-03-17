# Data Fetch Protocol — Phase 5 / Pre-Earnings

| Data | Source | Prompt |
|---|---|---|
| Consensus EPS estimate | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS estimate for upcoming quarter and full year. Table format."` |
| Consensus revenue estimate | Same as above | `"Extract: consensus revenue estimate for upcoming quarter and full year. Table format."` |
| Earnings date + time | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: next earnings date and whether BMO or AMC. One line."` |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Analyst estimate revisions | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Summarize any recent upward or downward EPS/revenue estimate revisions. Under 100 words."` |
