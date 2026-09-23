# Scale by delegation

Use a tree only when distinct capabilities or features need independent review. Every spec retains the same seven sections and a readable size. Parents constrain; children specify; neither repeats the other.

```text
docs/specs/
  001-product.md
  capabilities/
    002-job-processing.md
  features/
    003-restart-recovery.md
docs/adr/
  001-job-storage.md
```

These are illustrative allocated IDs, not mandatory files. Use the next available IDs in the project's convention. Keep decisions at the appropriate shared scope instead of duplicating them per feature.

- A product spec identifies the problem and users, product outcomes, non-goals, and constraints that bind all capabilities. Scope lists capabilities in one line each, linking those with actual specs. Product acceptance criteria describe product outcomes, not a copy of every child's checks.
- A capability spec describes a subsystem with a meaningful independent delivery or failure boundary. Its scope links features; its criteria capture the subsystem's contract and interactions.
- A feature spec is the leaf handed to an implementing agent. Its criteria are concrete enough to verify the requested behavior without reconstructing intent from implementation notes.

Give children explicit parent links. If a capability crosses multiple boundaries, link the applicable constraints and clarify ownership instead of duplicating the same requirement. A conflict is a question for the owning human, not permission for a local override.

Write child specs just in time. A future capability can remain one line and an open question in its parent until it is next to be built. Do not populate an entire speculative tree.

When a spec grows toward 200 lines, inspect why. Push independent behavior into children and mechanics into an ADR, schema, test, code, or runbook. Do not split a single inseparable decision into many files merely to satisfy a line count.

Before implementation, read the applicable product, capability, and feature specs in that order, then the relevant accepted decisions and interfaces. Read the relevant branch of the tree, not all siblings. Re-ground when revisions or new human instructions change the context.
