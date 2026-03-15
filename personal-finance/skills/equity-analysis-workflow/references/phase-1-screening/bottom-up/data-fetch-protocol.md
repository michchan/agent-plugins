# Data Fetch Protocol — Phase 1 / Bottom-Up Screening

| Data | Source | Prompt |
|---|---|---|
| Screener (valuation + growth ratios) | `https://finance.yahoo.com/screener/` | `"Extract: ticker, company name, market cap, P/S (NTM), EV/EBITDA, revenue growth YoY, FCF margin, short interest % of float. Table format only. Top 20 results."` |
| Recent SEC filings (FCF / growth validation) | `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=10-Q&dateb=&owner=include&count=1` | `"Extract: most recent quarter revenue, operating cash flow, capex, free cash flow. No prose."` |
| Insider activity (Form 4) | `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=4&dateb=&owner=include&count=10` | `"Extract: last 5 Form 4 filings — insider name, role, transaction type (buy/sell), shares, price, date. Table format."` |
| 52-week range + short interest | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price, 52-week high, 52-week low, short interest % of float. One-line each."` |
