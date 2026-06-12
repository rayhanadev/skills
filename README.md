# skills

My personal [Claude Code](https://claude.com/claude-code) skills — the ones I reach for day to day. They live here so I can version them, share them, and drop them into any project.

A skill is just a folder with a `SKILL.md` inside: YAML frontmatter (a `name` and a `description` that tells the model when to use it) followed by Markdown instructions. Claude Code loads the frontmatter for every available skill and pulls in the full body only when a skill is actually triggered, so they stay cheap until they're needed.

## The skills

| Skill | What it does | How it fires |
| --- | --- | --- |
| [`ship`](skills/ship/SKILL.md) | Takes the current branch from done-coding to merge-ready in one pass: review the diff against the repo's conventions → deslop → commit & push → open a PR → babysit until mergeable. | `/ship` only (won't auto-invoke) |
| [`deslop`](skills/deslop/SKILL.md) | Simplifies and refines recently-touched code while preserving behavior, and consolidates near-duplicate helpers. | `/deslop`, or "clean up / simplify this code" |
| [`babysit`](skills/babysit/SKILL.md) | Keeps a PR merge-ready: resolves clear conflicts, triages review comments (including bots), and fixes in-scope CI in a loop. | `/babysit`, or "get this PR mergeable" |
| [`voice`](skills/voice/SKILL.md) | Writes prose in my voice — blog posts, READMEs, release notes, anything that should sound like me. | `/voice`, or "write this in my voice" |

`ship` is a pipeline that chains the other three — it's the one I run most.

## Install

These are written to be project-agnostic, so they work as **personal skills** available in every project.

Clone the repo and copy (or symlink) each skill into your Claude Code skills directory:

```sh
git clone https://github.com/rayhanadev/skills.git
cp -r skills/skills/* ~/.claude/skills/
```

Or symlink the folder so you stay up to date with `git pull`:

```sh
ln -s "$PWD/skills/skills"/* ~/.claude/skills/
```

To scope a skill to a single project instead, drop it in that repo's `.claude/skills/` directory.

Restart Claude Code (or start a new session) and the skills show up — type `/` to see them, or just describe what you want and the matching one gets invoked.

## Using them

- **Slash commands:** type `/ship`, `/deslop`, `/babysit`, or `/voice`.
- **Natural language:** ask for what you want ("clean up the code I just changed", "draft a README in my voice") and Claude picks the skill whose `description` matches. `ship` is the exception — it commits and pushes, so it only runs when you explicitly call `/ship`.

## Notes

- The code skills (`ship`, `deslop`, `babysit`) started life in a specific repo and have been generalized to read whatever conventions a project actually ships (`AGENTS.md` / `CLAUDE.md` / `CONTRIBUTING.md`, linter config, neighboring code) instead of hardcoding one stack's rules.
- `deslop` can optionally use [`truffler`](https://github.com/rayhanadev/truffler) to hunt for duplicate functions, but falls back to plain `grep`/`rg` if it isn't installed.

Cheers!
