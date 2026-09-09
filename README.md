# Memory Formation Skill

When a coding-agent session ends, what should a future agent inherit, and what should be allowed to disappear? Returning agents need decisions, constraints, and findings that still matter. Session history can explain what happened without making that knowledge easy to find or use.

**Memory formation is deciding what deserves to become durable project knowledge—not simply storing or summarizing previous context.**

- **History/context:** what happened.
- **Compaction/summarization:** a compressed representation of what happened.
- **Memory formation:** deciding what is important enough to survive.
- **Memory structure/schema:** deciding where different kinds of durable knowledge belong.

This skill is a small, inspectable Markdown protocol for long-running software projects. It guides three decisions: **selection** (what to retain), **organization** (where it belongs), and **adaptation** (which structure fits this project as it evolves). The goal is selective retention that improves future agent behavior without accumulating unnecessary context. Existing project notes can serve as memory; the skill supplies a selection and maintenance protocol.

[Install](#install) · [Quick start](#quick-start) · [Project-specific memory](#project-specific-memory) · [Evaluating the idea](#evaluating-the-idea)

## What It Does

- Initializes a project memory folder after inspecting the repository, docs, priorities, and active work.
- Selects and adapts files, sections, and content to fit the project instead of copying templates blindly.
- Selects consequential status, decisions, findings, and next steps for memory, leaving transient details out.
- Reads relevant memory when resuming work, checks whether it still applies, and updates or deprecates stale knowledge.
- Keeps memory in plain Markdown so it can be reviewed, edited, committed, copied, or ignored like any other project file.

## Project-Specific Memory

The existing examples deliberately retain different kinds of knowledge:

| Example | Memory files | Why this shape fits the work |
| --- | --- | --- |
| [Frontend](examples/frontend) | Current status, learnings, next steps | A bounded performance fix needs the cause, compatibility constraints, and a clear follow-up queue. |
| [ML project](examples/ml-project) | Current status, decisions, learnings | Experiment choices depend on evaluation priorities and prior failures, so their rationale needs a durable home. |
| [Scientific code](examples/scientific-code) | Current status, learnings, open questions | Validation scope and unresolved scientific explanations shape the next experiment. |

These are starting points and demonstrations, not a fixed taxonomy. An ML project may later need dataset versions, leakage risks, or model artifact references; research may need assumptions and validation records; product work may need interfaces, constraints, or migrations. The agent reasons about the actual repository.

When recurring knowledge has no suitable home, a category becomes misleading, or project goals change, reconsider the schema. Prefer an existing section where it suffices. A meaningful change needs a concrete reason, preservation of useful content, and updated references.

## Install

Packaged for Codex and Claude Code, with a portable skill directory for Hermes Agent and other compatible clients. Installation makes the skill available; it does not create project memory automatically.

### Codex

Run in your terminal:

```bash
codex plugin marketplace add farrimoh/memory-formation-skills
codex plugin add memory-formation@memory-formation
```

Start a new session, then use the prompt below. See the [official plugin documentation](https://developers.openai.com/plugins/build/plugins) for marketplace setup and desktop installation options.

### Claude Code

Run inside Claude Code:

```text
/plugin marketplace add farrimoh/memory-formation-skills
/plugin install memory-formation@memory-formation
```

For a local preview, run `claude --plugin-dir .` at the repository root. See the [Claude Code plugin documentation](https://code.claude.com/docs/en/plugins-reference).

### Hermes Agent

Run in your terminal:

```bash
hermes skills tap add farrimoh/memory-formation-skills
hermes skills install farrimoh/memory-formation-skills/memory-formation
```

See the [Hermes skills documentation](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills).

### Other Compatible Clients

Install the complete [skills/memory-formation](skills/memory-formation) directory using your client's native skill installer, or point the agent at its `SKILL.md`. The skill is self-contained; repository templates and examples are optional references.

## Quick Start

Open the project you want to work on and ask:

```text
Use the memory-formation skill to initialize project memory for this repository.
```

The agent should:

1. Inspect the repository structure and existing docs.
2. Ask for or infer the project description and user priorities.
3. Choose an appropriate Markdown memory schema.
4. Create a project memory folder, usually `memory/` or `.agent/memory/`.
5. Populate only the files needed for selected durable knowledge, reusing existing project memory where available.

To resume work, ask the agent to use the skill to read relevant project memory and check it against the current repository and task.

At the end of a work session, ask:

```text
Use the memory-formation skill to update project memory for this session.
```

The agent should update only durable, useful knowledge. These are agent instructions, not a background service; memory must be read and updated during the agent's workflow.

## Default Memory Files

The starting schema offers:

- `CURRENT_STATUS.md`: current project state, active branch/work, known constraints.
- `DECISIONS.md`: durable architectural, product, workflow, or research decisions.
- `OPEN_QUESTIONS.md`: unresolved questions blocking or shaping future work.
- `NEXT_STEPS.md`: ordered follow-up tasks and recommended resume path.
- `LEARNINGS.md`: lessons, failed approaches, gotchas, and project-specific heuristics.

Use only the files and headings the project needs. See the [templates](templates) and the [skill's selection and evolution rules](skills/memory-formation/SKILL.md).

## What Should Be Remembered

Before writing, ask: **Will this help future work, and what would be lost if it were omitted?** Retain information likely to matter again when it is expensive to rediscover, constrains a decision, records a validated learning or important failure, explains current state, or prevents a likely mistake.

Usually leave out transient debugging details, raw logs, routine implementation details, facts easily reconstructed from code, unadopted speculation, and redundant information. Link to existing evidence or documentation instead of copying it. Never retain secrets or private local paths.

## Memory Has A Lifecycle

**candidate → evaluate → store/update → reuse → revise/deprecate**

Memory is not append-only. Update the existing entry when knowledge changes; remove or mark obsolete guidance so conflicting instructions do not accumulate. Keep a short superseded note only when it still explains a consequential decision.

For consequential knowledge, keep enough provenance to show its kind (decision, observation, experiment result, assumption, or open question), why it matters, and the evidence or project event behind it. A short sentence and a repo-relative reference can be enough; no event database is needed.

## Worked Example

The [scientific example](examples/scientific-code) shows the memory left after these illustrative sessions. Report paths and results describe a fictional simulation project, not experiments run in this repository.

1. **Select and store.** A long-run experiment finds that halving the timestep still fails the energy-drift tolerance with boundary implementation v1. Repeating the run is expensive, and the result constrains the next investigation. The agent records the conditions and report reference in `LEARNINGS.md`, while leaving the cause uncertain in `OPEN_QUESTIONS.md`. A temporary output-directory error is fixed and intentionally omitted from memory.
2. **Reuse.** A fresh agent considers another timestep-only fix. It reads the finding and investigates the boundary update instead of repeating the same failed configuration.
3. **Revise.** Paired runs with corrected boundary handling pass at the original timestep. The agent replaces the stale failure status, marks the timestep explanation as superseded, and retains the old failure only with its v1 scope. High-density behavior remains an open question. The existing three files still fit, so no schema change is needed.

## Evaluating The Idea

Selective, adaptive memory formation is an **evaluable design hypothesis**, not a demonstrated performance improvement. Compare the same project tasks over several sessions with:

| Condition | Memory available to the agent |
| --- | --- |
| A. No persistent project memory | Repository and ordinary project artifacts, without added memory |
| B. Fixed/conventional project memory | A fixed set of project notes maintained with routine session summaries |
| C. Selective, adaptive memory formation | This skill's selection, revision, provenance, and schema evolution rules |

Then give fresh agents the resulting repository and permitted memory, without the prior conversations. Ask: Why did we choose X? What approach already failed? Which assumptions constrain the solution? What should happen next? What evidence established this constraint?

Measure recall of consequential knowledge, stale-memory errors, repeated work, irrelevant retained information, context/token cost (including maintenance), and downstream task success. Keep model, tools, tasks, and budgets comparable, and judge answers against project evidence. Conventional notes can already be selective; define that baseline clearly before attributing any difference to this protocol.

No benchmark or performance results are included here.

## Design Principles

- Markdown first.
- Project-specific over universal.
- Selective memory over exhaustive logging.
- Agent-agnostic instructions.
- No database, server, framework, or runtime dependency.

See [docs/design.md](docs/design.md) for more detail. Plugin manifests live in `.codex-plugin/` and `.claude-plugin/`; marketplace entries live in `.agents/plugins/marketplace.json` and `.claude-plugin/marketplace.json`.

## Contributing

Keep changes focused and examples portable. Use repo-relative paths or clear placeholders, and keep shared plugin metadata consistent across both manifests. Before submitting, check JSON/YAML syntax, relative Markdown links, and `git diff --check`. If Claude Code is installed, run `claude plugin validate .`. For behavior changes, describe a realistic task and the expected memory selection and update.

## License

[Apache License 2.0](LICENSE).
