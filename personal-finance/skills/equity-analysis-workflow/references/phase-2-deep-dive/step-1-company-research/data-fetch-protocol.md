# Data Fetch Protocol — Phase 2 / Step 1: Company Research

| Data | Source | Prompt |
|---|---|---|
| Current stock price + 52-week range | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price, 52-week high, 52-week low. One line each."` |
| Business description, management team, risk factors, competitors | Latest 10-K via `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=10-K&dateb=&owner=include&count=1` | `"Extract: (1) business description — segments, revenue mix, pricing model, key customers; (2) management team — CEO, CFO with tenure; (3) top 10 risk factors as bullet points; (4) named competitors. Sections clearly labeled."` |
| Income statement (4 years) | `https://finance.yahoo.com/quote/{TICKER}/financials` | `"Extract: last 4 fiscal years — revenue, gross profit, operating income, net income. Annual table format only."` |
| Balance sheet (2 years) | `https://finance.yahoo.com/quote/{TICKER}/balance-sheet` | `"Extract: last 2 fiscal years — total debt, cash & equivalents, total equity. Annual table format only."` |
| Cash flow summary (4 years) | `https://finance.yahoo.com/quote/{TICKER}/cash-flow` | `"Extract: last 4 fiscal years — operating cash flow, capex, free cash flow. Annual table format only."` |
| Key metrics / KPIs | Latest 10-Q via `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=10-Q&dateb=&owner=include&count=1` | `"Extract: operational KPIs disclosed by management (ARR, NRR, customer count, retention, GMV, or equivalent). Table format. Most recent quarter only."` |
| Company history, events & acquisitions | Web search: `"{COMPANY} history acquisitions milestones"` + Wikipedia company page | `"Summarize the major milestones in the last 20 years: strategic pivots, acquisitions (name, deal size, rationale, outcome), divestitures, regulatory events, and leadership transitions. Chronological bullet list, 1–2 sentences per event."` |
| Past major price actions | Web search: `"{TICKER} stock major price moves history"` + financial news archives | `"List noticeable price moves greater than ±20% in the past 10 years. For each: date range, approximate magnitude, and primary cause (e.g. earnings miss, guidance cut, macro shock, M&A, short report). Chronological table."` |
