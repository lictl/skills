# Project guidance

<!-- Adapt this template; replace {{...}} with verified facts or explicit unknowns, and remove comments. Keep existing project rules that remain applicable. -->

## Project map

{{One paragraph describing the project and links to its main entry points.}}

- Specs: {{spec directory or index}}
- Decisions: {{ADR directory or index}}
- Project memory: {{memory directory or index; read relevant notes only}}
- Current work and delivery evidence: {{existing issue, PR, or handoff convention}}

## Commands

{{List supported setup, build, and focused test commands with working directories and prerequisites. Distinguish commands verified here from commands found in documentation but not run. If no project exists yet, say commands are not established.}}

## Working agreement

- Before each slice, check the current request, applicable parent and feature specs, relevant accepted ADRs, and interfaces. Reuse unchanged context; check revisions when work resumes.
- Humans direct intent through chat or comments. Continue implementation, agent review, and merge autonomously within that scope; no routine document or PR sign-off is required. Ask only for an actual blocker, material intent decision, or necessary human action, and continue unaffected work. Record agent-made technical decisions honestly.
- Parent specs constrain child specs. Accepted ADRs constrain architecture. Tests, code, and runtime show implemented behavior. Memory is fallible context. Surface conflicts instead of silently choosing a convenient authority.
- Keep specs compact: problem, desired behavior, scope, non-goals, constraints, acceptance criteria, open questions. Put decisions in ADRs and executable constraints in tests, types, schemas, or configuration.
- Work in independently verifiable slices, preferably a thin observable behavior. Use bounded experiments to resolve implementation uncertainty. Continue unaffected work while material questions remain open.
- Connect completion claims to acceptance criteria and actual evidence. Report failed or unrun checks and environmental limits. Do not weaken a check merely to obtain a passing result.
- Prefer focused feature tests: unit tests for logic, e2e tests for important user workflows, and boundary tests where needed. For bugs, add a regression test that fails before the fix and passes after when practical, including relevant negative cases. Reuse existing coverage; avoid redundant tests, implementation-mirroring assertions, and tests for documentation-only edits. Not every change needs every test layer.
- Save project memory for verified counterintuitive facts or reusable lessons from substantial investigation. Capture the mistaken assumption/trap, finding or fix, evidence, and revalidation context. Skip routine progress, obvious facts, and duplicated explanations; update or retire stale notes.

## Local constraints

{{Only project-specific facts that affect decisions: compatibility requirements, generated files, data handling, required environments, or relevant operational boundaries. Link longer explanations.}}

## Commit messages

Git history is part of the traceable work log. Keep messages brief:

- Aim for a subject of about 50 characters or fewer. A subject alone is enough when no explanation or reference is needed.
- If a body is useful, separate it from the subject with a blank line and wrap prose around 72 characters. Explain the problem and why the change is needed, plus non-obvious consequences. Do not narrate the diff or copy the PR/test log. Separate paragraphs with blank lines; short bullets are fine.
- Put real issue references at the bottom. Use `Resolves: #123` only when the change completes that issue; use `See also: #456, #789` for related or partial work. Omit unused references.
- Add `Changelog: <category>` only for a changelog-worthy change, choosing one of `added`, `fixed`, `changed`, `deprecated`, `removed`, `security`, `performance`, or `other`. Omit the trailer entirely for documentation-only changes and small refactors.
- Preserve this format and useful references in the final squash/merge commit; do not concatenate worker messages into a long summary.

Message shape (replace example references and omit optional parts):

```text
Short summary of the change

Optional explanation of the problem and why this change is needed.
Mention non-obvious consequences only when useful.

Resolves: #123
See also: #456, #789
Changelog: fixed
```

## GitHub delivery

<!-- Keep this section when GitHub orchestration is adopted. Adapt to the repository's existing policy; otherwise omit it. -->

- All agents use the shared repository-owner GitHub account. The parent coordinates issues, delegation, review, and merge. Delegate implementation by default; fan out independent slices and serialize dependencies.
- Create or reuse an issue before implementation. Link intent, scope, acceptance criteria, planned verification, and dependencies. For larger tasks, link child issues from a parent. Each implementation issue has one active writer and normally one PR.
- Assign each worker a distinct branch and `<fixed-project-root>/.ai/worktree/<issue-number>-<slug>`. Verify the base ref/SHA, preserve existing changes, and ignore `/.ai/worktree/`. Pass the fixed root explicitly; do not nest orchestration roots inside worker checkouts. Coordinate shared test resources and numbered documents.
- Workers implement, verify, push, and open/update a PR with a brief behavior summary, evidence, caveats, and follow-up links. Link issue and PR in both directions; use closing references only for issues actually completed by the PR.
- The orchestrator reviews the diff and evidence and posts findings with the reviewed commit. Workers fix the same branch and reply with commits/evidence. Re-review changed revisions, then mark draft PRs ready and merge once findings and required checks pass. No separate approving account or human merge confirmation is needed; report an actual GitHub merge blocker if encountered.
- Resolve ordinary failures and missing evidence autonomously. Hand off only when a blocker cannot be resolved within scope or needs human action; state what is needed and continue unaffected work. Follow-ups need an origin link, clear remaining outcome, and acceptance criteria; they do not excuse missing agreed behavior.
- Record assignment, blockers, review/fix results, and merge on GitHub. Resume existing issues, PRs, and worktrees instead of creating duplicates. Close issues when their outcomes are delivered and preserve useful state before removing finished worktrees.

{{Link the project's detailed workflow or available github-orchestrate skill if maintained.}}

## Handoff

Report the behavior changed, evidence obtained, remaining uncertainty, and any human decision still needed in the existing delivery location. Update a spec when intent changes; correct editorial errors or stale links without adding implementation history. Record useful discoveries in their durable home and avoid duplicating them in memory.
