# Design

Memory Formation Skill is intentionally small. It gives coding agents a repeatable way to create and maintain project-specific memory without introducing a database, service, framework, or agent-specific dependency.

## Core Principle

Memory is not storage. Memory is selection.

A useful project memory system should preserve context that changes future behavior: current state, decisions, constraints, failed approaches, open questions, next steps, and lessons learned. It should not become a transcript, log archive, or duplicate copy of the repository.

Selection decides what deserves to survive. Organization decides where it belongs. Adaptation decides which structure fits the project as it evolves. Before writing, ask what future work would lose if the candidate were omitted; if nothing consequential would be lost, leave it out.

## Why Markdown

Markdown is:

- Easy for humans to read and edit.
- Easy for coding agents to inspect and update.
- Compatible with GitHub, GitLab, editors, and plain text tools.
- Versionable with normal code review.
- Portable across Codex, Claude Code, Cursor, and other agents.

The skill needs no database or generated index; its workflow runs through the agent's normal file access.

## Default Schema

The starting schema offers:

- `CURRENT_STATUS.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`
- `NEXT_STEPS.md`
- `LEARNINGS.md`

Choose only the files needed for the project's recurring handoff questions:

- What is true now?
- Why are things this way?
- What is unresolved?
- What should happen next?
- What should future agents avoid relearning?

## Schema Evolution

The schema is expected to change as the project changes. Early projects may need more assumptions and questions. Mature projects may need validation, release status, or operational notes. Research projects may need experiments, datasets, metrics, and reproducibility notes.

The rule is simple: add structure when it reduces future confusion; remove structure when it becomes empty, redundant, or misleading. Explain meaningful changes, move useful knowledge without duplicating it, and repair affected references. A new topic alone does not justify a new file.

The [frontend](../examples/frontend), [ML](../examples/ml-project), and [scientific](../examples/scientific-code) examples illustrate different selections of files and content. They are demonstrations, not a fixed taxonomy or evidence that schema changes improve performance.

## Memory Maintenance

The behavioral lifecycle is **candidate → evaluate → store/update → reuse → revise/deprecate**. Reconcile new evidence with the existing entry and any dependent status or next steps. Keep superseded knowledge only when its history still helps future work, with a clear replacement or explanation. Unresolved contradictions remain questions, not established facts.

For consequential entries, preserve enough context to distinguish a decision from an observation, experiment result, assumption, or open question. Record why it matters and the evidence or event behind it, including the conditions under which it applies. This can be a few bullets, not a mandatory metadata form.

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
- What evidence supports this, and does it still apply?

If an entry does not help with one of those questions, it probably does not belong in project memory.

These are design goals. See [Evaluating the idea](../README.md#evaluating-the-idea) for a proposed comparison; this repository does not establish a measured performance benefit.
