---
description: Screen for equity ideas by type (Defensive / Core / Satellite)
argument-hint: "[equity type and/or criteria, e.g. 'Core, FCF compounder']"
---

Load the `equity-analysis-workflow` skill and run Phase 1 screening. If the argument does not specify an equity type (Defensive / Core / Satellite), ask the user which type they are hunting for before proceeding. Use the stated type and any additional criteria to set screening parameters, then invoke the underlying idea-generation workflow with the personal investor context.
