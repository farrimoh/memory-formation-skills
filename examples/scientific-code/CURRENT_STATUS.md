# Current Status

## Snapshot

- Project: Particle simulation code for parameter sweep studies.
- Date: 2026-06-25
- Current focus: Verify energy conservation after integrator changes.
- Working state: Small deterministic runs complete and produce stable output files.
- Known broken state: Long runs still show energy drift above the expected tolerance.

## Active Context

- Branch or work area: integrator validation.
- Main files or modules involved: `src/integrators/`, `tests/validation/`, `configs/sweeps/`.
- Important constraints: Preserve reproducibility of published benchmark configurations.
- User priorities: Prefer physically meaningful validation over speed improvements.

## Recent Completed Work

- Added a deterministic short-run validation case.
- Confirmed the new integrator improves stability for small step sizes.

## Validation

- Checks run: deterministic short-run validation; existing unit tests.
- Passing: Unit tests and small-step validation.
- Failing: Long-run drift tolerance.
- Not yet verified: Sweep behavior across high-density configurations.

## Notes For Next Agent

- Resume by comparing long-run drift between old and new integrators using the same seed and timestep.

