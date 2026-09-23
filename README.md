# Human-readable agentic workflow skills

Agents expand execution capacity. Humans retain ownership of intent. These skills establish a small set of readable documents and a workflow grounded in executable evidence.

| Skill | Use it to |
| --- | --- |
| [agentic-bootstrap](agentic-bootstrap/SKILL.md) | Prepare local documentation and workflow changes for a human to review and commit. |
| [write-spec](write-spec/SKILL.md) | Draft or revise compact product, capability, and feature intent with observable acceptance criteria. |
| [write-adr](write-adr/SKILL.md) | Record a significant architecture choice, its rationale, alternatives, consequences, and lifecycle. |
| [github-orchestrate](github-orchestrate/SKILL.md) | Delegate issue-scoped implementation to workers in worktrees, publish PRs, and review/fix them with a traceable GitHub work log. |

Each directory is a standalone skill with templates and optional supporting references. The Markdown instructions are agent-neutral; `agents/openai.yaml` supplies optional Codex UI metadata. Bootstrap can use the companion skills when available but does not depend on them.

## Installation

In Codex, ask the built-in installer:

```text
Use $skill-installer to install agentic-bootstrap, write-spec,
write-adr, and github-orchestrate from the GitHub repo lictl/skills.
```

On the next turn, open the project you want to set up and ask:

```text
Use $agentic-bootstrap to adopt this workflow in this project.
```

Bootstrap leaves local changes uncommitted. Review and commit them yourself; subsequent tasks use the issue/PR workflow. ADR/spec changes require human document review before merge; ordinary code-only work remains autonomous.

For a manual Codex install, copy the complete skill folders into your project's `.agents/skills/` or your personal `~/.agents/skills/`, including their assets and references. If the skills do not appear, restart Codex. See the [official skill installation guidance](https://learn.chatgpt.com/docs/build-skills#install-curated-skills-for-local-use).

GitHub orchestration also needs Git and authenticated GitHub access through a connector or CLI, using the shared repository-owner account. Installing the skills alone does not start project work.

## Default project layout

```text
AGENTS.md
docs/
  adr/001-descriptive-decision.md
  specs/001-descriptive-feature.md
  memory/
.ai/worktree/  # ignored local worker checkouts when GitHub delivery is adopted
```

These are naming examples, not documents to fabricate at bootstrap. Keep a coherent existing layout unless a migration is requested. ADRs and specs have separate stable number sequences. Specs may grow into a tree of numbered product, capability, and feature documents when independent review requires it.

## When to write a spec or ADR

Write or update a **spec** to define what the system should do: observable behavior, scope, constraints, and acceptance criteria. Use it when that intent needs a durable explanation; a small, unambiguous task can use its issue instead.

Write an **ADR** when a significant technical choice has alternatives and consequences worth remembering, such as storage, service boundaries, or an API contract. Explain the decision and why it fits the constraints. Routine implementation details do not need an ADR.

| Example | What to write |
| --- | --- |
| Add the ability to cancel an export using the existing architecture. | **Spec:** when cancellation is allowed, what happens to partial output, and how success is verified. |
| Replace a storage dependency while preserving existing behavior. | **ADR:** alternatives considered, the reason for replacement, and migration or compatibility trade-offs. |
| Make queued jobs recover after restart, requiring a new persistence design. | **Both:** the spec defines recovery guarantees; the ADR explains the chosen persistence design. Link them without repeating their content. |
| Fix a typo or an off-by-one error without changing intended behavior. | **Neither new document:** use the issue/PR and, for the bug, a focused regression test. Update a spec only if intended behavior changes. |

Reuse the spec that owns the behavior. When replacing an accepted architecture decision, create a new ADR and link the superseded record so its reasoning remains available.

## Working agreement

Bootstrap is a local, human-committed setup step. After adoption, agents work within the requested scope; ADR/spec edits retain a human review gate before merge:

Human direction → draft/implementation → checks → agent review/fixes → human document review when ADR/spec content changes → merge → next authorized slice.

- Specs answer seven questions: problem, desired behavior, scope, non-goals, constraints, acceptance criteria, and open questions. About 200 lines is a readability diagnostic, not a target.
- Humans establish intent through chat/comments; this is distinct from review of an actual ADR/spec. New documents remain Proposed/Draft until explicit human approval is recorded with the reviewed revision. Complete drafting, checks and agent review before presenting the document/diff or PR. Editorial ADR/spec edits and mixed PRs also require human review. Changes to reviewed content need renewed review; unrelated code commits or adding approval evidence without changing that content do not. Ordinary code-only work stays autonomous.
- Approved specs define intent; accepted ADRs constrain architecture. Tests, code, and runtime are evidence of current behavior. Conflicts require explicit resolution, not a simplistic ranking that lets code erase a decision.
- Prefer slices that demonstrate observable behavior through the necessary layers. Bounded experiments and enabling changes are useful when they resolve a named uncertainty.
- Prefer feature tests: unit tests for logic and e2e tests for important user workflows where appropriate. Bug fixes should have focused regression/negative coverage that demonstrates the original failure and the fix when practical. Avoid redundant tests, implementation-mirroring assertions, and mandatory coverage at every layer.
- Map acceptance criteria to verification evidence, recording what was actually run. Keep results in the issue/PR, not an expanding spec.
- Keep Git history traceable with brief commits: about 50 characters for the subject, an optional why-focused body wrapped around 72, and issue references at the bottom. Add a `Changelog` trailer only when warranted; omit it for documentation-only changes and small refactors. Preserve the same format through squash/merge.
- Save memory for verified counterintuitive facts or reusable lessons from significant investigation. Record the trap, finding/fix, evidence, and revalidation context; skip routine logs and obvious facts. Route enforceable constraints to tests, schemas, ADRs, code, or configuration.

This workflow does not require a spec for every typo or an ADR for every coding choice. Review effort follows behavior change and risk. Relevant nonfunctional constraints remain part of intent; compactness is not a reason to omit them.

## GitHub delivery

Human intent → issue → delegated worker/worktree → PR with evidence → agent review/fixes → human review for ADR/spec edits → merge.

Delegate implementation by default and parallelize independent slices. Use one active writer, branch, and worktree per issue, normally with one PR. Larger tasks use a parent issue and linked slice issues; dependent work waits or declares an explicit stacked-PR integration plan.

```text
Issue #42
  branch:   codex/issue-42-restart-recovery
  worktree: <fixed-project-root>/.ai/worktree/42-restart-recovery
  PR:       links #42, verification, caveats, and follow-ups
  review:   findings and fixes tied to commit revisions
```

Issues, Git commits, and PRs form the durable execution record. Issues track scope, ownership, dependencies, and current state; commits briefly explain changes and why; PRs record verification, caveats, review findings, and fixes. Specs, ADRs, and memory keep their distinct roles.

All agents use the shared GitHub account that owns the repository. The orchestrator reviews through PR comments. For ADR/spec edits, leave the PR open with auto-merge disabled until actual human approval of the document content is recorded; agent reviews, passing checks and task authorization do not satisfy that gate. Once applicable reviews and checks pass, merge the current reviewed head. Unchanged references to ADRs/specs do not add a human gate to code-only work. Report actual GitHub blockers without changing protections as a workaround.

Follow-up issues capture separate actionable work; they cannot hide unfinished acceptance criteria or missing document review. Agents research and propose architecture within agreed scope; humans review ADR/spec text and resolve material choices. Keep intent, review evidence and execution history connected on GitHub rather than creating a parallel task system.

The [orchestration skill](github-orchestrate/SKILL.md) includes just issue and PR templates, plus [worktree and GitHub details](github-orchestrate/references/operations.md). Follow-ups reuse the issue template; reviews are short comments.

## Design references

- [Michael Nygard: Documenting Architecture Decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) supports short records, stable numbering, decision status, consequences, and retained superseded history.
- [AGENTS.md](https://agents.md/) describes repository guidance with build/test commands and scoped instructions. These skills keep that guidance focused and link project detail.
- [DORA: Working in small batches](https://dora.dev/capabilities/working-in-small-batches/) supports feedback through small, verifiable increments.
- [Agile Alliance: Acceptance Testing](https://agilealliance.org/glossary/acceptance-testing/) describes behavior examples as formal specifications or complements to narrative specs. These skills use compact narrative intent plus verification evidence; that is a workflow choice, not a universal requirement.
- [Git worktrees](https://git-scm.com/docs/git-worktree) provide separate checkouts while retaining shared repository state; the orchestration skill accounts for that boundary.
- [GitHub issue/PR links](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue) define linking and closure behavior.

The specific directory defaults, seven-section spec, memory contract, and readability threshold are conventions for this skill set, not claims of an industry standard.
