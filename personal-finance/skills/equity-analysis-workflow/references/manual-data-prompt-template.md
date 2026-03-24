# Manual Data Prompt Template

Use this template when composing a manual fetch prompt for the user to copy-paste into their own tools.

Populate each section using the data requirements (for fields and sources). Derive the return format structure from the data requirements following `references/data-cache-file-instruction.md`.

---

## Template

```
You are a financial data assistant. I need current data for [BRIEF DESCRIPTION OF WHAT IS BEING FETCHED — e.g. "a top-down equity screen of the cybersecurity sector" or "company research on CrowdStrike (CRWD)"]. Please fetch all of the following and return results as a single markdown code block.

---

## 1. [Section Name]
[Description of what to fetch]
Fetch:
- [Field 1]
- [Field 2]
- [Field 3]

Source suggestion: [Source name and/or URL from the data requirements]

---

## 2. [Section Name]
[Description of what to fetch]
Ticker: [TICKER] ([Full company/ETF name])
Fetch:
- [Field 1]
- [Field 2]
- [Field 3]

Source: [URL from the data requirements]

---

## [N]. [Section Name]
[Repeat as needed for each data group in the data requirements]

---

Return everything as a single markdown code block, structured exactly like this:

[Paste the expected cache file structure here, derived from the data requirements per `data-cache-file-instruction.md`, with {PLACEHOLDER} tokens for each value]
```

---

## Composition rules

1. **Role line** — always open with `You are a financial data assistant.`
2. **Brief description** — one sentence after the role line summarising the fetch context (ticker, sector, phase, step).
3. **Numbered sections** — one section per logical data group in the data requirements; keep them short and scannable.
4. **Sources** — pull suggested sources from the data requirements; include a URL where available.
5. **Return format** — always close with the instruction to return as a single markdown code block, followed by the expected file structure (derived from the data requirements per `references/data-cache-file-instruction.md`) with `{VALUE}` or `{PLACEHOLDER}` tokens.
6. **"Return as a markdown codeblock"** — explicitly include this instruction in the prompt so the tool returns parseable output.
