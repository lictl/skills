# Worktree and GitHub details

## Worktrees

Use one fixed absolute project root. Every worker checkout lives under `<root>/.ai/worktree/`; a worker must not create another orchestration root inside its checkout.

1. Inspect local changes, `git worktree list --porcelain`, and existing task branches. Reuse matching task work rather than resetting or overwriting it.
2. Ignore `/.ai/worktree/` through `.gitignore` or a local Git exclude. Check recursive build/watch tools if they scan ignored directories; do not ignore all of `.ai/`.
3. Fetch the intended base and record its branch and SHA. New worktrees do not include uncommitted root-checkout changes; transfer required task context deliberately and preserve unrelated work.
4. Create a free path and branch from that base, then run the worker's commands from its own checkout. For verified task variables:

```sh
git -C "$orchestration_root" worktree add -b "$task_branch" "$task_worktree" "$base_sha"
```

Do not force-reset an occupied branch or overwrite an existing directory. A new repository needs a baseline commit before dispatch.

Worktrees share Git refs/configuration and may share ports, databases, simulators, or external build directories. Coordinate shared resources or serialize conflicting checks. Dependent slices normally start after their prerequisite merges, from a refreshed base. Use stacked PRs only when needed and record their merge order and base changes.

After merge or explicit abandonment, preserve needed commits, uncommitted/untracked work, and useful ignored artifacts before `git worktree remove`. Do not remove an active worker's checkout. Disposable caches need no retention.

## GitHub record

Keep the issue's assignment/status/PR link current and the PR's summary/evidence/caveats current. Record meaningful transitions through comments, not repeated unchanged status reports. Use short role labels such as `Worker for #42` or `Orchestrator review of <sha>` to distinguish agents using the shared account.

Use `Closes #42` only when the PR fulfills the issue. GitHub closing keywords apply to PRs targeting the default branch; otherwise keep explicit links and verify closure after final integration. Use `Related to #42` for partial or parent-issue references.

For multiline CLI bodies, use a file with `--body-file`; connectors can use structured body fields. Link large logs and identify the tested commit/environment instead of pasting everything into the PR.

Before retrying an ambiguous creation, push, or merge, check GitHub's actual state. Resume the existing issue, branch, PR, and worktree when possible, transferring an interrupted worker's ownership explicitly. If GitHub is unavailable, preserve local work and pending publication content, and report what remains unrecorded.

## Commit messages

Use a subject around 50 characters or fewer. Add a body only when useful: a blank line after the subject, prose wrapped around 72 characters, and a brief explanation of the problem, why, and any non-obvious consequences. Short paragraphs or bullets are fine; do not repeat the diff or PR log.

Put references at the bottom: `Resolves: #123` only for an issue the change completes, and `See also: #456, #789` for related or partial work. Use actual issue numbers and omit unused fields. Add `Changelog: <category>` only when warranted, selecting `added`, `fixed`, `changed`, `deprecated`, `removed`, `security`, `performance`, or `other`; omit it for documentation-only changes and small refactors.

## Merge

The orchestrator's review comment and successful verification are the workflow's review gate. Merge directly with the shared owner account; do not add a separate reviewer or approval ceremony. Use the reviewed head SHA as the merge precondition when supported, and re-review if it changes. Confirm GitHub reports the PR merged before reporting completion. If existing repository rules prevent merging, report the actual unmet requirement.

Check the final squash/merge message follows the commit convention and retains useful issue/PR references and any applicable changelog trailer. Replace verbose generated message concatenations with a concise summary so the merged Git history remains a useful work log.

## References

- [Git worktrees](https://git-scm.com/docs/git-worktree)
- [GitHub issue/PR linking](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue)
