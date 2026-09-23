---
name: write-spec
description: Create, review, or revise a compact, human-owned product, capability, or feature spec with observable acceptance criteria and explicit open questions. Use for defining or changing intended behavior, not for implementation plans, architecture decision records, or documenting every detail of existing code.
---

# Write Spec

Write the smallest statement of intent a responsible engineer can read end-to-end before implementation. A spec is a decision aid, not a prediction of every implementation detail.

## Ground the request

Read applicable project instructions, the current request, the existing spec if any, relevant parent specs and accepted ADRs, and enough interfaces/tests to understand the boundary. Do not require a repository bootstrap before writing a single spec.

Separate explicit human requirements, observed current behavior, and unresolved choices. Preserve the origin of material constraints with a short source link or attribution. An implementation, old agent summary, or test does not prove a behavior is desired. Existing accepted constraints still matter when the code does not follow them.

For behavior-changing ambiguity, put a precise question in Open questions and identify which behavior it blocks. Suggest options and a recommendation when useful. Label any proposed assumption as unapproved; merely writing it down does not authorize building on it. Low-impact implementation choices need not become product questions. Continue drafting settled content while questions are pending.

## Choose the document and identity

Reuse an existing spec when it owns the same behavior. Otherwise use the repository's numbering convention or `docs/specs/NNN-descriptive-slug.md`, starting at `001`.

By default, allocate a single spec sequence across `docs/specs/` and its subdirectories, separate from ADR numbering. Use a number above the largest known or reserved ID, including available archived/history records; never recycle or renumber published IDs. Recheck before writing and resolve concurrent draft collisions without overwriting another file.

Start with a flat feature spec. Read [product scaling guidance](references/product-specs.md) only for product/capability work or when a spec has become too broad. Do not invent a product tree for a small change.

## Write seven sections

Adapt [the spec template](assets/spec-template.md). Keep exactly these body sections; place brief status and provenance metadata before them:

1. **Problem:** Who experiences what problem, and why solving it matters.
2. **Desired behavior:** Observable outcomes, including relevant failure behavior. Use examples where they remove ambiguity.
3. **Scope:** What this change owns; link children for separately reviewable behaviors.
4. **Non-goals:** Plausible nearby work explicitly excluded.
5. **Constraints:** Real binding requirements, with their sources. A technology choice belongs here only when it is actually required, otherwise in an ADR or implementation.
6. **Acceptance criteria:** A small set of observable, falsifiable outcomes with stable local IDs such as `AC-001`. Include applicable boundary or failure cases and identify a feasible test or manual verification method. Do not write a full test plan here.
7. **Open questions:** Unresolved material choices and their impact. Write `None` only when supported by the request and evidence.

Keep the spec readable in one sitting, normally well below 200 lines. The threshold diagnoses mixed scopes or implementation detail; do not compress dense prose or hide required behavior in appendices to evade it. Split independent behavior, and route mechanics to code, schemas, tests, configuration, runbooks, or ADRs. Keep essential acceptance criteria with their behavior.

Review applicable concerns such as data loss, compatibility, migration, access control, accessibility, and performance. Include only those relevant to the change, under the seven sections. Do not invent targets or add an eighth generic checklist.

Prefer “Queued jobs recover after restart” over a database table, locking strategy, and polling interval unless those mechanisms are binding requirements. A useful example can expose ambiguity more cheaply than another paragraph.

## Preserve human ownership

- Human instructions in chat or comments can authorize the spec's intent. Record that source and use `Approved` for covered intent, `Draft` for unresolved proposals. This status does not claim a human read the generated document. Do not require another review simply because an agent wrote it down.
- Do not invent a reviewer or approval, and do not treat a request to draft as acceptance of agent-invented behavior. Continue already-authorized implementation while only the portions needing a material human decision remain pending.
- For a material revision, make the intent delta and affected acceptance criteria explicit. Keep prior approval distinguishable from the proposed revision, using version control or a separate draft where necessary. Update approval status only to reflect real evidence.
- Editorial corrections, clarified wording that preserves meaning, resolved questions reflecting an existing decision, and evidence links do not require a new approval ritual. Make any uncertain semantic change visible.
- When a child conflicts with its parent or an accepted ADR, flag it for resolution at the owning level. Do not silently alter the parent, discard a constraint, or weaken an acceptance test.

## Review and deliver

Read the complete spec. Check that every criterion traces to stated intent, no assumption has become a requirement, non-goals agree with scope, and links resolve. Preserve stable criterion IDs as wording evolves; do not reuse retired IDs for unrelated behavior.

When using GitHub delivery, issues link the applicable spec and criterion IDs; PRs carry verification and review history. Keep assignments and execution logs out of the spec. An issue or orchestrator comment cannot silently change approved intent. Coordinate new spec IDs with the orchestrator when several workers are active.

Return the document, a concise intent delta for revisions, and only the material unresolved questions. Spec writing alone does not authorize implementation. If implementation is already part of the authorized task, proceed with settled slices and place test results in the delivery evidence, not a growing spec log.
