# Data Requirements — Phase 2 / Step 5: Competitive Analysis

Input fields needed to invoke `financial-analysis:competitive-analysis`.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Subject business description | Segments, products, pricing model, customers | _(from Step 2 output)_ | Current session |
| Peer tickers and names | Top 3 comparable competitors | _(from Step 2 output or Step 4 peer list)_ | Current session |
| Step 4 peer market data | EV, NTM revenue, NTM FCF per peer | _(from Step 4 peer-data output)_ | Current session |
| Competitive positioning dimensions | 2 dominant axes for the 2×2 map | "Product breadth vs. enterprise readiness" | Current session |
| TAM and market share estimates | Total addressable market split by competitor | "Subject: ~8%, Peer 1: ~22%" | 1 year |
