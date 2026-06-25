# Open Questions

## Blocking Questions

- Question: Is the long-run energy drift caused by timestep size or the boundary condition update?
  - Why it matters: The next fix depends on whether the integrator or boundary logic is responsible.
  - Who or what can answer it: Paired old/new integrator runs with identical seeds and timestep sweeps.
  - Current best assumption: Timestep sensitivity is the most likely cause.

## Non-Blocking Questions

- Should validation plots be committed as artifacts or generated only on demand?

## Resolved Questions

- 

