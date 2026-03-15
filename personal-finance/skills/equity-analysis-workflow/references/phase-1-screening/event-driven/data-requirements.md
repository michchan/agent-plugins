# Data Requirements — Phase 1 / Event-Driven Screening

Fields required to run an event-driven screen (catalyst → entry point).

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Event type | Earnings, FDA decision, M&A close, product launch, spin-off, index inclusion, etc. | "FDA PDUFA decision" | Permanent |
| Expected event date | Date or date range when the catalyst is expected | "2025-04-15" | 1 day |
| Ticker | Company ticker(s) associated with the event | "MRNA" | Permanent |
| Sector | Sector of the company | "Biotechnology" | Permanent |
| Expected impact | Bull-case and bear-case price impact assessment | "Bull: +40% on approval; Bear: -25% on rejection" | 1 month |
| Relevant macro context | Any macro factors that amplify or dampen the catalyst | "Risk-off environment may limit upside even on approval" | 1 month |
| Prior event outcome | How the company performed around the last similar event (optional) | "Q3 2024 earnings: +12% on day; beat EPS by $0.08" | Permanent |
| Watchlist overlap | Whether the ticker is already on the user's watchlist | "Yes — added 2025-02-01" | 1 week |
