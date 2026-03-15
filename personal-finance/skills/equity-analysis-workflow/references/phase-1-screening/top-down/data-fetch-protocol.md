# Data Fetch Protocol — Phase 1 / Top-Down Screening

| Data | Source | Prompt |
|---|---|---|
| Sector ETF performance | `https://finance.yahoo.com/quote/{ETF_TICKER}` | `"Extract: YTD return, 1-year return, current price, 52-week range. Table format. No prose."` |
| Sector ETF holdings (top 10) | ETF provider page (e.g. iShares, SPDR) or `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&company={ETF_NAME}&type=N-PORT&dateb=&owner=include&count=5` | `"Extract: top 10 holdings by weight, ticker, and weight %. Table format only."` |
| Macro regime indicators | Yahoo Finance or general web search | `"Extract current values only: Fed funds rate, 10-year Treasury yield, latest CPI YoY, DXY level. One-line each."` |
| Analyst consensus on sector | General web search for recent sector notes from major banks | `"Summarize analyst consensus on {SECTOR}: overweight/neutral/underweight, key themes, top stock picks mentioned. Under 200 words."` |
