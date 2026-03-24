# Data Requirements — Phase 1 / Top-Down Screening

Fields required to run a top-down screen (macro → sector → names).

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Sector name | Name of the sector under review | "Semiconductors" | Permanent |
| Sector ETF ticker | Representative ETF | "SOXX" | Permanent |
| Macro regime indicators | Current rate environment, GDP trend, inflation regime, dollar strength | "Fed funds: 4.25%, 10Y: 4.3%, CPI YoY: 3.1%, DXY: 104" | 3 days |
| Sector ETF performance | YTD and 1-year return vs. S&P 500 | "SOXX YTD: +12.4%, 1Y: +28.1%; SPY YTD: +8.2%" | 3 days |
| Analyst consensus on sector | Overweight / Neutral / Underweight calls from major banks, key sector themes, top stock picks or overweights mentioned by name | "Goldman: OW; key theme: AI capex cycle, data center buildout; top picks: NVDA, AVGO" | 1 month |
| Major holdings / names | Top holdings in sector ETF; names of specific interest | "NVDA 10.5%, AVGO 8.2%, TSM 6.1%" | 1 quarter |
| Market size & TAM | Global market size ($B), consensus CAGR range, key growth drivers, North America share | "$200–265B in 2026E; 10–14% CAGR to 2030–2034; cloud sub-segment ~15% CAGR; NA ~45% share" | 1 quarter |
| Peer revenue snapshot | Top 5–8 named peers: FY revenue (TTM), YoY revenue growth %, consensus forward EPS growth % | "CRWD: $3.9B TTM, +23% YoY; PANW: $8.0B TTM, +14% YoY" | 1 quarter |
| Regulatory / structural risks | Pending or recently enacted rules directly affecting sector revenue models | "EU AI Act compliance costs; US DOGE-driven budget cuts to federal IT spend" | 1 month |
| Recent M&A / corporate events | Notable acquisitions, partnerships, or product launches among top 5 names (last 12 months) | "PANW acquired CyberArk $25B (Feb 2026); CRWD/AWS expanded partnership" | 1 month |
| Competitive landscape | Tier structure (platforms vs. point vendors), key competitive dynamic, Microsoft/incumbent threat assessment | "Big Three: PANW, CRWD, MSFT; platformization compressing point vendors; MSFT bundling risk in SMB" | 1 quarter |
| Sector thesis / narrative | Bull case and bear case for the sector right now | "Bull: AI cycle sustains; Bear: rate sensitivity compresses multiples" | 1 quarter |

## Fetch Protocol

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
