# Data Requirements — Phase 2 / Step 1b: Competitive Context

Input fields needed to invoke `financial-analysis:competitive-analysis`.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Competitors list | Named peers from 10-K; seeds the analysis | "Salesforce, HubSpot, Zendesk" | 1 year |
| Business description | Subject company's segments, products, positioning | "CRM-focused SaaS, primarily mid-market" | 1 year |
| Revenue by segment | For relative sizing vs. competitors | "CRM 60%, Analytics 25%, Support 15%" | 1 quarter |
| Key metrics / KPIs | Subject company's KPIs for benchmarking | "NRR: 118%, ARR: $1.2B" | 1 quarter |
| Risk factors | Competitive risks highlighted by management | "Increasing competition from Salesforce Einstein" | 1 year |
| Step 1 output | Company research report from prior step | _(from current session)_ | Current session |
