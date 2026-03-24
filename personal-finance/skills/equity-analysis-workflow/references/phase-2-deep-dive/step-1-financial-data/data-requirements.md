# Data Requirements — Phase 2 / Step 1: Financial Data Collection

## Time Span by Equity Type (READ FIRST)

| Equity Type | Trailing Years |
|---|---|
| Growth | 5 |
| Core | 8 |
| Defensive | 12 |

Applies to: Income Statement, Balance Sheet, and Cash Flow Summary.

## Requirements

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Income statement (1)(2)  | Revenue, gross profit, EBIT, EBITDA, net income, EPS (diluted); revenue growth %; gross/EBIT/EBITDA/net income margins; R&D and S&M/G&A ($ and % of revenue) | "FY2024 Rev: $1.1B, GM: 72%, EBITDA: $130M (12%), EPS: $2.10, RevGrowth: 18%" | 1 year |
| Balance sheet (1)(2)  | Total debt, cash, net debt, total equity, total assets, current assets, current liabilities, goodwill & intangibles, net debt/EBITDA, book value per share | "FY2024: Debt $200M, Cash $450M, Assets $2.1B, BV/Share $8.40" | 1 year |
| Cash flow summary (1)(2)  | Operating Cash Flow, capex, FCF, FCF margin, SBC, dividends paid, share repurchases, FCF yield, change in working capital | "FY2024 FCF: $180M (16% margin), SBC $45M, Buybacks $120M" | 1 year |
| Key metrics / KPIs | For modeling operational drivers | "ARR: $1.2B, NRR: 118%" | 1 quarter |
| Consensus EPS estimates | NTM and N+1 estimates | "NTM EPS: $2.45; N+1 EPS: $3.10" | 3 days |
| Consensus revenue estimates | NTM and N+1 | "NTM Rev: $1.28B; N+1 Rev: $1.52B" | 3 days |
| Current stock price | For per-share reference | "$142.50" | 1 day |

**Remarks:**

(1) Data in trailing N years — see `data-requirements.md` › "Time Span by Equity Type"

(2) Derived fields (margins, revenue growth %, ratios, per-share values, FCF yield) are computed from raw data already collected — no additional fetch required. See `## Derived Field Formulas` below.

## Derived Field Formulas

| Field | Formula |
|---|---|
| Revenue Growth % | `(Revenue[t] / Revenue[t-1]) - 1` |
| Gross / EBIT / Net Income Margin | `Line Item / Revenue` |
| EBITDA | `EBIT + D&A` — D&A sourced from cash flow statement non-cash add-back |
| EBITDA Margin | `EBITDA / Revenue` |
| Net Debt / EBITDA | `Net Debt / EBITDA` |
| Book Value Per Share | `Total Equity / Diluted Shares Outstanding` |
| FCF Yield | `FCF / Market Cap` — uses current stock price × diluted shares |
| R&D / S&M / G&A % of Revenue | `Line Item ($) / Revenue` |
| ROIC | `NOPAT / Invested Capital` — NOPAT = EBIT × (1 − effective tax rate); Invested Capital = Total Equity + Net Debt; effective tax rate = Tax Expense / Pre-tax Income (Income Statement) |
| ROE | `Net Income / Total Equity` |
| ROA | `Net Income / Total Assets` |
| FCF Conversion | `FCF / Net Income` |
| Interest Coverage | `EBIT / Interest Expense` — Interest Expense from Income Statement collected above |

If D&A is not surfaced from the income statement data, it is typically the largest non-cash line in the operating section of the cash flow statement — fetch it from the same Income Statement / Cash Flow source.