---
type: concept
tags: [tooling, obsidian, logging, workflow]
created: 2026-08-27
updated: 2026-08-27
aliases: [PROJECT_NOTES.md, mklink, symlink logging]
---

# PROJECT_NOTES.md Symlink

How a code repo's progress log and an Obsidian note stay the same file.

A project repo gets a `PROJECT_NOTES.md` at its root that is a Windows hard link
or symlink to a changelog note inside the vault. Writing to either path writes to
both, so the log lives in the repo where the work happens and in the vault where
it is searchable, without copying anything.

```
mklink "C:\path\to\new-project-repo\PROJECT_NOTES.md" "C:\path\to\vault\...\Updates - X.md"
```

Run it from an elevated prompt. `mklink` with no flag creates a symbolic link to
a file; `mklink /H` creates a hard link, which survives the target being moved by
some editors and does not need elevation.

## Why it is worth keeping

The global instruction "log this" or "update notes" checks for `PROJECT_NOTES.md`
in a repo root. This is the mechanism that makes that instruction land in the
vault rather than in a file nobody reads again.

## Caveat

If the vault side is ever deleted and recreated, the link breaks silently and
writes go to a fresh unlinked file. Worth re-checking after any vault move,
including the 2026-08-27 migration. See
[[decisions/vault-as-single-source-of-truth|the vault migration decision]].
