# Open Questions

Illustrative snapshot after the boundary correction; see [Learnings](LEARNINGS.md) for the evidence and its limits.

## Blocking Questions

- Question: Does corrected boundary handling keep high-density long runs within the energy-drift tolerance?
  - Why it matters: Standard-density validation is insufficient to resume the full parameter sweep.
  - Who or what can answer it: Paired high-density runs with the same seed, timestep, and run length across boundary implementations.
  - Current best assumption: Unverified; do not extrapolate the standard-density result.

## Non-Blocking Questions

- Should validation plots be committed as artifacts or generated only on demand?

## Resolved Questions

- Resolved 2026-06-29: The boundary update explained the tested standard-density drift. See the [paired result and superseded assumption](LEARNINGS.md#2026-06-29-boundary-correction-validated-at-standard-density).
