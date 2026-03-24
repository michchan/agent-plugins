# Data Fetch Protocol — Phase 2 / Step 3: Financial Modeling

No external fetches required for projections. All inputs are read from prior step outputs.

| Data | Source | Prompt |
|---|---|---|
| Historical income statement | Current session; fallback: `*-financial-data.md` (Step 1 output) | — |
| Historical balance sheet | Current session; fallback: `*-financial-data.md` (Step 1 output) | — |
| Historical cash flow | Current session; fallback: `*-financial-data.md` (Step 1 output) | — |
| Key metrics / KPIs | Current session; fallback: `*-financial-data.md` (Step 1 output) | — |
| Consensus EPS / revenue estimates | Current session; fallback: `*-financial-data.md` (Step 1 output). Re-fetch if stale (TTL: 3 days) per Step 1 data-fetch-protocol | — |
| Company research context | Current session; fallback: `*-company-research.md` (Step 2 output) | — |

## Projection Methodology

Projections are built analytically from the data above — no external source fetch is needed. Use the following approach:

1. **Revenue**: Anchor near-term (NTM, N+1) to consensus estimates. Extrapolate beyond using historical growth trend, KPI trajectory (e.g. NRR, ARR growth), and company research context (competitive positioning, end-market growth).
2. **Margins**: Trend from historical levels, adjusted for scale effects and company-disclosed targets.
3. **FCF**: Derive from projected EBITDA minus capex, working capital changes, and taxes. Calibrate against historical FCF conversion rate.
4. **Balance sheet**: Project net debt by applying FCF less capital returns (dividends, buybacks) implied by historical policy.

Record key assumptions explicitly in the output file — this allows Step 4 (DCF) to audit and override individual drivers.
