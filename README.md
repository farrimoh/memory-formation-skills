# Memory Formation Skill

This skill automatically generates and maintains a project-specific memory system so coding agents can resume work without reconstructing context from scratch.

It is a minimal, Markdown-based workflow for Codex, Claude Code, Cursor, and other coding agents working on long-running software projects. The goal is not to store everything. The goal is to help the agent decide what deserves to be remembered for this project.

## What It Does

- Initializes a project memory folder after inspecting the repository, docs, priorities, and active work.
- Selects a lightweight memory schema that fits the project instead of forcing one universal structure.
- Adapts files, sections, and content to the project instead of copying templates blindly.
- Updates memory at the end of a session with status, completed work, decisions, failed approaches, open questions, next steps, and lessons learned.
- Keeps memory in plain Markdown so it can be reviewed, edited, committed, copied, or ignored like any other project file.

## Repository Layout

```text
skills/memory-formation/SKILL.md
templates/
  CURRENT_STATUS.md
  DECISIONS.md
  OPEN_QUESTIONS.md
  NEXT_STEPS.md
  LEARNINGS.md
examples/
  frontend/
  ml-project/
  scientific-code/
docs/design.md
```

## Quick Start

Ask your coding agent to use the skill:

```text
Use the memory-formation skill to initialize project memory for this repository.
```

The agent should:

1. Inspect the repository structure and existing docs.
2. Ask for or infer the project description and user priorities.
3. Choose an appropriate Markdown memory schema.
4. Create a project memory folder, usually `memory/` or `.agent/memory/`.
5. Populate the initial files with project-specific context.

At the end of a work session, ask:

```text
Use the memory-formation skill to update project memory for this session.
```

The agent should update only durable, useful context. It should not create a transcript of the session.

## Default Memory Files

The default schema uses:

- `CURRENT_STATUS.md`: current project state, active branch/work, known constraints.
- `DECISIONS.md`: durable architectural, product, workflow, or research decisions.
- `OPEN_QUESTIONS.md`: unresolved questions blocking or shaping future work.
- `NEXT_STEPS.md`: ordered follow-up tasks and recommended resume path.
- `LEARNINGS.md`: lessons, failed approaches, gotchas, and project-specific heuristics.

Agents may add, remove, or rename files when the project needs a different shape. See `skills/memory-formation/SKILL.md` for the selection and evolution rules.

The templates are starting points. The skill asks the agent to reason about the project first, then choose the files, headings, and remembered details that are actually relevant.

## Before And After Example

Before a session, `NEXT_STEPS.md` might say:

```markdown
# Next Steps

1. Investigate why the dashboard list re-renders after every filter change.
2. Add a regression test once the cause is known.
```

After the session, the agent updates memory:

```markdown
# Next Steps

1. Add a focused regression test for filter changes in the dashboard list.
2. Profile the export modal separately; it still has unrelated render spikes.
```

And records the learning:

```markdown
# Learnings

## 2026-06-25

- The dashboard list re-render was caused by recreating the filter options array in the parent component.
- Memoizing the options at the data boundary fixed the issue; memoizing individual rows did not.
```

The useful result is preserved, but the full debugging transcript is not.

## What Should Be Remembered

Remember durable context that will save future work:

- Current state and known constraints.
- Decisions and why they were made.
- Failed approaches that are likely to be retried.
- Project-specific conventions.
- Open questions and blockers.
- Next steps with enough detail to resume.
- Lessons learned from bugs, experiments, performance work, or integrations.

Do not remember:

- Full chat transcripts.
- Temporary command output unless it explains a durable fact.
- Secrets, tokens, credentials, or private local paths.
- Vague summaries like "worked on frontend."
- Information already obvious from source files unless the reasoning behind it matters.

## Design Principles

- Markdown first.
- Project-specific over universal.
- Selective memory over exhaustive logging.
- Agent-agnostic instructions.
- No database, server, framework, or runtime dependency.

See `docs/design.md` for more detail.
