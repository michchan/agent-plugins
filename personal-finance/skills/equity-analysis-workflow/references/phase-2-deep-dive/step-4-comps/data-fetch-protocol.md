# Data Fetch Protocol — Phase 2 / Step 4: Peer Comparison (Comps)

| Data | Source | Prompt |
|---|---|---|
| Step 1 company research (peer list + subject context) | Current session | — |
| Subject stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price, market cap, EV (enterprise value) if shown. One line each."` |
| Subject consensus estimates | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: NTM EPS and revenue consensus. Table format."` |
| Peer prices and multiples | `https://finance.yahoo.com/quote/{PEER_TICKER}` (repeat per peer) | `"Extract: current price, market cap, P/E NTM, EV/EBITDA, EV/Sales. One line each."` |
| Peer consensus estimates | `https://finance.yahoo.com/quote/{PEER_TICKER}/analysis` | `"Extract: NTM EPS and revenue consensus. Table format."` |
| Peer LTM financials (if needed) | EDGAR 10-K/10-Q for each peer | `"Extract: last 12 months revenue, EBITDA, free cash flow, total debt, cash. Table format only."` |
| Subject company financials (LTM / historical) | Current session (Steps 1/2 output) | — |
| Subject company KPIs | Current session (Step 1 output) | — |
| Step 2 financial model | Current session | — |
