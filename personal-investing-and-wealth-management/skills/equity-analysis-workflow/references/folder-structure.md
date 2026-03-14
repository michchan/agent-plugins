# Folder Structure

**Always ask the user to confirm equity type and lifecycle stage before creating any files.**
This ensures outputs land in the correct folder.

```
/Equity-analyses/
  /Defensive/
    /Screening/        ← Phase 1 screening outputs
    /Watchlist/        ← initiated, not yet held
    /Holding/          ← current positions
    /Closed/           ← exited positions
  /Core/
    /Screening/
    /Watchlist/
    /Holding/
    /Closed/
  /Satellite/
    /Screening/
    /Watchlist/
    /Holding/
    /Closed/

  /{Type}/{Stage}/{TICKER}/
    {TICKER}-data.md                       ← Phase 2 data cache (Step 0 output)
    /Initiation/
      company-research.md                  ← Phase 2 Task 1
      competitive-analysis.md              ← Phase 2 Task 1b (optional)
      financial-model.xlsx                 ← Phase 2 Task 2
      dcf-model.xlsx                       ← Phase 2 Task 3
      comps.xlsx                           ← Phase 2 Task 4
      initiation-report.docx               ← Phase 2 Task 5
    /Thesis/
      thesis-v1-{YYYY-MM}.md               ← Phase 4 (increment version on major updates)
    /Reviews/
      {YYYY}-Q{N}-earnings-preview.md      ← Phase 5 pre-earnings
      {YYYY}-Q{N}-earnings-update.md       ← Phase 5 post-earnings
```

## Lifecycle transitions

- **Screening → Watchlist**: After Phase 2 initiation + Phase 4 thesis. Stock clears your bar but you haven't bought yet.
- **Watchlist → Holding**: After buying. Move the folder; no file changes needed.
- **Holding → Closed**: After selling. Move the folder; add a closing note to the thesis file with exit rationale and date.
