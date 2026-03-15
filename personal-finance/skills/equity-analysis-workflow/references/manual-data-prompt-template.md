# Manual Data Prompt Template

Use this template when composing a manual fetch prompt for the user to copy-paste into their own tools.

Populate each section using the current step's `data-requirements.md` (for fields and sources) and `data-file-template.md` (for the expected output structure).

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

Source suggestion: [Source name and/or URL from data-fetch-protocol.md]

---

## 2. [Section Name]
[Description of what to fetch]
Ticker: [TICKER] ([Full company/ETF name])
Fetch:
- [Field 1]
- [Field 2]
- [Field 3]

Source: [URL from data-fetch-protocol.md]

---

## [N]. [Section Name]
[Repeat as needed for each data group in data-requirements.md]

---

Return everything as a single markdown code block, structured exactly like this:

[Paste the full contents of data-file-template.md here, with {PLACEHOLDER} tokens for each value]
```

---

## Composition rules

1. **Role line** — always open with `You are a financial data assistant.`
2. **Brief description** — one sentence after the role line summarising the fetch context (ticker, sector, phase, step).
3. **Numbered sections** — one section per logical data group in `data-requirements.md`; keep them short and scannable.
4. **Sources** — pull suggested sources from `data-fetch-protocol.md`; include a URL where available.
5. **Return format** — always close with the instruction to return as a single markdown code block, followed by the full structure from `data-file-template.md` with `{VALUE}` or `{PLACEHOLDER}` tokens.
6. **"Return as a markdown codeblock"** — explicitly include this instruction in the prompt so the tool returns parseable output.
