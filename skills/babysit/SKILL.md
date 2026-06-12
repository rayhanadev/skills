---
name: babysit
description: >-
  Keep a PR merge-ready by triaging review comments, resolving clear merge
  conflicts, and fixing in-scope CI in a loop. Use when the user types
  `/babysit` or asks to get a PR mergeable, green, or its comments triaged.
---

# Babysit PR

Drive a pull request to a merge-ready state, then **report back — never merge it yourself** unless explicitly told to.

A PR is merge-ready when all of these hold:

- No merge conflicts with the base branch.
- Every unresolved review comment (human or bot) is either addressed or has a written reason it wasn't.
- Required CI checks are green, or the only failures are demonstrably outside this PR's scope (and you've said which and why).

## Work in a loop

Each commit you push makes CI re-run and reviewers re-evaluate, so don't fix everything blind and check once. Loop:

1. **Assess** the current state (below).
2. Pick the highest-priority blocker — conflicts first, then failing required checks, then review comments.
3. Make the smallest correct fix, commit, and push.
4. Re-fetch state and repeat until merge-ready.

Stop the loop when the PR is merge-ready or you hit a [stop condition](#stop-conditions).

## 1. Assess

Pull just the state you need, not the whole payload:

```sh
gh pr view --json number,state,mergeable,mergeStateStatus,reviewDecision,statusCheckRollup
gh pr checks            # human-readable CI status
```

`mergeStateStatus` tells you the headline problem: `DIRTY` = conflicts, `BEHIND` = behind base, `BLOCKED` = required check or review missing, `UNSTABLE` = a non-required check is failing, `CLEAN` = ready.

## 2. Merge conflicts

Merge the latest base branch and resolve conflicts intelligently, preserving the intent and correctness of changes on *both* sides — yours and the base. Read enough surrounding code to understand what each side was doing before you pick.

- If the two sides have genuinely conflicting intent (not just textual overlap), abort the merge and ask the user which should win.
- If the branch is merely `BEHIND` (no real conflict), merging latest base is also worth doing proactively — another PR may have already fixed a failure you're seeing.

## 3. Review comments

Fetch only unresolved threads, and read only what you need to act:

- List unresolved review threads — GitHub exposes `isResolved` on review threads through the GraphQL API; the REST comments endpoint does not, so filter resolved ones out yourself before acting.
- Read each comment's **body and the file/line it points at**, nothing more. Don't dump entire JSON responses or unrelated payload fields into context.
- After you've addressed a thread, resolve it (GraphQL `resolveReviewThread`, or the UI). Reply briefly when an explanation helps.

Triage each comment before acting on it:

- **Fix now** — a real bug, regression, correctness or security issue, or a clear violation of the repo's conventions.
- **Usually fix** — a duplicated helper, misleading name, unnecessary indirection, or a genuinely confusing bit of code.
- **Defer / document** — a valid point that's out of this PR's scope; note it (a follow-up issue or a reply) instead of expanding the PR.
- **Reject** — wrong, or would broaden scope / conflict with repo conventions; reply with a short, specific reason.

Validate bot comments (Bugbot, CodeRabbit, Copilot, etc.) the same way as human ones — they produce false positives. Act only on the valid ones, and say plainly when you disagree or are unsure rather than silently complying.

## 4. CI

Fix failures **caused by changes in this PR's scope**. Read the failing job's logs, reproduce locally where you can, and push a targeted fix.

- Never edit CI checks or workflow files just to make a failure pass, and never make unrelated code changes to placate a check. If a fix would require either, stop and report instead.
- For a merge-blocking failure that looks unrelated to your changes, first check whether the branch is `BEHIND` and merge latest base — another PR may have already fixed it.
- After pushing, re-watch CI rather than assuming green: `gh pr checks --watch`.

## Scope discipline

Everything you change should trace back to a conflict, a failing check, or a valid review comment on *this* PR. If getting to mergeable would require broadening scope, altering intended behavior, or touching unrelated code, that's a stop condition — report it, don't do it quietly.

## Stop conditions

Pause and ask the user when:

- A merge conflict has genuinely conflicting intent on the two branches.
- A required check fails for reasons outside this PR's scope, even after merging the latest base.
- Resolving a comment would broaden scope or change intended behavior.
- The only way to make a check pass is to weaken the check itself.

## Report

When the loop ends, report the final state concisely: mergeable yes/no, CI status, which comments you fixed vs. deferred/rejected (and why), any base merges you did, and anything still blocking. Then hand it back — don't merge.
