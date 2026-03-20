# Data Fetch Protocol — Phase 2 / Step 2: Financial Model

| Data | Source | Prompt |
|---|---|---|
| Consensus EPS estimates (NTM, N+1) | `https://finance.yahoo.com/quote/{TICKER}/analysis` | `"Extract: consensus EPS estimates for current fiscal year and next fiscal year. Revenue estimates too if shown. Table format only."` |
| Consensus revenue estimates | Same as above | Included in above prompt |
| Current stock price | `https://finance.yahoo.com/quote/{TICKER}` | `"Extract: current price. One line."` |
| Income statement | Current session (Step 1 output); fallback: data file | — |
| Balance sheet | Current session (Step 1 output); fallback: data file | — |
| Cash flow summary | Current session (Step 1 output); fallback: data file | — |
| Key metrics / KPIs | Current session (Step 1 output); fallback: data file | — |

## Manual Prompt Batching

When **Manual prompt** is selected and the equity type's trailing-year span (N) exceeds 5 (see `data-requirements.md` › Time Span by Equity Type), split data collection into separate prompts — one per 4-year batch.

Compose one prompt codeblock per batch. Each prompt must specify the exact year range in the header and use the matching rows from `data-file-template.md` as the return structure.

After all batches are returned, merge results into a single cache file.
