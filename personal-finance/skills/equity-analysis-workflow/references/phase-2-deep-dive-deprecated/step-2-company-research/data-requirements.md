# Data Requirements — Phase 2 / Step 2: Company Research

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Business description | Segments, revenue mix, pricing model, customers | "Cloud software, 3 segments: CRM 60%, Analytics 25%, Support 15%" | 1 year |
| Management bios | Career history, tenure, background, and notable decisions for CEO, CFO, and 2-3 other key executives (enough to write 300-400 words per person) | "CEO John Smith: 20-yr tech background, previously VP at Oracle, joined 2019, led SaaS transition" | 1 year |
| Industry overview | Industry structure, growth drivers, regulatory environment, and macro tailwinds/headwinds | "SaaS CRM market: ~$80B, growing 12% annually; key drivers: digital transformation, SMB adoption" | 1 year |
| Competitive analysis | Per-competitor profile (5-10 peers): business model, strengths, weaknesses, market share, and differentiation vs. subject company | "Salesforce: dominant CRM, 20% share, strong enterprise; weak in SMB pricing vs. subject" | 1 year |
| TAM sizing | Total addressable market estimate with source or methodology | "CRM TAM: $80B by 2026 per Gartner; company-disclosed TAM: $75B" | 1 year |
| Risk factors | 8-12 risks structured across 4 categories (e.g. competitive, regulatory, operational, macro); sourced from 10-K and supplemented with independent research | "Competitive: margin pressure from Salesforce; Regulatory: GDPR compliance cost" | 1 year |
| Competitors list | Named peers from 10-K | "Salesforce, HubSpot, Zendesk" | 1 year |
| Key metrics / KPIs | Operational KPIs disclosed by company | "ARR: $1.2B, NRR: 118%, Customers: 12,400" | 1 quarter |
| Historical financials | Income statement, cash flow, and balance sheet data — reuse Step 1 (Financial Data Collection) output; no separate fetch required. **Fallback:** if Step 1 did not run, fetch these directly. | _(from `*-financial-data.md`)_ | Inherits from Step 1 (1 year for historical data) |
| Current stock price | For context | "$142.50" | 1 day |
| 52-week range | High and low | "$98.00 – $168.00" | 3 days |
| Company history, events & acquisitions | Major milestones, pivots, acquisitions, divestitures, regulatory events in trailing 20 years | "2017: Acquired XYZ for $1.2B; 2020: pivoted to SaaS model" | 1 year |
| Past major price actions | Noticeable price moves (>±10%) with causes — trailing 10 years | "Mar 2020: −45% (COVID selloff); Nov 2021: +60% (earnings beat + raised guidance)" | 1 year |
