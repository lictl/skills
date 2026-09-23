---
name: github-orchestrate
description: Delegate GitHub issue-scoped implementation to agents in isolated worktrees, review and fix their PRs, then merge with a shared repository-owner account. Use when this delivery workflow is requested or adopted by project guidance.
---

# GitHub Orchestrate

All agents use the same GitHub account, which owns the repository. Agents continue autonomously through authorized implementation, review and ordinary code-only merges. PRs that create or change ADRs or specs require human review before merge, including editorial document edits and mixed code/document PRs. A shared account, agent review, successful check or instruction to start work is not evidence of human review.

Delegate implementation by default; parallelize independent slices and serialize dependencies. Use one worker for a small task. If agents are unavailable, preserve the same GitHub work log while working sequentially. Writing or installing this skill alone does not start a live task.

`agentic-bootstrap` is excluded from this delivery loop: its setup changes stay local and uncommitted for human review and commit. Subsequent authorized tasks use the autonomous workflow below.

## 1. Define and delegate

Read project guidance, the current request, and relevant specs/ADRs. Confirm the repository and base branch, then find existing task issues, PRs, and worktrees before creating more.

- Create or reuse an issue using [the issue template](assets/issue-template.md). State the outcome, scope, acceptance criteria, verification, and dependencies. Link specs rather than copying them. A small task may describe its human-approved intent directly in the issue.
- Use a parent issue only when several slices need coordination. Give each slice one active worker, branch, worktree, and normally one PR. Coordinate overlapping files, shared interfaces, and numbered docs.
- Create the worker's checkout at `<fixed-project-root>/.ai/worktree/<issue-number>-<slug>`, using `codex/issue-<number>-<slug>` unless the project specifies another branch convention. Follow [worktree and GitHub details](references/operations.md).
- Hand over the issue URL, exact worktree path, branch, starting base ref/SHA, and verification expectations. Record the assignment on the issue. Do not have multiple agents write the same checkout.

## 2. Implement and open the PR

The worker reads the issue and linked intent, implements in its assigned worktree, runs relevant checks, commits, pushes, and opens or updates the PR. Keep incomplete work in draft. Use [the PR template](assets/pr-template.md) for a brief behavior summary, verification, caveats, and follow-up links.

Keep commits brief and traceable using the [commit-message convention](references/operations.md#commit-messages): a short subject, an optional explanation of why, and issue references. Preserve that convention in the final squash/merge commit too.

Prefer focused unit tests for feature logic and e2e tests for important workflows where appropriate. For bugs, add a regression test that fails for the original defect and passes after the fix when practical, with relevant negative cases. Extend existing coverage instead of duplicating it; documentation-only edits and low-impact changes need proportionate checks, not test scaffolding. Report unrun before/after checks honestly.

When implementation or review uncovers a verified counterintuitive fact or reusable lesson from costly investigation, update project memory in the assigned worktree with the trap, resolution, and evidence. Include it in the task's commit/PR (or a review-fix commit), so it survives merge and cleanup. Skip routine progress notes.

Link issue and PR in both directions. Use a closing reference only when the PR completes that issue; use a non-closing reference for partial work or a parent issue. Return the PR URL, head SHA, evidence, and any blockers to the orchestrator.

Issues, commits, and PRs form the work log. Commits record concise changes and reasons; issues and PRs record assignments, material decisions/blockers, verification, review findings, and completion. Internal agent messages must not be the only record needed to resume work.

## 3. Review and fix

The orchestrator reviews the actual diff and evidence against the issue's criteria and relevant specs/ADRs. Post a short review comment identifying the reviewed head SHA, actionable findings, and any missing verification. Use inline comments when useful. Agent review can be recorded as a comment; the human ADR/spec review below remains required.

For ADR/spec changes, finish the agent review and fixes first, then present the actual documents/diff and PR for human review. Record explicit human approval from chat or GitHub and the document revision it covers. Do not infer approval from silence or the agent's use of the human's GitHub account. Keep proposed/draft documents visibly pending; do not mark them Accepted/Approved on the strength of task authorization alone.

The gate covers document creation, revision, renaming and deletion. After actual approval, recording its evidence and changing Proposed to Accepted or Draft to Approved does not require another review if the reviewed decision or requirements text remains unchanged.

Send finding links to the worker. The worker fixes the same branch, pushes, and replies with the fix commit and evidence. The orchestrator verifies fixes and changed revisions, including relevant integration changes. Resolve ordinary failures autonomously and continue unaffected slices. If a blocker cannot be resolved within the task or needs human input, state the problem, attempts, and exact decision/action needed; do not merely hand back a failed check or loop without progress.

Create or reuse follow-up issues for separate useful work. Reuse the issue template and add the origin issue/PR, why the work is separate, and what remains. Link back from the PR. Missing agreed behavior, regressions, or failed required checks remain blockers; moving them to a follow-up does not resolve them. Material scope changes still need human agreement.

## 4. Merge and close the loop

Once criteria are verified and findings resolved, mark a draft PR ready and confirm required checks and mergeability for the reviewed head. If it changes an ADR or spec, leave it open with auto-merge disabled until the human has approved the actual document content. Changed reviewed content needs renewed human review; unrelated code commits or recording approval evidence without changing that content do not invalidate it. Agent re-review still covers every new PR head. Unchanged references to an ADR/spec alone do not trigger this gate.

When the applicable review gate is satisfied, merge using the shared owner account and the repository's normal method, protecting against an unreviewed newer head. Do not add another approval step for code-only PRs. If GitHub blocks the merge, report the actual blocker without changing protections as a workaround.

Confirm the merge, update/close the completed issue, and continue the remaining authorized slices. A parent remains open until its outcome is complete; an unrelated follow-up is a separate task. Confirm memory notes and other useful state are preserved before removing finished worktrees.

Finish with issue/PR links, merge result or pending human document review, verification and follow-ups. A PR awaiting review is not a completed merge and its delivery issue stays open. Another orchestrator should be able to resume from GitHub without the private agent conversation.
