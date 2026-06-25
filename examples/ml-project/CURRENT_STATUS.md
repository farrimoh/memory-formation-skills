# Current Status

## Snapshot

- Project: Text classification model for support ticket routing.
- Date: 2026-06-25
- Current focus: Improve minority-class recall without reducing macro F1.
- Working state: Baseline transformer model trains and evaluates reproducibly.
- Known broken state: Class weighting improved recall but reduced precision too much for billing-related tickets.

## Active Context

- Branch or work area: experiment tracking and evaluation.
- Main files or modules involved: `training/`, `evaluation/`, `configs/`.
- Important constraints: Report macro F1 and per-class recall; do not optimize only aggregate accuracy.
- User priorities: Prefer reproducible experiments over one-off metric gains.

## Recent Completed Work

- Added a stratified validation split.
- Compared baseline loss to weighted loss.

## Validation

- Checks run: training smoke run; evaluation on validation split.
- Passing: Baseline metrics reproduce within expected variance.
- Failing: Weighted loss does not meet precision constraints.
- Not yet verified: Focal loss and threshold tuning.

## Notes For Next Agent

- Resume by testing threshold tuning before changing the model architecture.

