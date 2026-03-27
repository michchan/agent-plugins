# Manual Data Prompt Template

Use this template when composing a manual fetch prompt. After composing, write it to the `.prompts/` file and copy its content to the clipboard — do **not** return the prompt text in chat.

Populate each section using the data requirements (for fields and sources).

---

## Rules

- **Role line** — always open with `You are a financial data assistant.`

- **Brief description** — one sentence after the role line summarising the fetch context (ticker, sector, phase, step).

- **Numbered sections** — one section per logical data group in the data requirements; keep them short and scannable.

- **Sources** — pull suggested sources from the data requirements; include a URL where available.

- **Return format** — always close with the instruction to return as a single markdown code block, followed by the expected file structure (derived from the data requirements per `references/data-cache-file-instruction.md`) with `{VALUE}` or `{PLACEHOLDER}` tokens.

- **"Return as a markdown codeblock"** — explicitly include this instruction in the prompt so the tool returns parseable output.

- [IMPORTANT] DO NOT mention the option to declare a field as "NOT DISCLOSED". As this will create an hallucination for the agent to skip eagerly. For example, a message like the following should be EXCLUDED: "Flag unavailable line items as [NOT DISCLOSED] rather than leaving blank.".

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