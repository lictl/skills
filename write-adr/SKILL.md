---
name: write-adr
description: Create, review, or supersede a numbered architecture decision record with context, alternatives, consequences, and honest decision status. Use for significant architecture choices or their rationale, not routine implementation details, feature requirements, or reconstructing unverified historical approval.
---

# Write ADR

Record one significant architecture decision so a future engineer can understand the choice, its limits, and why alternatives were not selected. Keep the record short, usually one or two pages.

## Establish the decision

Read applicable instructions, relevant intent from specs or human chat/comments, existing ADRs, and the code or experiments needed to understand the decision. Distinguish observed facts, proposals, and decisions, including who made them.

Use an ADR when a choice materially affects boundaries, interfaces, dependencies, data models, quality attributes, operations, or costly future change. Do not create one for every local coding choice or merely to populate `docs/adr/`.

Identify the decision maker and task authority. Agents may investigate and propose architecture within the agreed scope, but an ADR needs human review of the actual document before merge. Task authorization is not document approval. If reconstructing an existing architecture, state what was observed, where, and what rationale is unknown. Do not turn “the code does this” into a fabricated historical decision.

## Choose the record

Use the repository convention or `docs/adr/NNN-descriptive-decision.md`, starting at `001`. ADR numbering is separate from spec numbering. Allocate above the largest known or reserved ADR ID across the ADR root and subdirectories, considering available archives/history. Never reuse IDs or renumber published records.

Recheck availability before writing. Resolve a collision by changing an unpublished draft and its references; never overwrite another record. Reuse a proposed ADR for the same unresolved decision rather than generating parallel proposals.

Adapt [the ADR template](assets/adr-template.md) and retain only useful detail:

- **Metadata:** Status, date, decision maker and source, human review evidence or Pending, related specs, and supersession links when applicable. Identify the document revision covered by review. If a historical decision date is unknown, distinguish the recording date rather than backdating it.
- **Context:** The problem, forces, and binding constraints, with evidence. Link requirements rather than restating the full spec.
- **Decision:** One clear choice and the scope in which it applies. Make proposals visibly conditional until accepted.
- **Alternatives:** Credible choices considered, including the status quo when plausible, with concrete reasons for accepting or rejecting them. Do not invent a prior evaluation or benchmarks.
- **Consequences:** Benefits, costs, risks, compatibility or migration effects, and reversibility where relevant. Include drawbacks, not just advocacy.
- **Validation and revisit conditions:** Evidence supporting the choice, what is still unverified, and the change or observation that would justify reconsidering it. Link experiments or tests instead of copying outputs.

## Maintain decision history

Use `Proposed` for a new ADR until the human reviews and explicitly approves its actual text, even when the task already establishes the intended direction. Use `Accepted` only with that review evidence. Identify the agent's technical authorship separately from the human reviewer. Preserve historical status honestly; do not invent retrospective approval for an older record. Ask about a material unresolved choice while continuing unaffected work.

After approval, updating Proposed to Accepted and recording the actual approval evidence does not need another review when the reviewed decision text is unchanged. Renaming or deleting an ADR still requires human review before merge.

Use existing project lifecycle terms where established. Otherwise use `Proposed`, `Accepted`, `Rejected`, `Deprecated`, and `Superseded` as needed. Mark a proposal rejected only when evidence supports that outcome.

An accepted decision's substantive rationale is historical. Correct typos or add clearly dated factual annotations without rewriting history. A materially different decision gets a new ADR. Keep the old accepted ADR in force while its replacement is merely proposed; after acceptance, mark the old record superseded and link both directions. Deprecation without replacement should state why and what still applies.

If the choice changes intended product behavior or violates a spec, surface the corresponding spec change for human agreement. An ADR is not a back door for redefining requirements. Writing the decision record alone does not authorize implementation, purchase, migration, or deployment.

## Review and deliver

Check the decision against relevant specs and other accepted ADRs. Verify numbering, links, status, date provenance, and any supersession references. Distinguish actual evidence from recommendations or pending experiments.

When using GitHub delivery, link the originating issue/PR and decision comment when relevant. Keep execution status and review/fix logs on GitHub. Coordinate new ADR IDs with the orchestrator when several workers are active.

Complete drafting, verification and agent review before requesting human review. Present the document/diff or PR and leave it unmerged until explicit human approval of the reviewed content is recorded in chat or GitHub with the revision covered. The gate includes editorial ADR edits and mixed code/ADR PRs. Agent comments, passing checks, shared-account reviews and earlier task authorization are not human approval. Changes to reviewed content require renewed review; unrelated code commits or recording approval evidence without changing that content do not. Never silently enable auto-merge while review is pending.

Return the record, material trade-offs and reviewable revision. State whether human review is pending and why. Keep task plans and implementation logs outside the ADR; this review gate does not create a separate approval step for ordinary code-only work.
