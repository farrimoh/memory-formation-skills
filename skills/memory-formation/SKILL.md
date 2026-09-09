---
name: memory-formation
description: Create and maintain a project-specific Markdown memory system for long-running coding projects. Use when asked to initialize project memory, update memory at the end of a coding session, preserve durable project context, capture decisions and lessons learned, or help future coding agents resume work without reconstructing context from scratch.
---

# Memory Formation

Use this skill to create, reuse, and update lightweight project memory. Memory formation means deciding what deserves to become durable project knowledge. Reason before writing: preserve knowledge that helps future work, not a transcript or compressed account of everything that happened.

## Scope And Decision Records

This skill selects knowledge for future work; it does not define approval boundaries or obtain authorization for implementation. A decision worth remembering may be a routine technical choice, a user decision, or an outcome recorded by a separate collaboration protocol.

If the project also uses `keep-me-in-the-loop`, its policy and decision log own approval boundaries and human decision status. Retain only the durable rationale or implications needed in memory, referencing the original entry by repo-relative path and decision ID instead of copying its proposal and approval history. Preserve whether a proposal is accepted, rejected, deferred, or pending; a memory entry is not evidence of approval. Neither skill requires the other.

## Workflow 1: Initialize Memory

1. Inspect existing project memory, repository structure, package files, docs, tests, examples, and active branches if available. Reuse an established memory location rather than creating a parallel set of notes.
2. Identify the project type, maturity, active work, risks, and likely future handoff needs.
3. Ask for missing project description or user priorities only when they cannot be inferred and would materially change the memory structure.
4. Select a memory schema using the process below.
5. Create a project memory folder. Prefer `memory/` unless the repo already has a convention such as `.agent/memory/`, `docs/memory/`, or `.ai/memory/`.
6. Apply the memory decision rule below before populating files with project-specific facts, consequential unknowns, and clear next steps. Create only the files that need content.
7. Do not invent progress, decisions, or constraints. Mark unknowns explicitly.

## Workflow 2: Update Memory

At the end of a session, update memory from the actual work performed.

1. Review changed files, commands run, test results, user decisions, failed approaches, and unresolved questions.
2. Evaluate candidates using the memory decision rule before storing anything. Compare them with existing memory and project docs; update the authoritative entry or link to it instead of duplicating it.
3. Update current status with the latest working state and move completed items out of next steps. Preserve completed work only if it still explains current state or future decisions.
4. Add or revise durable decisions, reusable learnings, and failed approaches a future agent might plausibly retry. Include useful provenance for consequential entries.
5. Reconcile affected memory with new evidence. Revise, remove, or explicitly supersede outdated claims and update dependent status, questions, and next steps. If evidence conflicts without resolving the issue, mark the uncertainty instead of silently choosing a claim.
6. Check whether the current structure still fits the knowledge being retained. Apply the structure-change rules below when there is a concrete mismatch.
7. Keep entries concise, dated when helpful, and tied to concrete files, features, experiments, or decisions. If nothing durable changed, leave memory unchanged.

## Workflow 3: Resume From Memory

1. Read the project's current-state summary and the memory relevant to the task before choosing an approach. Follow references to decisions, findings, and constraints as needed.
2. Check whether consequential claims still apply to the current repository and task, using their recorded scope and available evidence. Do not rerun expensive validation merely to rediscover a supported finding. Treat assumptions and open questions as uncertain.
3. Use applicable knowledge to guide the next action and avoid repeating a validated failure under the same conditions. New conditions or evidence may justify revisiting it.
4. Correct affected stale memory when discovered, using the update workflow. Memory records project knowledge; it does not override the user's current instructions.

## Memory Decision Rule

For each candidate, ask: **Will this help future work, and what would be lost if it were omitted?** Retain it only when it is likely to matter in future sessions and has a concrete reason: expensive rediscovery, a decision or constraint to respect, a validated learning, an important failure to avoid repeating, necessary current state, or prevention of a likely mistake.

Use the smallest useful entry in the appropriate existing location. If code or maintained documentation already represents it adequately, omit it or keep only a reference and the non-obvious implication. Do not store an item merely because it happened this session. Consequential assumptions and open questions can qualify, but must remain explicitly uncertain.

Memory follows a lightweight lifecycle: **candidate → evaluate → store/update → reuse → revise/deprecate**. It is not append-only. Keep a superseded entry only when its history still explains future work; label it clearly and point to the replacement so it cannot be mistaken for active guidance.

## Provenance For Consequential Knowledge

In plain language, identify the kind of knowledge (decision, observation, experiment result, assumption, or open question), why it is worth retaining, and the evidence or project event behind it. Use a repo-relative report, test, config, commit, or user decision reference when available. Do not invent evidence; state when it is unavailable or unverified.

Include the conditions that limit a finding, such as dataset version, configuration, or validation scope. When superseding knowledge, explain what changed and which evidence supports the replacement. A few sentences or bullets suffice; do not require a metadata form for every entry or collect raw event logs.

## Memory Schema Selection Process

Consider the default schema, selecting only the files the project needs:

- `CURRENT_STATUS.md`
- `DECISIONS.md`
- `OPEN_QUESTIONS.md`
- `NEXT_STEPS.md`
- `LEARNINGS.md`

Treat templates as starting points, not fixed forms; project types below are examples, not a closed taxonomy. This workflow is self-contained and does not require template files to be installed. Personalize memory at three levels:

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

Candidates to evaluate with the decision rule:

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
- Routine implementation details and transient debugging issues that do not affect future work.
- Unadopted speculative ideas without a consequential open question or assumption.
- Redundant knowledge already adequately represented in memory or maintained project docs.
- Secrets, tokens, credentials, private URLs, or personal data.
- Absolute local filesystem paths in committed memory files.
- Raw logs or large command outputs; retain only qualifying conclusions and references to evidence.
- Speculation presented as fact.
- Completed tasks that no longer matter unless they explain current state or future decisions.

## End-Of-Session Update Checklist

Before ending a session, check for consequential changes in these areas. These are review prompts, not mandatory entries:

- Current status: What works now? What is partially done? What is broken?
- Completed work: What changed in durable terms?
- Decisions: What was decided, by whom if relevant, and why?
- Failed approaches: What was tried and should not be retried blindly?
- Open questions: What still needs user input, research, or validation?
- Next steps: What should the next agent do first?
- Lessons learned: What project-specific insight will save time later?
- Validation: What tests, builds, checks, or manual verification were run?

Do not add a session marker or rewrite status just to show that this checklist was reviewed.

## When To Change The Memory Structure

During updates, notice when the current files no longer match the project's shape. Prefer an existing section when it is sufficient; do not restructure for a one-off topic or stylistic preference.

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

1. Identify the concrete mismatch and how the proposed structure will improve retrieval or maintenance. Make the smallest change that addresses it.
2. Move useful existing content to its new home without leaving duplicate active entries. Add a short note in `CURRENT_STATUS.md`, `DECISIONS.md`, or the existing equivalent explaining the reason and where the content moved.
3. Update affected references, including any index or README inside the memory folder if one exists.
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
