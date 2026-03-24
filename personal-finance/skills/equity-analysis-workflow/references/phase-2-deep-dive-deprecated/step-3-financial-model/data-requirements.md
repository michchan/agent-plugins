# Data Requirements — Phase 2 / Step 3: Financial Modeling

Builds forward statement projections using Step 1 historical data as the foundation and Step 2 company research for qualitative context.

## Projection Horizon by Equity Type

| Equity Type | Forward Years |
|---|---|
| Growth | 5 |
| Core | 5 |
| Defensive | 3 |

Applies to: forward income statement, balance sheet, and cash flow projections.

## Requirements

| Field | Description | Example | Cache TTL | Source |
|---|---|---|---|---|
| Historical income statement | Revenue, gross profit, EBIT, EBITDA, net income, EPS — trailing N years as baseline | _(from Step 1 output)_ | Current session | Step 1 |
| Historical balance sheet | Debt, cash, equity, assets — trailing N years | _(from Step 1 output)_ | Current session | Step 1 |
| Historical cash flow | Operating cash flow, capex, FCF — trailing N years | _(from Step 1 output)_ | Current session | Step 1 |
| Key metrics / KPIs | Operational drivers (ARR, NRR, etc.) for growth assumption calibration | _(from Step 1 output)_ | Current session | Step 1 |
| Consensus EPS estimates | NTM and N+1 — for near-term sanity check of projections | _(from Step 1 output)_ | Current session (re-fetch if stale per Step 1 TTL) | Step 1 |
| Consensus revenue estimates | NTM and N+1 | _(from Step 1 output)_ | Current session | Step 1 |
| Company research context | Business description, competitive positioning, risk factors — for assumption qualifications | _(from Step 2 output)_ | Current session | Step 2 |
| Forward revenue projections (1)(2) | Revenue forecast for each projection year | "FY2026E: $1.45B (+13%)" | Current session | Modeled |
| Forward EBIT projections (1)(2) | EBIT and EBIT margin forecast | "FY2026E EBIT: $160M (11%)" | Current session | Modeled |
| Forward EBITDA projections (1)(2) | EBITDA and EBITDA margin forecast | "FY2026E EBITDA: $195M (13%)" | Current session | Modeled |
| Forward net income projections (1)(2) | Net income and EPS forecast | "FY2026E EPS: $2.80" | Current session | Modeled |
| Forward FCF projections (1)(2) | FCF and FCF margin forecast | "FY2026E FCF: $210M (14%)" | Current session | Modeled |

**Remarks:**

(1) Projections are modeled (not fetched) — derived from historical trends, KPI trajectory, and consensus anchoring. No external fetch required.

(2) Cover the forward horizon per equity type — see "Projection Horizon by Equity Type" above.
