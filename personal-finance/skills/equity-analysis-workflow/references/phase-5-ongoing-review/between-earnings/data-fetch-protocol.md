# Data Fetch Protocol — Phase 5 / Between Earnings

| Data | Source | Prompt |
|---|---|---|
| Recent company news | General web search | `"Find news in the past 30 days about {TICKER} / {COMPANY NAME}. Key headlines only. Bullet points, chronological."` |
| Current stock price + price action | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price, 1-month return, 3-month return, YTD return. One line each."` |
| Upcoming earnings date | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: next earnings date and whether BMO or AMC. One line."` |
| Upcoming catalyst dates | `https://finance.yahoo.com/calendar/earnings` | `"Extract all earnings dates for portfolio holdings in the next 60 days. Table format."` |
| Competitor news | General web search | `"Find news in the past 30 days about key competitors of {TICKER}. Bullet points, chronological."` |
