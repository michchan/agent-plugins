# Data Fetch Protocol — Phase 1 / Event-Driven Screening

| Data | Source | Prompt |
|---|---|---|
| Earnings calendar | `https://finance.yahoo.com/calendar/earnings` | `"Extract: all earnings dates for {TICKER} in the next 90 days. Include date, time (BMO/AMC if known), and consensus EPS estimate. Table format."` |
| SEC filing schedule | `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=&dateb=&owner=include&count=10` | `"Extract: next expected filing type and due date for {TICKER}. One line only."` |
| Fed / regulatory announcement calendar | General web search for FOMC meeting dates, FDA PDUFA dates, or relevant regulatory calendar | `"List upcoming {EVENT_TYPE} dates in the next 90 days. Date and event description only. No prose."` |
| Event background / context | Company IR page or news search | `"Summarize the context for {EVENT_TYPE} at {TICKER}: what happened last time, what to watch, bull/bear scenarios. Under 250 words."` |
