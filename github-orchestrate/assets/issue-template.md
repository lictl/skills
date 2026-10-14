<!-- Aim for fewer than 40 Markdown source lines in the opening human summary, using normal prose. Omit irrelevant or empty fields and remove these comments. -->

## Goal and why

{{Problem, observable outcome, and why it matters. Link the owning intent or briefly identify the dated human direction.}}

## Scope and success

- Scope: {{bounded change and any material exclusions}}
- Success: {{short observable acceptance criteria and how they will be verified}}
- Decisions or human action: {{material choices, blockers, or actions needed; include human review of actual ADR/spec revisions before merge when applicable}}

<!-- Optional trailing section for task pickup. Keep it concise and link authoritative documents instead of copying policy. Material human decisions, blockers and actions belong above. -->

## Agent handoff

- Context: {{intent/spec/ADR links, dependencies, and exact relevant revision or environment}}
- Current state and pickup: {{brief progress and next steps or constraints for the next agent}}
- Verification: {{technical commands/checks, evidence links, and remaining acceptance or environment limits}}
- Worker: {{agent/task name or Unassigned}}
- Branch/worktree: {{branch and repository-relative .ai/worktree/<number>-<slug> path}}
- PR base: {{target repository, branch, and starting SHA}}
- PR: {{URL, when available}}
- Worktree closeout: {{Pending delivery, Removed and verified, Blocked with reason and owner, or No disposable worktree}}

{{Record later milestones as concise comments and keep the current summary accurate. At completion, record the outcome, tested revision, verification, caveats and follow-ups on GitHub; the parent removes the finished worktree and records verified cleanup. Do not use extra local recovery copies as the work log.}}
