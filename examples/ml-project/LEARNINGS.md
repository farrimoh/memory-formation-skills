# Learnings

## Project-Specific Lessons

### 2026-06-25

- Class weighting increased minority recall but overcorrected billing-related predictions.
- Stratified validation split reduced metric noise compared with the previous random split.

## Failed Approaches

- Approach: Increase class weights globally.
  - Tried because: Minority classes had low recall.
  - Result: Billing precision dropped below the acceptable threshold.
  - Future guidance: Try threshold tuning or focal loss before larger model changes.

## Gotchas

- Validation reports must include the same label ordering as production routing rules.

