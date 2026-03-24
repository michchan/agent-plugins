# Data Requirements — Phase 1 / Bottom-Up Screening

Fields for a bottom-up screen (criteria → names). Not all fields are required — supply what is relevant.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Revenue growth rate | YoY or TTM revenue growth (%) | "32% YoY" | 1 quarter |
| FCF yield | Free cash flow / market cap (%) | "4.2%" | 3 days |
| FCF margin | Free cash flow / revenue (%) | "18%" | 1 quarter |
| NTM P/S | Next-twelve-months price-to-sales ratio | "6.4x" | 3 days |
| EV/EBITDA | Enterprise value / EBITDA (LTM or NTM) | "22x NTM" | 3 days |
| Insider activity | Recent insider buys/sells (Form 4 data) | "CEO bought 50k shares at $142 on 2025-01-15" | 1 month |
| Short interest | Short interest as % of float | "8.3% of float" | 1 month |
| 52-week range position | Current price as % of 52-week range | "72% of 52-week range" | 3 days |
| Minimum market cap | Floor for market cap inclusion ($M) | "$2,000M" | Permanent |
| Universe / sector filter | Sector or industry to restrict the screen | "Software" | Permanent |

## Fetch Protocol

| Data | Source | Prompt |
|---|---|---|
| Screener (valuation + growth ratios) | `https://finance.yahoo.com/screener/` | `"Extract: ticker, company name, market cap, P/S (NTM), EV/EBITDA, revenue growth YoY, FCF margin, short interest % of float. Table format only. Top 20 results."` |
| Recent SEC filings (FCF / growth validation) | `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=10-Q&dateb=&owner=include&count=1` | `"Extract: most recent quarter revenue, operating cash flow, capex, free cash flow. No prose."` |
| Insider activity (Form 4) | `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=4&dateb=&owner=include&count=10` | `"Extract: last 5 Form 4 filings — insider name, role, transaction type (buy/sell), shares, price, date. Table format."` |
| 52-week range + short interest | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price, 52-week high, 52-week low, short interest % of float. One-line each."` |
