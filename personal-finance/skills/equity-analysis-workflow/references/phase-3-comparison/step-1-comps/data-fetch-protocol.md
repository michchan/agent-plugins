# Data Fetch Protocol — Phase 3 / Step 1: Comps (Trading Multiples)

| Data | Source | Prompt |
|---|---|---|
| Phase 2 Step 2 financial model (LTM revenue, EBITDA, cash flow) | Saved output | — |
| Phase 2 Step 1 company research (business description, competitor list) | Saved output | — |
| Phase 2 balance sheet data (debt and cash for EV) | Saved output | — |
| Subject market cap + EV | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price, market cap, enterprise value if shown. One line each."` |
| Subject NTM EPS + revenue | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: NTM EPS estimate and NTM revenue estimate. Table format."` |
| Peer prices + multiples | `https://finance.yahoo.com/quote/{PEER_TICKER}` (per peer) | `"Extract: current price, market cap, P/E NTM, EV/EBITDA NTM, EV/Sales NTM. One line each."` |
| Peer NTM estimates | `https://finance.yahoo.com/quote/{PEER_TICKER}/analysis` | `"Extract: NTM EPS and revenue consensus. Table format."` |
| Peer LTM financials (if not in Phase 2 outputs) | EDGAR 10-Q for each peer | `"Extract: last 12 months revenue, EBITDA, free cash flow, total debt, cash. Table only."` |
