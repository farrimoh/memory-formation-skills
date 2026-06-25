# Learnings

## Project-Specific Lessons

### 2026-06-25

- Dashboard list render stability depends on filter option object identity.
- Memoizing rows did not fix the root cause because the list props still changed every render.

## Failed Approaches

- Approach: Memoize each dashboard row component.
  - Tried because: The profiler showed repeated row renders.
  - Result: Rows still re-rendered because the list received new filter option props.
  - Future guidance: Check parent prop identity before optimizing row internals.

## Gotchas

- Saved views depend on filter option ids and display order.

