# Phase 2 — Deep Dive (Initiation)

For any stock that clears screening, this phase builds conviction. It runs as a **sequential workflow**.

**Before starting: confirm with the user:**
1. Equity type (Defensive / Core / Satellite)
2. Lifecycle stage (Watchlist — not yet held, or Screening — still evaluating)
3. Whether to run steps one at a time (pausing for review between each) or all at once

This determines the folder path for all outputs.

## Initiation Workflow

| Step | Action |
|------|--------|
| **1. Company Research** | Data collection (workflow handles analysis) |
| **2. Financial Model** | Data collection (workflow handles analysis) |
| **3. Valuation (DCF)** | Invoke skill `financial-analysis:dcf` |
| **4. Full Report** | Invoke skill `equity-research:initiating-coverage` |

## Detailed Instruction Map

| Task | Instructions |
|---|---|
| Step 1: Company Research | `step-1-company-research/` |
| Step 2: Financial Model | `step-2-financial-model/` |
| Step 3: DCF | `step-3-dcf/` |
| Step 4: Full Report | `step-4-full-report/` |
