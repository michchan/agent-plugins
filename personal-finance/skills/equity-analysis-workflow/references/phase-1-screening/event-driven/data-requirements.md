# Data Requirements — Phase 1 / Event-Driven Screening

Fields required to run an event-driven screen (catalyst → entry point).

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Event type | Earnings, FDA decision, M&A close, product launch, spin-off, index inclusion, etc. | "FDA PDUFA decision" | Permanent |
| Expected event date | Date or date range when the catalyst is expected | "2025-04-15" | 7 days |
| Ticker | Company ticker(s) associated with the event | "MRNA" | Permanent |
| Sector | Sector of the company | "Biotechnology" | Permanent |
| Expected impact | Bull-case and bear-case price impact assessment | "Bull: +40% on approval; Bear: -25% on rejection" | 1 month |
| Relevant macro context | Any macro factors that amplify or dampen the catalyst | "Risk-off environment may limit upside even on approval" | 1 month |
| Prior event outcome | How the company performed around the last similar event (optional) | "Q3 2024 earnings: +12% on day; beat EPS by $0.08" | Permanent |
| Watchlist overlap | Whether the ticker is already on the user's watchlist | "Yes — added 2025-02-01" | 1 week |

## Fetch Protocol

| Data | Source | Prompt |
|---|---|---|
| Earnings calendar | `https://finance.yahoo.com/calendar/earnings` | `"Extract: all earnings dates for {TICKER} in the next 90 days. Include date, time (BMO/AMC if known), and consensus EPS estimate. Table format."` |
| SEC filing schedule | `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=&dateb=&owner=include&count=10` | `"Extract: next expected filing type and due date for {TICKER}. One line only."` |
| Fed / regulatory announcement calendar | General web search for FOMC meeting dates, FDA PDUFA dates, or relevant regulatory calendar | `"List upcoming {EVENT_TYPE} dates in the next 90 days. Date and event description only. No prose."` |
| Event background / context | Company IR page or news search | `"Summarize the context for {EVENT_TYPE} at {TICKER}: what happened last time, what to watch, bull/bear scenarios. Under 250 words."` |
