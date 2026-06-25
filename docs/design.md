# Design

Memory Formation Skill is intentionally small. It gives coding agents a repeatable way to create and maintain project-specific memory without introducing a database, service, framework, or agent-specific dependency.

## Core Principle

Memory is not storage. Memory is selection.

A useful project memory system should preserve context that changes future behavior: current state, decisions, constraints, failed approaches, open questions, next steps, and lessons learned. It should not become a transcript, log archive, or duplicate copy of the repository.

## Why Markdown

Markdown is:

- Easy for humans to read and edit.
- Easy for coding agents to inspect and update.
- Compatible with GitHub, GitLab, editors, and plain text tools.
- Versionable with normal code review.
- Portable across Codex, Claude Code, Cursor, and other agents.

The skill avoids databases and generated indexes because v1 should work in any repository without setup.

## Default Schema

The default schema is:

- `CURRENT_STATUS.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`
- `NEXT_STEPS.md`
- `LEARNINGS.md`

These files cover the minimum recurring handoff needs in long-running coding projects:

- What is true now?
- Why are things this way?
- What is unresolved?
- What should happen next?
- What should future agents avoid relearning?

## Schema Evolution

The schema is expected to change as the project changes. Early projects may need more assumptions and questions. Mature projects may need validation, release status, or operational notes. Research projects may need experiments, datasets, metrics, and reproducibility notes.

The rule is simple: add structure when it reduces future confusion; remove structure when it becomes empty, redundant, or misleading.

## Agent-Agnostic Behavior

The skill avoids relying on one agent's command syntax, memory feature, or file convention. Any coding agent can implement the workflow by reading `SKILL.md`, inspecting the repository, and updating Markdown files.

## Non-Goals

- No database.
- No web service.
- No required CLI.
- No framework dependency.
- No hidden agent state.
- No exhaustive session logging.
- No replacement for source code, tests, issues, or project documentation.

## Quality Bar

A good memory update should help a future agent answer:

- What changed?
- What matters now?
- What should I do next?
- What should I avoid retrying?
- What did the user care about?
- What remains uncertain?

If an entry does not help with one of those questions, it probably does not belong in project memory.

