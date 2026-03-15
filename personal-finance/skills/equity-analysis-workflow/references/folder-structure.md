# Folder Structure

**Always ask the user to confirm equity type and lifecycle stage before creating any files.**
This ensures outputs land in the correct folder.

```
/Equity-analyses/
  /Screening/                              ← Phase 1 outputs (equity type not yet determined)
    top-down-{SECTOR}-{YYYY-MM}.md         ← Phase 1 top-down: sector macro + ETF data (overwrite per session)
    bottom-up-{CRITERIA}-{YYYY-MM}.md      ← Phase 1 bottom-up: screen results (new file per run)
    events-{YYYY-MM}.md                    ← Phase 1 event-driven: catalyst calendar (overwrite per session)
  /Defensive/
    /Watchlist/        ← initiated, not yet held
    /Holding/          ← current positions
    /Closed/           ← exited positions
  /Core/
    /Watchlist/
    /Holding/
    /Closed/
  /Satellite/
    /Watchlist/
    /Holding/
    /Closed/

  /{Type}/{Stage}/{TICKER}/
    /Data/                                         ← data cache files (inputs to skills)
      company-research.md                          ← Phase 2 Step 1a (refresh: ~12 months / 10-K)
      financial-model.md                           ← Phase 2 Step 2 (refresh: ~3 months / earnings)
      comps.md                                     ← Phase 3 Step 1 (refresh: ~3 months)
      Q{N}-{YEAR}-pre-earnings.md                  ← Phase 5 pre-earnings (per event, archived)
      Q{N}-{YEAR}-earnings.md                      ← Phase 5 post-earnings (per event, archived)
      between-earnings.md                          ← Phase 5 between-earnings (overwritten each session)
      {YEAR}-annual-review.md                      ← Phase 5 annual review (per year, archived)
    /Initiation/
      company-research.md                          ← Phase 2 Step 1a
      competitive-analysis.md                      ← Phase 2 Step 1b (optional)
      financial-model.xlsx                         ← Phase 2 Step 2
      dcf-model.xlsx                               ← Phase 2 Step 3
      comps.xlsx                                   ← Phase 2 Step 4
      initiation-report.docx                       ← Phase 2 Step 5
    /Thesis/
      thesis-v1-{YYYY-MM}.md                       ← Phase 4 (increment version on major updates)
    /Reviews/
      {YYYY}-Q{N}-earnings-preview.md              ← Phase 5 pre-earnings report
      {YYYY}-Q{N}-earnings-update.md               ← Phase 5 post-earnings report
```

## Lifecycle transitions

- **Screening → Watchlist**: After Phase 2 initiation + Phase 4 thesis. Assign equity type (Defensive/Core/Satellite) at this point and create the ticker folder under the appropriate type.
- **Watchlist → Holding**: After buying. Move the folder; no file changes needed.
- **Holding → Closed**: After selling. Move the folder; add a closing note to the thesis file with exit rationale and date.
