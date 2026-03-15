# Data Fetch Protocol — Phase 1 / Top-Down Screening

| Data | Source | Prompt |
|---|---|---|
| Sector ETF performance | `https://finance.yahoo.com/quote/{ETF_TICKER}` | `"Extract: YTD return, 1-year return, current price, 52-week range. Table format. No prose."` |
| Sector ETF holdings (top 10) | ETF provider page (e.g. iShares, SPDR) or `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&company={ETF_NAME}&type=N-PORT&dateb=&owner=include&count=5` | `"Extract: top 10 holdings by weight, ticker, and weight %. Table format only."` |
| Macro regime indicators | Yahoo Finance or general web search | `"Extract current values only: Fed funds rate, 10-year Treasury yield, latest CPI YoY, DXY level. One-line each."` |
| Analyst consensus on sector | General web search for recent sector notes from major banks | `"Summarize analyst consensus on {SECTOR}: overweight/neutral/underweight, key themes, top stock picks mentioned. Under 200 words."` |
| Market size & TAM | Mordor Intelligence, GlobeNewswire, Statista, or general web search | `"Find current global market size ($B), consensus CAGR range, fastest-growing sub-segment, and North America share for the {SECTOR} market. Numbers only, cite source name."` |
| Competitive landscape | General web search for recent sector competitive analysis | `"Describe the competitive structure of {SECTOR}: identify Tier 1 platform players and Tier 2 specialists, name top 5 players with latest ARR or annual revenue and YoY growth, and summarise the key competitive dynamic (e.g. platformisation, bundling, consolidation). Under 200 words."` |
| Peer revenue snapshot | Yahoo Finance, Macrotrends, or company IR pages for each named ticker | `"For each of these tickers: {LIST}, extract TTM revenue ($B), YoY revenue growth %, and consensus forward EPS growth %. Table format only."` |
| Regulatory / structural risks | General web search for recent regulatory news in {SECTOR} | `"List any pending or recently enacted regulations or structural policy changes directly affecting {SECTOR} revenue models. One bullet per item, under 150 words total."` |
| Recent M&A / corporate events | General web search | `"List notable acquisitions, partnerships, or major product launches among the top 5 companies in {SECTOR} over the last 12 months. Include deal size where available. Bullet list, under 150 words."` |
