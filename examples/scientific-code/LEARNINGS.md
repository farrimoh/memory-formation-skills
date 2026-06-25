# Learnings

## Project-Specific Lessons

### 2026-06-25

- Small-step deterministic validation is stable with the new integrator.
- Long-run validation needs the same seed and timestep across old and new integrator comparisons.

## Failed Approaches

- Approach: Compare drift from different sweep configs.
  - Tried because: Existing outputs were available.
  - Result: Differences in seed and timestep made the comparison inconclusive.
  - Future guidance: Use paired configs before drawing conclusions.

## Gotchas

- Benchmark configs are treated as reproducibility fixtures; update them only with an explicit decision.

