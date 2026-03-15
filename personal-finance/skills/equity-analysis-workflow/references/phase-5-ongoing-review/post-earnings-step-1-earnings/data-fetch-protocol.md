# Data Fetch Protocol — Phase 5 / Post-Earnings Step 1: Earnings Analysis

| Data | Source | Prompt |
|---|---|---|
| Reported EPS vs. consensus | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: reported EPS, consensus EPS, beat/miss amount. One line each."` |
| Reported revenue vs. consensus | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: reported revenue, consensus revenue, beat/miss. One line each."` |
| IR press release | Company IR page (earnings press release URL) | `"Extract: segment results, key metrics, and updated guidance. Under 400 words. Bullet points."` |
| Updated guidance | Same IR press release | Included in above prompt |
| Analyst estimate revisions | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS and revenue estimates post-earnings update. Table format."` |
| Post-earnings stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
