# Data Fetch Protocol

Token-efficient data fetching for equity analysis. Read this before any Phase 2 fetch.

---

## Fetch Priority Order

1. **SEC EDGAR** — structured, low-token financials for public companies
2. **Company IR page** — business description, segment data, press releases
3. **Yahoo Finance** — stock price, consensus estimates, analyst targets
4. **News / general web** — last resort; use only for qualitative context not in filings

---

## EDGAR URL Patterns

Replace `{TICKER}` with the stock symbol (e.g. `AAPL`) and `{CIK}` with the company's CIK number.

### Step 1 — Get filing index (resolve CIK + list recent 10-Ks)
```
https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={TICKER}&type=10-K&dateb=&owner=include&count=3
```
- Fetch with prompt: `"Extract: company name, CIK number, and the URL of the most recent 10-K filing index page. Nothing else."`
- This resolves the CIK if you only have the ticker.

### Step 2 — Get 10-K filing document list
```
https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK={CIK}&type=10-K&dateb=&owner=include&count=1&search_text=
```
- Fetch the filing index page to find the primary document URL (usually ends in `.htm` or `-10k.htm`).
- Prompt: `"Extract only the URL of the primary 10-K document (the full annual report, not the index). Return just the URL."`

### Step 3 — Fetch financial data from 10-K
Fetch the primary 10-K document URL with a targeted prompt (see prompts below).

### Alternative — EDGAR full-text search
```
https://efts.sec.gov/LATEST/search-index?q=%22{TICKER}%22&dateRange=custom&startdt={YYYY-01-01}&enddt={YYYY-12-31}&forms=10-K
```

---

## Targeted Fetch Prompts by Data Type

### Financial statements (Income Statement, Balance Sheet, Cash Flow)
```
Extract: revenue, gross profit, operating income, net income, free cash flow (or operating cash flow minus capex), total debt, cash and equivalents for the last 4 fiscal years. Present as a compact table with years as columns. No prose, no footnotes, no headers beyond the table.
```

### Business description & segments
```
Extract: business segments, revenue by segment (most recent year), key products or services, pricing model, major customers or end markets, and geographic revenue split if available. Under 400 words. No legal boilerplate.
```

### Management team
```
Extract: CEO name and tenure, CFO name and tenure, any other C-suite relevant to the business (e.g. CTO for tech, CMO for consumer). Include prior roles only if notable. Under 150 words.
```

### Risk factors
```
List the top 10 risk factors as bullet points only. One sentence per bullet. No sub-bullets, no section headers, no numbering beyond the bullet itself.
```

### Key metrics & KPIs
```
Extract all non-GAAP or operational KPIs disclosed (e.g. ARR, NRR, DAU, same-store sales, RevPAR, tons shipped). Include definition and most recent 2 years of values. Table format preferred. No prose.
```

### Competitors list
```
Extract: list of named competitors mentioned in the 10-K (Business section or Risk Factors). Return as a plain comma-separated list of company names only. No descriptions.
```

---

## What to Save in `{TICKER}-data.md`

Structure the cached file with these sections. Leave a section blank (with a `N/A` note) rather than omitting it.

```markdown
# {TICKER} Data Cache
Source: SEC EDGAR 10-K ({fiscal year}) + supplemental

## Income Statement Summary
Fetched: {YYYY-MM-DD} | Refresh: when new 10-K is filed (≈annually)
| Metric | FY{N-3} | FY{N-2} | FY{N-1} | FY{N} |
...

## Balance Sheet Summary
Fetched: {YYYY-MM-DD} | Refresh: when new 10-K is filed (≈annually)
| Metric | FY{N-1} | FY{N} |
...

## Cash Flow Summary
Fetched: {YYYY-MM-DD} | Refresh: when new 10-K is filed (≈annually)
| Metric | FY{N-3} | FY{N-2} | FY{N-1} | FY{N} |
...

## Key Metrics / KPIs
Fetched: {YYYY-MM-DD} | Refresh: after each earnings release (≈quarterly)
...

## Business Description
Fetched: {YYYY-MM-DD} | Refresh: ~12 months, or sooner on major restructuring/M&A
...

## Management Team
Fetched: {YYYY-MM-DD} | Refresh: ~12 months, or sooner on leadership change
...

## Competitors
Fetched: {YYYY-MM-DD} | Refresh: ~12 months
...

## Risk Factors
Fetched: {YYYY-MM-DD} | Refresh: when new 10-K is filed (≈annually)
...

## Notes
Any caveats, fiscal year end dates, currency, restatements, etc.
```

---

## Data Freshness Policy

Stock price and consensus estimates are NOT cached — always fetch fresh from Yahoo Finance.

For all other sections in `{TICKER}-data.md`, check the section's `Fetched:` date before re-fetching:

| Section | Refresh trigger |
|---------|----------------|
| Income Statement, Balance Sheet, Cash Flow | New 10-K filed (check EDGAR; typically ~12 months after prior filing) |
| Key Metrics / KPIs | After each earnings release (~quarterly) |
| Business Description | 12 months, or sooner on major restructuring, spinoff, or M&A |
| Management Team | 12 months, or sooner on CEO/CFO change |
| Risk Factors | New 10-K filed (~annually) |
| Competitors | 12 months |

**Do not re-fetch a section if its `Fetched:` date is within the threshold above**, unless the user explicitly requests a refresh or you have reason to believe a material event has occurred (e.g. news of a CEO departure → refresh Management Team only).

You may refresh individual sections without rebuilding the entire file.
