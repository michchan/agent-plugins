# Data Requirements — Phase 2 / Step 2: Company Research

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Business description | Segments, revenue mix, pricing model, customers | "Cloud software, 3 segments: CRM 60%, Analytics 25%, Support 15%" | 1 year |
| Management team | CEO, CFO, key C-suite | "CEO: John Smith (since 2019); CFO: Jane Lee (since 2021)" | 1 year |
| Risk factors | Top 10 bullet points from 10-K | "1. Customer concentration — top 5 = 30% of revenue" | 1 year |
| Competitors list | Named peers from 10-K | "Salesforce, HubSpot, Zendesk" | 1 year |
| Key metrics / KPIs | Operational KPIs disclosed by company | "ARR: $1.2B, NRR: 118%, Customers: 12,400" | 1 quarter |
| Historical financials | Income statement, cash flow, and balance sheet data — reuse Step 1 (Financial Data Collection) output; no separate fetch required. **Fallback:** if Step 1 did not run, fetch these directly (see `data-fetch-protocol.md`). | _(from `*-financial-data.md`)_ | Inherits from Step 1 (1 year for historical data) |
| Current stock price | For context | "$142.50" | 1 day |
| 52-week range | High and low | "$98.00 – $168.00" | 3 days |
| Company history, events & acquisitions | Major milestones, pivots, acquisitions, divestitures, regulatory events in trailing 20 years | "2017: Acquired XYZ for $1.2B; 2020: pivoted to SaaS model" | 1 year |
| Past major price actions | Noticeable price moves (>±10%) with causes — trailing 10 years | "Mar 2020: −45% (COVID selloff); Nov 2021: +60% (earnings beat + raised guidance)" | 1 year |
