---
type: concept
tags: [tooling, obsidian, logging, workflow]
created: 2026-08-27
updated: 2026-08-31
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

## A claimed link is not a verified link

On 2026-08-29, a coding agent working in the Home Made Easier repo logged "Fixed
the PROJECT_NOTES.md hard link itself (was a broken symlink pointing to a
malformed path)." On 2026-08-31 that link was checked directly and it was never
actually linked - a plain file with matching content, not a hard link. The
agent's own changelog entry reporting success was wrong.

The same audit found the `avelisse-android` and `avelisse-ios` links were also
never real links, despite an earlier claim in this vault's own conversation
history that they were "already linked."

**The only real check is comparing inode numbers, not reading a claim.** On
Windows, via a POSIX shell: `stat -c %i <path>` on both the repo file and the
vault file - if the numbers match, it is a genuine hard link; if not, it is two
separate files that may happen to agree today and will silently diverge the
moment either side is edited. Trust the check, not the log entry.
