---
name: ship
description: Take the current branch from done-coding to merge-ready in one pass — review the diff against the repo's conventions, deslop, commit and push, open a PR with a structured description, then babysit until mergeable. Use when the user types `/ship` or asks to ship, finalize, or land the current branch.
disable-model-invocation: true
---

# Ship

Sequential release pipeline for the current branch. Run only when explicitly invoked — it commits, pushes, and opens a PR.

Each stage runs in order. Do not advance while a stage still has unresolved findings.

Copy this checklist and track progress:

```
Ship progress:
- [ ] 1. Review the diff against the repo's conventions
- [ ] 2. Deslop the touched code
- [ ] 3. Commit and push
- [ ] 4. Open the PR
- [ ] 5. Babysit to merge-ready
```

## 1. Review against the repo's conventions

Find and read the repo's contributor guidance first (its rules change): check for `AGENTS.md`, `CLAUDE.md`, `CONTRIBUTING.md`, or a docs directory, in that order. Then review this branch's diff against those rules — run `/review` or `/code-review` if available, otherwise review the diff yourself. Fix real violations before continuing. Pause for the user only if a fix would change behavior or broaden scope.

## 2. Deslop

Run `/deslop` ([`../deslop/SKILL.md`](../deslop/SKILL.md)) to simplify the recently modified code while preserving functionality, including its duplicate-consolidation pass. Apply the refinements before committing.

## 3. Commit and push

- Stage only the intended changes; never commit secrets.
- **Changeset** (only if the repo uses one — look for a `.changeset/` directory): add a changeset when a published package's user-facing behavior changed. Run the repo's changeset command (e.g. `pnpm changeset`, `npx changeset`) unless the user asks for a manual file; select the affected package(s); pick the bump level the change warrants (`patch` for fixes and small refinements, `minor` for additive behavior, `major` for breaking changes); summarize the user-visible behavior. Skip the changeset for private-only, docs-only, test-only, or tooling-only changes, and note why.
- Run the repo's configured checks that fit the change before committing. Discover them from `package.json` scripts, a `Makefile`, `justfile`, `Taskfile`, or the contributor docs — typically the project's test, lint, typecheck, and format-check commands, invoked with the repo's package manager/runner.
- Write a concise commit message in the repo's style, focused on the *why*.
- Push the branch, setting upstream with `-u` on the first push.
- Git safety: no force-push to the default branch, no skipped hooks, no `git config` changes.

## 4. Open the PR

Create the PR with `gh pr create`, passing the body via a heredoc. If the repo ships a PR template, follow it. Otherwise use this structure:

````md
## Why

<What this change accomplishes and the underlying reason, in 1-3 sentences.>

Before:

```
<the problem / prior behavior — code, output, or description>
```

After:

```
<the new behavior>
```

## What changed

- <key change>
- <key change>

## Test plan

- <command or manual step that verifies it>
- <command or manual step, or "Not run" with the reason>
````

Return the PR URL.

## 5. Babysit

Run `/babysit` ([`../babysit/SKILL.md`](../babysit/SKILL.md)) to drive the PR to merge-ready: resolve merge conflicts preserving intent, triage unresolved comments (including review bots), and fix in-scope CI in a loop until the PR is mergeable, green, and its comments are triaged. Report back instead of merging.

## Stop conditions

Pause and ask the user when:

- Review or babysit surfaces a change that would broaden scope or alter intended behavior.
- A merge conflict has genuinely conflicting intent on the two branches.
- CI fails for reasons outside this branch's scope even after merging the latest base.
