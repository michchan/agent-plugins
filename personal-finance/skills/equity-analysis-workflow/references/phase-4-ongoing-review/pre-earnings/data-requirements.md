# Data Requirements — Phase 5 / Pre-Earnings

Input fields needed to invoke `equity-research:earnings-preview`.

| Field | Description | Example | Cache TTL |
|---|---|---|---|
| Consensus EPS estimate | Street consensus for upcoming quarter | "$0.62" | 1 day |
| Consensus revenue estimate | Street consensus for upcoming quarter | "$312M" | 1 day |
| Whisper number | Buy-side whisper vs. published consensus (if available) | "Whisper EPS: $0.67 vs. consensus $0.62" | 1 day |
| Prior quarter actuals | EPS and revenue reported last quarter | "Q3 2024: EPS $0.58, Rev $298M" | 1 quarter |
| Key metrics to watch | KPIs most important this quarter | "ARR, NRR, net new logos" | 1 quarter |
| Management guidance | Revenue and EPS guidance given last quarter | "Q4 guidance: Rev $305–315M, EPS $0.59–0.63" | 1 quarter |
| Prior year comp | Same quarter last year actuals | "Q4 2023: EPS $0.44, Rev $256M" | 1 year |
| Earnings date + time | BMO or AMC, exact date | "2025-02-05, AMC" | 1 day |
| Current stock price | For risk/reward framing | "$142.50" | 1 day |
