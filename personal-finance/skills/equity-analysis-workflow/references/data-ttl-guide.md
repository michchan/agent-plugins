# Data TTL Guide — Cache Freshness Rules

When evaluating whether a cached data section is still fresh, apply this guide in order: check for event-driven overrides first, then apply the tier's reset trigger, then fall back to the fallback duration if the trigger event date is unknown.

---

## Section 1 — Determination Principles

Apply in priority order. Use the most specific principle that applies.

1. **Regulatory filing anchor** — Data sourced directly from a filed document (10-K, 10-Q, 8-K) is immutable for the period it covers. Its TTL resets only when the next filing supersedes it. Historical periods are permanently frozen.

2. **Publication cadence, not calendar duration** — TTL is tied to the next expected update event (next earnings release, next 10-K, next analyst revision), not a fixed number of days since the `Fetched:` date. Use the fallback duration only when the trigger event date is unknown.

3. **Market price derivation** — Data derived from live prices (stock price, market cap, EV, peer multiples) is intraday. For a buy-and-hold investor, one trading week is a reasonable reuse window for thesis-level analysis, but any stale market-derived input used in a valuation calculation must be surfaced to the user before proceeding.

4. **Consequence of staleness** — When two data types share a similar update cadence, assign the shorter TTL to whichever field causes a larger analytical error if stale (e.g., analyst consensus estimates directly drive NTM multiples and entry price decisions).

5. **Event-driven override (always wins)** — Any TTL can be overridden to "immediately stale" by a material event (earnings release, executive departure, product launch, restatement, M&A close). Check for event overrides before applying calendar-based TTL.

---

## Section 2 — TTL Tiers

| Tier | Reset Trigger | Fallback Duration |
|---|---|---|
| **Immutable** | Restatement only | Never expires |
| **Annual** | Next 10-K filing | ~365 days |
| **Quarterly** | Next earnings release | ~90 days |
| **Weekly** | Next business week | 7 calendar days |
| **Intraday** | Any new market session | 1 business day |

**Intraday** corresponds to the `_(always fetch fresh)_` annotation in `data-cache-file-instruction.md`.
**Immutable** corresponds to the "Permanent" TTL — omit the `Fetched:` line entirely in the cache file.

---

## Section 3 — Field-Level Lookup Table

> **Reference guide for judgment — not exhaustive.** This table covers common fields encountered in the workflow. It may not list every field you encounter. Apply the principles from Section 1 to determine TTL for unlisted fields, and confirm with the user when uncertain.

Organized by tier, from longest TTL (top) to shortest (bottom). The "Event Override" column names events that immediately invalidate the cache regardless of calendar age.

### Immutable

| Field | Event Override |
|---|---|
| Company basics (legal name, HQ, founding date, exchange, GICS) | Merger close, name change, spin-off |
| Historical annual financials — prior completed fiscal years (Income Statement, Cash Flow Statement, Balance Sheet) | SEC restatement filing |
| Quarterly results — prior quarters | 10-Q restatement |
| SaaS KPIs (ARR, NRR, customer count) — prior quarters | Metric definition restatement |

### Annual

| Field | Reset Trigger | Event Override |
|---|---|---|
| Employee count | Next 10-K | Significant layoff announcement (>10% workforce) |
| Industry / TAM estimates | Updated industry report or 10-K | Major regulatory change affecting TAM scope |
| Risk factors | Next 10-K | New material litigation or regulatory action |
| Historical annual financials — most recent completed fiscal year | Next 10-K | 10-K restatement |
| M&A precedent transactions (closed, disclosed) | New comparable deal closes | — |

### Quarterly

| Field | Reset Trigger | Event Override |
|---|---|---|
| Product and service list | Next earnings release | New product launch, product sunset, M&A close |
| Management team (CEO, CFO, key executives) | Next earnings release | Executive departure or appointment |
| Competitive landscape | Next earnings release | Competitor M&A, major new entrant |
| Quarterly results — most recent quarter | Next 10-Q or 10-K | Preliminary results release |
| SaaS KPIs — most recent quarter | Next earnings release | — |
| Peer LTM financials | Next peer earnings release | 10-Q / 10-K filing for any peer |

### Weekly

| Field | Event Override |
|---|---|
| Recent news (headlines, press releases) | Any material news event |
| Analyst consensus estimates (NTM revenue, EPS, EBIT) | Earnings release, guidance update, major analyst initiation/downgrade |
| Peer NTM consensus estimates | Peer earnings release, peer guidance update |
| Peer EV multiples (EV/NTM Revenue, EV/NTM FCF) | Resets when price or consensus resets |
| M&A precedents — pending deals | Deal close, termination, or revised terms |

> **Note on analyst consensus:** Even within the weekly window, flag to the user if any material guidance event has occurred since the `Fetched:` date.

### Intraday

| Field | Event Override |
|---|---|
| Stock price (subject company) | — |
| Market cap (subject company) | — |
| Enterprise value (subject company) | Debt issuance, equity raise, buyback announcement |
| Peer stock prices and market caps | — |

---

## Section 4 — Partial Staleness Rules

A single cache file contains sections with different TTLs. Evaluate each `##` section independently.

1. **Section-level, not file-level** — do not treat the whole file as fresh or stale based on a single `Fetched:` date.
2. **Stale section not needed for current step** → skip re-fetch; note the staleness in output.
3. **Stale section needed, can be fetched independently** → re-fetch only that section; append to a new dated file.
4. **Stale section needed, cannot be fetched independently** → surface to user: "Section X is stale (fetched {date}, TTL {tier}). Re-fetch full file or proceed with stale data?"
5. **Immutable sections** → skip TTL evaluation entirely; never re-fetch.
6. **Stale Intraday or Weekly field used in a valuation calculation** → always confirm with user before proceeding; do not silently reuse.
7. **Log partial reuse** → note in output: "Note: [Section] data is from {date} and may be stale; re-fetch deferred per user confirmation."
