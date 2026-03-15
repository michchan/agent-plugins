# Data Requirements — Phase 4 / Thesis Documentation

Input fields needed to invoke `equity-research:thesis`. Sourced from Phase 2 and Phase 3 outputs.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Investment rationale | Core reason to own the stock | "Durable ARR compounder with expanding FCF margin" | Manual |
| Bull case | Upside scenario and key assumptions | "NRR expands to 125%, multiple re-rates to 12x EV/S → $210" | Manual |
| Base case | Central scenario and key assumptions | "20% ARR growth, 18% FCF margin → $165" | Manual |
| Bear case | Downside scenario and key assumptions | "Competition intensifies, NRR falls to 105% → $95" | Manual |
| Entry price rationale | Why current price is a good entry | "Trading at 20% discount to DCF base case" | Permanent |
| Price target | 12-month target price | "$165" | 1 quarter |
| Stop-loss level | Price at which thesis is invalidated | "$110 (below DCF bear case)" | Manual |
| Position sizing | Initial position size (% of portfolio) | "3% of portfolio" | Manual |
| Key risks | Top 3–5 risks that could invalidate the thesis | "1. NRR compression 2. Competitive displacement 3. Macro slowdown" | 1 year |
| Monitoring triggers | Events or metrics that would prompt thesis review | "NRR below 110% for 2 consecutive quarters" | Manual |
| Peer context | Relative valuation vs. peers | _(Phase 3 Step 1 output)_ | 1 quarter |
| Competitive positioning summary | Moat assessment | _(Phase 3 Step 2 output)_ | 1 year |
