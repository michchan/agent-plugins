# Data Requirements — Phase 1 / Top-Down Screening

Fields required to run a top-down screen (macro → sector → names).

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Sector name | Name of the sector under review | "Semiconductors" | Permanent |
| Sector ETF ticker | Representative ETF | "SOXX" | Permanent |
| Macro regime indicators | Current rate environment, GDP trend, inflation regime, dollar strength | "Fed funds: 4.25%, 10Y: 4.3%, CPI YoY: 3.1%, DXY: 104" | 1 day |
| Sector ETF performance | YTD and 1-year return vs. S&P 500 | "SOXX YTD: +12.4%, 1Y: +28.1%; SPY YTD: +8.2%" | 1 day |
| Analyst consensus on sector | Overweight / Neutral / Underweight calls from major banks, key sector themes | "Goldman: OW; key theme: AI capex cycle, data center buildout" | 1 month |
| Major holdings / names | Top holdings in sector ETF; names of specific interest | "NVDA 10.5%, AVGO 8.2%, TSM 6.1%" | 1 quarter |
| Sector thesis / narrative | Bull case and bear case for the sector right now | "Bull: AI cycle sustains; Bear: rate sensitivity compresses multiples" | 1 quarter |
