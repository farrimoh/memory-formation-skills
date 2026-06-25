# Decisions

## Active Decisions

### Decision: Track Macro F1 And Per-Class Recall

- Date: 2026-06-25
- Context: Accuracy hid poor performance on rare routing classes.
- Decision: Use macro F1 and per-class recall as primary evaluation signals.
- Why: The product impact comes from missed rare classes, not only aggregate correctness.
- Alternatives considered: Accuracy, weighted F1.
- Consequences: Experiments must include a per-class metric table.

## Superseded Decisions

- 

