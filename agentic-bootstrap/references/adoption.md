# Adoption guidance

Bootstrap prepares local changes for human review and commit. The ongoing work loop described here applies after adoption; do not execute it to publish or commit the bootstrap itself.

## Layout and stable identities

For a new convention, put ADRs in `docs/adr/`, specs in `docs/specs/`, and project memory in `docs/memory/`. Use `NNN-descriptive-slug.md` for ADR and spec documents, starting at `001`. Indexes, templates, and directory guides are not decision or spec documents and need no number.

Maintain separate ADR and spec number sequences. Within each root, allocate across subdirectories so references remain unambiguous. A growing product can use `docs/specs/001-product.md`, `capabilities/002-job-processing.md`, and `features/003-restart-recovery.md`; numbering does not encode execution order or hierarchy. Link parents explicitly.

Use the next number above the largest known or reserved ID, checking existing files and available indexes/history. Never reuse a retired ID or renumber published records. Continue past `999` without renaming earlier files. Preserve an established repository numbering scheme rather than imposing a second one.

Before creating a file, recheck availability. Where branches or contributors collide, resolve the unpublished draft's ID and its references during integration; never overwrite an existing document. This convention does not require parallel agents or a numbering service.

## Convert without losing context

- Map existing sources to their roles before moving them. A useful `decisions/` or `design/` directory is not defective because its name differs.
- Extend an existing `AGENTS.md` surgically. Preserve package-specific guidance, user edits, and supported compatibility files. Do not flatten distinct subprojects into one set of commands.
- For a requested migration, record old-to-new paths, preserve content and approval status, update internal references, and leave a forwarding note where a known external link would otherwise break. Avoid maintaining two editable authorities.
- Do not turn implementation archaeology into accepted ADRs. An observed choice can be documented as such, with evidence and unknown rationale, or proposed for present-day review.
- Adopt incrementally: document the next requested change, not every historical feature. Missing tests or uncertain commands should be visible gaps, not invented assurances.

## Minimum document contracts

A spec has seven body headings: Problem, Desired behavior, Scope, Non-goals, Constraints, Acceptance criteria, and Open questions. Add concise metadata for draft/approved intent, owner, its source, and parent links. Keep it readable in one sitting; about 200 lines is a diagnostic, not a target or permission to omit important intent. Put implementation detail elsewhere. New unresolved behavior choices remain questions, not defaults.

An ADR records one significant decision with date, proposed/accepted status, decision maker and source, context, decision, credible alternatives, and consequences. Record costs and revisit conditions where useful. Retain accepted history; a changed decision gets a new ADR linked to the superseded one. No ceremony is needed for every local implementation choice.

Human direction establishes intent, but ADR/spec documents need human review of their actual text before merge. Keep new ADRs Proposed and specs Draft until explicit human approval is recorded with the source and document revision. Agents may research, propose, validate and publish a reviewable PR; they cannot substitute their own review or passing checks for human approval. This gate includes editorial ADR/spec edits and mixed PRs. Changed reviewed content needs renewed review; unrelated code commits or adding the approval record without changing that content do not. Preserve historical status without inventing earlier human review. Ordinary code-only delivery remains autonomous.

Include document renames and deletions in that gate. After actual approval, updating Proposed to Accepted or Draft to Approved and recording its evidence does not require another review when the reviewed decision or requirements text is unchanged.

## Proportionate testing

Prefer adding or extending tests for new behavior. Use unit tests for meaningful logic and boundaries, integration/contract tests where a component boundary matters, and a small set of e2e tests for important user workflows through the application. Assert observable outcomes, including persistence or state transitions when relevant, rather than merely checking that a screen exists. Reuse the project's established tools; bootstrap records test commands and gaps rather than inventing an entire test stack.

For a bug, first capture a focused reproduction or regression test when practical. Verify that the same test fails for the original defect and passes after the fix, and record that evidence. Include relevant negative/boundary cases for invalid input or failure handling; one test may serve both regression and negative coverage. Do not claim a before/after result that was not run. If automation or reproduction is impractical, explain the limit and record the strongest available alternative evidence.

Choose the smallest test set that protects the behavior. Do not add tests for documentation-only edits, duplicate existing coverage, mirror implementation details, demand every layer for every feature, or chase an arbitrary coverage percentage. Run focused tests and required project checks; broaden only for changed behavior, failures, or a concrete unresolved risk.

## Project memory

Save a project memory when a verified fact contradicts a plausible instinct/assumption, or when substantial time or repeated attempts produce a reusable lesson. The value is avoiding a future wrong turn, not recording how much work happened. Use the [memory template](../assets/memory-template.md) for one short note per topic; update an existing note instead of duplicating it.

Record the tempting assumption or costly trap, the verified observation or resolution, a source/reproducible check, date, relevant environment, and when to revalidate it. Mention failed approaches only when they would otherwise be tempting to repeat. Separate any uncertain explanation from the observed fact; effort alone does not make a hypothesis true. Link tests, ADRs, or runbooks for the detailed evidence rather than copying them.

Memory must not contain secrets, session transcripts, speculative requirements, obvious facts, or copied task history. It cannot override human intent or repository instructions. Save qualifying lessons as part of the task, and refresh or retire stale notes when evidence changes; no separate approval or per-task memory entry is needed. This applies to project notes, not unrelated personal memory stores.

Execution progress belongs in the project's issue, PR, or task tracker. In the GitHub workflow, issues and PRs are the durable work log: record assignment, material blockers, review findings, verification, and completion there. Internal agent messages supplement that record. Add a local handoff only when continuity needs it; do not maintain a duplicate backlog in memory.

## Ongoing work loop

1. Before a slice, re-ground in the current request/comments and applicable product, capability, and feature specs, then relevant accepted decisions and interfaces. Read only the relevant branch of the spec tree; an unchanged revision need not be ritualistically reread. Continue authorized work autonomously while preserving the ADR/spec human-review gate before merge; ask for other material decisions/actions only when needed and continue unaffected work.
2. Name the observable result, acceptance criteria, and verification method. Prefer a vertical slice; permit a time-bounded spike or enabling change when it resolves a named uncertainty. A spike is evidence, not approval to ship its assumptions.
3. Implement and check against compiler, tests, runtime, and human feedback. Derive behavioral checks from approved examples and criteria, not just from the code being generated. Review important failure paths and applicable compatibility, migration, accessibility, security, or performance constraints.
4. If a discovery changes intended behavior, propose the smallest explicit spec change and obtain any missing human decision before depending on it. Otherwise route it to its durable home below. Editorial repairs, resolved questions, and links may keep a spec accurate without changing intent.
5. Review the diff and results against the criteria. Record which checks passed, failed, or were not run and why. In GitHub mode, the orchestrator posts findings and verifies fixes against the current head. For ADR/spec changes, finish this work before presenting the documents for human review; leave the PR open with auto-merge disabled until approval is recorded. Once applicable reviews and checks pass, merge using the shared owner account. A follow-up issue does not waive a failed criterion or missing document review.

| Discovery | Durable home |
| --- | --- |
| Intended behavior or binding product constraint | Spec, with human agreement for material changes |
| Significant architecture choice and trade-offs | ADR |
| API invariant | Schema or contract test |
| Behavioral edge case within agreed intent | Test |
| Operating procedure | Runbook |
| Local implementation detail | Code or a useful comment |
| Deployment setting | Configuration; link an ADR if rationale matters |
| Verified counterintuitive fact or reusable lesson from costly investigation | Evidence-backed memory note |

For relevant acceptance criteria, link tests or a reproducible manual check in the delivery evidence. Do not put command output, a growing test matrix, or a task checklist into the spec. Record actual validation limits rather than claiming simulator, mock, or unit evidence proves an untested production boundary.
