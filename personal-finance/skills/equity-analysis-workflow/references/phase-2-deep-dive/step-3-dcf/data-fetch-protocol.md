# Data Fetch Protocol — Phase 2 / Step 3: DCF Valuation

| Data | Source | Prompt |
|---|---|---|
| Step 2 financial model (forward projections) | Current session; fallback: data file | — |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Consensus EPS/revenue estimates | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS and revenue estimates for current and next fiscal year. Table only."` |
| Historical income statement (4 years) | Current session; fallback: data file (Steps 1/2 output) | — |
| Historical cash flow (4 years) | Current session; fallback: data file (Steps 1/2 output) | — |
| Balance sheet (debt, cash) | Current session; fallback: data file (Steps 1/2 output) | — |
| Key metrics / KPIs | Current session; fallback: data file (Step 1 output) | — |

## Peer Comparable Data — Resolution Protocol

For each required peer ticker {P}, resolve each field using the following priority:

### Level 1: Subject's own peer data cache

- File: subject's `*-peer-data.md` (path per folder-structure.md, most recent)
- Look for row where Ticker = {P}
- Apply per-field TTL per `data-requirements.md`; skip stale fields and mark them as needing resolution

### Level 2: Cross-ticker peer data file

- Only for fields not resolved in Level 1
- Scan all other tickers' `*-peer-data.md` files (path per folder-structure.md, exclude subject)
- For each file: check Peer Comparable Data table for a row where Ticker = {P}
- Select the most recently fetched match; apply per-field TTL per `data-requirements.md`

### Level 3: Peer's own financial model

- Only for fields not yet resolved that can be derived from a financial model (see derivations below)
- Find {P}'s `*-financial-model.md` (path per folder-structure.md, most recent)
- Derive:
  - Revenue Growth → Income Statement section: (LTM Revenue / prior year) - 1
  - FCF Margin → Cash Flow Summary section: most recent FCF Margin column
  - Gross Margin → Income Statement section: most recent Gross Margin column
  - NTM Revenue → Consensus Estimates section: NTM Revenue row
- Apply per-field TTL per `data-requirements.md`

### Level 4: Fresh fetch from Yahoo Finance

- For any field still unresolved after Levels 1–3

| Field | Source | Prompt |
|---|---|---|
| Peer EV + market data | `https://finance.yahoo.com/quote/{PEER_TICKER}` per peer | `"Extract: current price, market cap, enterprise value. One line each."` |
| Peer NTM revenue + FCF estimates | `https://finance.yahoo.com/quote/{PEER_TICKER}/analysis` per peer | `"Extract: NTM revenue and FCF consensus. Table format."` |
| Peer revenue growth + margins | EDGAR 10-Q or Yahoo Finance per peer | `"Extract: LTM revenue growth, gross margin, FCF margin. Table only."` |

_Peer data feeds `{YYYY-MM-DD}-peer-data.md` under `/Data/`; per-field TTL per `data-requirements.md`._

### Transparency Summary

After resolving all peer fields, show the user the following table before running the DCF:

| Peer | EV | NTM Rev | NTM FCF | Rev Growth | FCF Margin | Gross Margin |
|---|---|---|---|---|---|---|
| {P} | {source} | {source} | {source} | {source} | {source} | {source} |

Source labels: `Fresh` (Level 4 fetch), `L1: own cache`, `L2: {ticker} cache`, `L3: fin-model`. This lets the user flag overrides before the DCF runs.
