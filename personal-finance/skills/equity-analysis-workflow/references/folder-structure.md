# Folder Structure

**Always ask the user to confirm equity type and lifecycle stage before creating any files.**
This ensures outputs land in the correct folder.

```
/Equity-analyses/
  /Screening/                                      ← Phase 1 outputs (equity type not yet determined)
    /Data/                                         ← Phase 1 raw data cache files
      {YYYY-MM-DD}-top-down-{SECTOR}.md               ← top-down data cache (written from data-file-template.md)
      {YYYY-MM-DD}-bottom-up-{CRITERIA}.md            ← bottom-up data cache
      {YYYY-MM-DD}-events.md                          ← event-driven data cache
    {YYYY-MM-DD}-top-down-{SECTOR}-report.md          ← Phase 1 top-down: polished screening report (output of equity-research:sector)
    {YYYY-MM-DD}-bottom-up-{CRITERIA}-report.md       ← Phase 1 bottom-up: polished screening report (output of equity-research:screen)
    {YYYY-MM-DD}-events-report.md                     ← Phase 1 event-driven: polished report (output of equity-research:catalysts)
    /_archived/                                    ← ignored/superseded screening cache files
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
    /Data/                                         ← data files (caches) (inputs to skills)
      company-research.md                          ← Phase 2 Step 1a (refresh: ~12 months / 10-K)
      financial-model.md                           ← Phase 2 Step 2 (refresh: ~3 months / earnings)
      comps.md                                     ← Phase 3 Step 1 (refresh: ~3 months)
      {YEAR}-Q{N}-pre-earnings.md                  ← Phase 5 pre-earnings (per event, archived)
      {YEAR}-Q{N}-earnings.md                      ← Phase 5 post-earnings (per event, archived)
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
      {YYYY-MM-DD}-thesis-v1.md                       ← Phase 4 (increment version on major updates)
    /Reviews/
      {YYYY}-Q{N}-earnings-preview.md              ← Phase 5 pre-earnings report
      {YYYY}-Q{N}-earnings-update.md               ← Phase 5 post-earnings report
    /_archived/                                    ← ignored/superseded files
```

## Lifecycle transitions

- **Screening → Watchlist**: After Phase 2 initiation + Phase 4 thesis. Assign equity type (Defensive/Core/Satellite) at this point and create the ticker folder under the appropriate type.
- **Watchlist → Holding**: After buying. Move the folder; no file changes needed.
- **Holding → Closed**: After selling. Move the folder; add a closing note to the thesis file with exit rationale and date.
