---
name: memory-formation
description: Create and maintain a project-specific Markdown memory system for long-running coding projects. Use when asked to initialize project memory, update memory at the end of a coding session, preserve durable project context, capture decisions and lessons learned, or help future coding agents resume work without reconstructing context from scratch.
---

# Memory Formation

Use this skill to create and update a lightweight project memory system. Memory is selective: preserve durable context that helps the next agent make better decisions, not a transcript of everything that happened.

## Memory Modes

Memory is elective. Do not assume every session should read or write project memory.

- `Memory off`: Do not read or write project memory unless the user explicitly asks. Use this for exploratory, private, noisy, or low-value sessions.
- `Read-only memory`: Read existing memory for context, but do not modify memory files.
- `Update memory`: Read existing memory when useful and update durable memory at the end of the session.
- `Initialize memory`: Create or restructure the project memory system.

Default to opt-in updates:

- Initialize memory only when requested.
- Update memory only when requested or when the repository has an explicit memory policy requiring end-of-session updates.
- Resume from memory only when requested or when the project workflow clearly names memory as the session state source.

Honor user control phrases:

- "Do not update memory this session."
- "Use memory read-only."
- "Update memory at the end."
- "Ignore project memory for this task."

If memory is off, do not create shadow notes, hidden summaries, or deferred memory updates. If memory is read-only, do not modify memory files. If the session produced a major durable change but memory updates are off, mention in the final response that memory was not updated.

## Workflow 0: Begin Session From Memory

Use this workflow only when the user asks to resume from memory or the repository has an explicit memory policy that makes memory the session state source.

1. Locate the project memory folder.
2. Read the current status, next steps, open questions, decisions, and learnings that are relevant to the requested task.
3. State the current goal, blocker if any, next action, and completed work that should not be repeated.
4. Continue from the recorded next action unless the user gives a newer instruction.
5. Do not update memory unless the session is also in `Update memory` mode.

## Workflow 1: Initialize Memory

1. Inspect the repository structure, package files, docs, tests, examples, and active branches if available.
2. Identify the project type, maturity, active work, risks, and likely future handoff needs.
3. Ask for missing project description or user priorities only when they cannot be inferred and would materially change the memory structure.
4. Select a memory schema using the process below.
5. Create a project memory folder. Prefer `memory/` unless the repo already has a convention such as `.agent/memory/`, `docs/memory/`, or `.ai/memory/`.
6. Populate initial memory files with project-specific facts, known unknowns, and clear next steps.
7. Do not invent progress, decisions, or constraints. Mark unknowns explicitly.

## Workflow 2: Update Memory

At the end of a session, update memory from the actual work performed.

1. Review changed files, commands run, test results, user decisions, failed approaches, and unresolved questions.
2. Update current status with the latest working state.
3. Move completed items out of next steps.
4. Add or revise decisions only when they are durable.
5. Record failed approaches when a future agent might plausibly retry them.
6. Capture lessons learned when they are project-specific and reusable.
7. Keep entries concise, dated when helpful, and tied to concrete files, features, experiments, or decisions.

## Memory Schema Selection Process

Start with the default schema:

- `CURRENT_STATUS.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`
- `NEXT_STEPS.md`
- `LEARNINGS.md`

Treat templates as starting points, not fixed forms. Personalize memory at three levels:

- Schema level: choose which memory files should exist.
- Section level: choose which headings each file should contain.
- Content level: choose what facts, decisions, failures, and next steps are worth preserving.

Then adapt the schema to the project:

1. Determine the dominant work type:
   - Frontend or product UI: consider `UI_STATE.md`, `DESIGN_DECISIONS.md`, or `KNOWN_ISSUES.md` if the default files become crowded.
   - Backend or platform: consider `INTEGRATIONS.md`, `API_CONTRACTS.md`, or `OPERATIONS.md`.
   - ML or data: consider `EXPERIMENTS.md`, `DATASETS.md`, or `METRICS.md`.
   - Scientific code: consider `ASSUMPTIONS.md`, `VALIDATION.md`, or `REPRODUCIBILITY.md`.
2. Determine project maturity:
   - Early exploration: favor open questions, assumptions, and next steps.
   - Active implementation: favor current status, decisions, and known issues.
   - Stabilization: favor validation, release status, and regression risks.
3. Determine handoff risk:
   - If future agents must understand why a path was chosen, emphasize decisions.
   - If future agents must reproduce results, emphasize commands, environment assumptions, and validation.
   - If future agents must continue a queue of work, emphasize next steps and blockers.
4. Adapt file sections:
   - Keep only headings that help future agents resume work.
   - Add project-specific headings when repeated context would otherwise be scattered.
   - Remove placeholder headings that do not fit the project.
   - Prefer precise project language over generic template labels.
5. Keep the schema as small as possible. Add a file or section only when it reduces confusion or prevents an existing file from becoming a mixed-purpose log.

## What To Remember

Remember:

- The current state of the project and active work.
- User priorities, constraints, and definitions of success.
- Durable architecture, product, workflow, research, or implementation decisions.
- Why important decisions were made, including rejected alternatives.
- Failed approaches that are non-obvious or likely to be retried.
- Open questions, blockers, and dependencies.
- Next steps that let another agent resume efficiently.
- Project-specific conventions, gotchas, and lessons learned.
- Validation status: what was tested, what passed, what failed, and what remains unverified.

## What Not To Remember

Do not remember:

- Full chat transcripts or step-by-step session logs.
- Generic facts the agent can infer from the codebase.
- Temporary thoughts that do not affect future work.
- Secrets, tokens, credentials, private URLs, or personal data.
- Absolute local filesystem paths in committed memory files.
- Large command outputs unless summarized into durable conclusions.
- Speculation presented as fact.
- Completed tasks that no longer matter unless they explain current state or future decisions.

## End-Of-Session Update Checklist

Before ending a session, update memory with:

- Current status: What works now? What is partially done? What is broken?
- Completed work: What changed in durable terms?
- Decisions: What was decided, by whom if relevant, and why?
- Failed approaches: What was tried and should not be retried blindly?
- Open questions: What still needs user input, research, or validation?
- Next steps: What should the next agent do first?
- Lessons learned: What project-specific insight will save time later?
- Validation: What tests, builds, checks, or manual verification were run?

If nothing durable changed, say so in `CURRENT_STATUS.md` or leave memory unchanged.

## When To Change The Memory Structure

Change the memory structure when the current files no longer match the project's shape.

Add a file when:

- One file is accumulating unrelated kinds of memory.
- A project domain needs repeated specialized tracking, such as experiments, datasets, API contracts, or validation runs.
- Future work depends on a category of context that is easy to lose.

Remove or merge a file when:

- It is empty after multiple sessions.
- Its contents duplicate another memory file.
- The project phase has ended and the content can be summarized elsewhere.

Rename a file when:

- The name no longer reflects how the project uses it.
- A more specific name would help future agents find the right context faster.

When changing structure:

1. Preserve useful existing content.
2. Add a short note in `CURRENT_STATUS.md` or `DECISIONS.md` explaining the change.
3. Update any index or README inside the memory folder if one exists.
4. Prefer repo-relative paths and stable project terms.

## Small Update Example

Before session:

```markdown
# Open Questions

- Why does the dashboard list re-render after each filter change?
```

After session:

```markdown
# Open Questions

- Should the export modal use the same memoized filter options, or does it need a separate data boundary?
```

```markdown
# Learnings

## 2026-06-25

- The dashboard list re-render came from recreating filter options in the parent component.
- Memoizing rows did not fix the root cause because the list props still changed every render.
```
