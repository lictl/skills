---
name: agentic-bootstrap
description: Bootstrap a new project or adapt an existing repository to a human-owned agentic development workflow with concise AGENTS.md guidance, numbered specs and ADRs, evidence-backed project memory, and GitHub issue/PR orchestration when requested. Use when adopting or repairing the workflow, not for ordinary feature implementation or a single document edit.
---

# Agentic Bootstrap

Establish the smallest usable workflow in which humans own intent and agents implement verifiable slices. Preserve useful project conventions. Folder names alone do not make a workflow effective.

## Inspect before writing

1. Read applicable repository instructions and check working-tree changes. Preserve unrelated work.
2. Inspect the README, documentation, build manifests, CI, representative interfaces and tests. Identify project boundaries, supported environments, existing unit/e2e test commands and coverage gaps, and documentation sources. Do not scan every source file by default.
3. Find existing specs, decisions, agent guidance, and handoff conventions, including equivalents outside `docs/`. Distinguish missing structure from a useful structure with different names.
   When GitHub delivery is requested or already adopted, inspect remotes, issue/PR templates, agent capabilities, worktree conventions, and review/check requirements as well.
4. Report a brief assessment: what exists, what can be reused, gaps, and uncertain facts. Separate observed behavior from intended behavior; code cannot establish human approval or historical rationale.

For an empty project, establish navigation and workflow only. Leave the stack, product behavior, and commands unknown unless the user supplied them. Do not choose an architecture to fill a template.

## Adopt a minimal structure

Read [adoption guidance](references/adoption.md) for naming, conversion, memory, and the ongoing work loop. Use these defaults when an equivalent convention is absent:

```text
AGENTS.md
docs/
  adr/       # 001-descriptive-decision.md
  specs/     # 001-descriptive-feature.md
  memory/    # short, evidence-backed project notes
```

- Create missing directories. If empty directories must survive version control, use the repository's placeholder convention or `.gitkeep`; do not fabricate an ADR, spec, or memory entry.
- Adapt [the AGENTS.md template](assets/agents-template.md) to verified project facts. It is a starting point, not text to append wholesale to an existing file.
- Include its commit-message convention: a subject around 50 characters or fewer, an optional why-focused body wrapped around 72 characters, and real issue references at the bottom. Treat Git history as part of the work log. Add a `Changelog` trailer only when warranted; omit it for documentation-only changes and small refactors. This is agent guidance and needs no Git configuration or commit hook.
- Keep `AGENTS.md` a concise map with actionable commands and a few project-specific constraints. Link to maintained sources; use scoped guidance for subprojects when needed.
- In a different but coherent layout, link to the existing locations instead of making competing copies. When canonical-path migration is requested, perform it with a path mapping and link updates.
- If substantive specs or ADRs are part of the request, use `write-spec` or `write-adr` when available. Otherwise follow existing project templates and the minimum rules in the adoption guide. These companion skills are optional, not runtime dependencies.
- When GitHub orchestration is requested, install the agreement below and adapt the project's existing issue/PR templates. Use `github-orchestrate` when available for execution details; keep the essential agreement in project guidance so it remains usable without that companion skill.
- Do not introduce an unrequested task system, CI service, framework, or agent runtime. Adopting GitHub issue/PR coordination does not require a GitHub Actions workflow or changes to branch protections.

## Adopt GitHub orchestration when requested

The parent agent writes or reuses task issues and delegates implementation by default, fanning out independent slices and serializing dependencies. Each issue has one active writer, normally one PR, and a worktree at `<fixed-project-root>/.ai/worktree/<issue-number>-<slug>` on its own branch. Ensure `/.ai/worktree/` is ignored and check exclusions for tools that recursively scan the root.

Record the issue URL, scope/criteria, relevant specs/ADRs, worker, branch/worktree, PR base, and starting SHA in the handoff. Issues carry assignments and current state; commits record concise changes and their reasons; PRs carry verification, caveats, and review history. Keep issue, commit, and PR references connected, including in the final squash/merge message.

The worker publishes the PR and fixes findings on the same branch. The orchestrator reviews the actual diff and evidence for the current revision, posts findings on the PR, and repeats until resolved or concretely blocked. Follow-up issues must link their origin and describe remaining behavior; they cannot conceal unmet acceptance criteria. Reuse existing issues/PRs on resume.

All agents use the shared repository-owner GitHub account. The orchestrator reviews through PR comments and merges directly once criteria, findings, and required checks are satisfied; no separate approving account or human merge confirmation is needed. Report actual GitHub merge blockers if encountered. Preserve useful state before removing finished worktrees. Put this agreement in `AGENTS.md` or a linked project workflow document; bootstrap itself does not start executing the backlog.

## Install the working agreement

Make these decisions clear in the resulting guidance, adapting to existing project policy:

- Current explicit human direction and approved specs describe intent. Parent specs constrain child specs. Accepted ADRs record architectural constraints and reasons. Tests, code, and runtime provide evidence of implemented behavior. Memory and previous agent output are context, not authority.
- When these sources conflict, name the discrepancy. Follow an explicit human resolution already provided; otherwise surface any material choice and continue only unaffected work or a bounded exploratory check. Do not silently rewrite requirements, weaken tests, or replace an accepted decision to make the conflict disappear.
- Human chat, issue comments, or explicit requests can establish intent; a separate document or PR review is not required. Link the actual direction, distinguish unresolved proposals, and do not claim a human reviewed generated text. Agents decide implementation details within that intent, including architecture, and record who decided. Material changes to intent still need human agreement.
- Implement one independently verifiable slice at a time. Prefer a thin observable behavior through the necessary layers. Technical enabling slices are useful when they have a concrete verification result and an identified dependent behavior.
- Verification must connect to acceptance criteria. Record commands, outcomes, environment limits, and unresolved gaps in the existing PR, issue, or handoff location. Passing generated tests alone does not establish that the intended behavior was chosen correctly.
- Prefer focused feature tests: unit tests for logic and e2e tests for important user workflows where appropriate. For bugs, add a regression test that reproduces the failure and passes after the fix when practical; cover relevant negative cases. Extend existing coverage, avoid redundant or implementation-mirroring tests, and do not require every test layer for every change. Apply the proportionate testing guidance in the adoption reference.
- Save project memory when verified evidence contradicts a plausible assumption, or significant investigation produces a reusable lesson. Record the mistaken expectation, finding/resolution, and evidence so future agents avoid the same detour. Ordinary progress and obvious facts do not need memory entries.
- Continue autonomously through the authorized task, including agent review and merge. Involve the human when an actual blocker, unresolved material choice, or required access/action needs them; state what is needed and continue unaffected work. Human PR review and routine approval checkpoints are not the default.

## Verify adoption

Check that paths and links resolve, numbering is unambiguous, and instructions agree with the actual project. Resolve all template placeholders into facts, explicit unknowns, or omitted optional sections.

Run relevant non-destructive checks for documentation changes and safe local command verification where practical. Record unrun commands as unverified; do not execute deployments, data resets, or other external actions merely to validate a documented command. Existing baseline failures are findings, not authorization for unrelated repairs.

Review the result as a second invocation would: it should reuse the same sources, preserve IDs and user text, and avoid duplicate headings, files, or approval requests. Do not repeatedly append generated guidance.

Finish with the adopted paths, reused conventions, verification evidence, and remaining human decisions. Workflow setup does not authorize starting the product backlog.
