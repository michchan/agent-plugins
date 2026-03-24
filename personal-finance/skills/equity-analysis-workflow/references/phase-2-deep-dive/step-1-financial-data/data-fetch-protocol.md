# Data Fetch Protocol — Phase 2 / Step 1: Financial Data Collection

| Data | Source | Prompt |
|---|---|---|
| Income statement | `https://finance.yahoo.com/quote/{TICKER}/financials` | `"Extract: last N fiscal years — revenue, gross profit, operating income (EBIT), net income, EPS (diluted), R&D, S&M, G&A. Annual table format only."` |
| Balance sheet | `https://finance.yahoo.com/quote/{TICKER}/balance-sheet` | `"Extract: last N fiscal years — total debt, cash & equivalents, total equity, total assets, current assets, current liabilities, goodwill & intangibles. Annual table format only."` |
| Cash flow summary | `https://finance.yahoo.com/quote/{TICKER}/cash-flow` | `"Extract: last N fiscal years — operating cash flow, capex, free cash flow, stock-based compensation, dividends paid, share repurchases, change in working capital. Annual table format only."` |
| Key metrics / KPIs | Latest 10-Q via `https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=10-Q&dateb=&owner=include&count=1` | `"Extract: operational KPIs disclosed by management (ARR, NRR, customer count, retention, GMV, or equivalent). Table format. Most recent quarter only."` |
| Consensus EPS estimates (NTM, N+1) | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS estimates for current fiscal year and next fiscal year. Revenue estimates too if shown. Table format only."` |
| Consensus revenue estimates | Same as above | Included in above prompt |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |

_N = trailing years per equity type — see `data-requirements.md` › Time Span by Equity Type._

## Derived / Computed Fields

No additional fetch required — compute derived fields from raw data collected above. See `data-requirements.md` › "Derived Field Formulas" for methods.

## Manual Prompt Batching

When **Manual prompt** is selected and the equity type's trailing-year span (N) exceeds 5 (see `data-requirements.md` › Time Span by Equity Type), split data collection into separate prompts — one per 4-year batch.

Compose one prompt codeblock per batch. Each prompt must specify the exact year range in the header and use the matching rows from `data-file-template.md` as the return structure.

After all batches are returned, merge results into a single cache file.
