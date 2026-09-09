# Learnings

Illustrative memory entries; the report paths below describe evidence in the fictional project.

## Project-Specific Lessons

### 2026-06-29: Boundary Correction Validated At Standard Density

- Small-step deterministic validation is stable with the new integrator.
- Experiment result: Boundary v2 passes the long-run energy-drift tolerance at the original timestep; the v1 control fails with the same seed, density, and run length.
- Evidence: `reports/validation/paired-boundary-v2.md`, including paired configs and tolerance checks. High-density sweeps were not tested.
- Why retained: Long runs are expensive, and the result directs the next validation effort toward high-density behavior rather than repeating a timestep-only fix.
- Superseded assumption: Timestep sensitivity was the leading explanation for the observed drift. The paired boundary comparison supports a boundary-update defect for the tested configuration; it does not establish that timestep choice is irrelevant generally.

## Failed Approaches

- Approach: Compare drift from different sweep configs.
  - Tried because: Existing outputs were available.
  - Result: Differences in seed and timestep made the comparison inconclusive.
  - Future guidance: Use paired configs before drawing conclusions.

- Approach: Halve the timestep without changing boundary implementation v1.
  - Tried because: Timestep sensitivity was a plausible explanation for long-run drift.
  - Result: The long standard-density run still exceeded tolerance on 2026-06-25; see `reports/validation/timestep-v1.md` for the matched settings and results.
  - Why retained: Avoid an expensive repeat of the same unsuccessful configuration.
  - Future guidance: This failure applies to boundary v1. The 2026-06-29 result above supersedes the old working-state conclusion that long runs remain broken; reassess if boundary logic or simulation conditions change.

## Gotchas

- Benchmark configs are treated as reproducibility fixtures; update them only with an explicit decision.
