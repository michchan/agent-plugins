# Data Cache File — Formatting Instructions

Derive the cache file structure from the data requirements using the conventions below.

---

## File Title

```
# {TICKER} — {Phase} {Subtask} Data
```

For sector-level tasks (e.g., top-down screening) where there is no single ticker, use:

```
# {SECTOR_NAME} — {Subtask} Data
```

---

## Section Structure

Create one `##` section per logical field group in the data requirements. Use the group's natural name as the heading (e.g., `## Macro Regime Indicators`, `## Consensus Estimates`).

---

## Timestamps

- **Fetched data** — first line of each section: `Fetched: {YYYY-MM-DD}`
- **Always-fresh fields** (TTL = days) — annotate: `Fetched: {YYYY-MM-DD} _(always fetch fresh)_`
- **Permanent or Manual fields** (TTL = Permanent / Manual) — omit the `Fetched:` line entirely
- **Cross-step data** (TTL = "Current session" or "Saved") — write `_(from {step name or file path})_` instead of a fetch date, and do not re-fetch

---

## Data Format by Type

| Data type | Format |
|---|---|
| Quantitative / time-series | Markdown table — columns = time periods or peer tickers; rows = line items. Include `%` margin/ratio columns where relevant. |
| Qualitative / narrative | Bulleted list, one item per bullet. Use short prose only when the field is explicitly narrative (e.g., Sector Thesis, Bull/Bear case). |
| Enum / status | Write the exact value from the allowed set (e.g., `Intact / Strengthened / Weakened / Invalidated`). |
| Checklist | `- [ ] {item}` per item |

---

## Placeholder Syntax

| Placeholder | Use for |
|---|---|
| `{PLACEHOLDER_NAME}` | String values |
| `{VALUE}` | Numeric values |
| `{$B}` | Dollar amounts in billions |
| `{YYYY-MM-DD}` | Dates |
| `{TICKER}` | Stock symbols |
| `{RANGE}` | Numeric ranges |

---

## Cross-Step References

When a field's source is a prior step's cache file, reference it inline instead of fetching:

```
_(from {relative/path/to/prior-step-data-file.md})_
```

Do not duplicate data that already exists in a prior step's file.
