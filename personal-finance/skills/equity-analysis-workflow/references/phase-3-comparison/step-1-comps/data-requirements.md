# Data Requirements — Phase 3 / Step 1: Comps (Trading Multiples)

Input fields needed to invoke `financial-analysis:comps`.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Subject ticker | Company being analyzed | "AAPL" | Permanent |
| Peer tickers | List of comparable company tickers | "MSFT, GOOGL, META" | 1 year |
| Subject LTM revenue | Last twelve months revenue | "$1.1B" | 1 quarter |
| Subject LTM EBITDA | LTM EBITDA (or EBIT if EBITDA not available) | "$320M" | 1 quarter |
| Subject LTM FCF | LTM free cash flow | "$180M" | 1 quarter |
| Subject market cap | Current market capitalization | "$18.5B" | 1 day |
| Subject enterprise value (EV) | EV = market cap + net debt | "$18.25B (net cash company)" | 1 day |
| Subject NTM EPS estimate | Next-twelve-months EPS consensus | "$2.45" | 1 day |
| Subject NTM revenue estimate | Next-twelve-months revenue consensus | "$1.28B" | 1 day |
| Peer LTM revenue / EBITDA / FCF | For each peer | _(fetched from EDGAR or Yahoo Finance)_ | 1 quarter |
| Peer market cap / EV | For each peer | _(fetched fresh)_ | 1 day |
| Peer NTM estimates | EPS + revenue for each peer | _(fetched fresh)_ | 1 day |
| Key growth rates | Revenue and EBITDA YoY growth rates | "Rev growth: 22% YoY" | 1 quarter |
| Key margins | Gross, EBIT, FCF margins | "Gross: 72%, EBIT: 9%, FCF: 16%" | 1 quarter |
