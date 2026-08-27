---
type: decision
tags: [vault, tooling, knowledge-management]
created: 2026-08-27
updated: 2026-08-27
aliases: [vault decision, obsidianvault migration]
---

# This vault replaces the old obsidianvault

**Date:** 2026-08-27

## Decision

`varbonidai` is the single source of truth for durable knowledge. The previous
Obsidian vault at `Documents/development/obsidianvault` is superseded. Its Kelly
material has been carried over in full. Nothing in this vault links back to it.

## Why

The old vault was organised as a folder hierarchy of notes with no rules about
where knowledge belongs, which produced predictable problems: a `rebranding.md`
under the Dictation App folder holding mixed Dictation App, Schengen, and Never
Pay Double content; twelve empty placeholder notes that had to be demoted to
plain text because they were dead links; the same project drifting under three
names.

This vault is built on the LLM-wiki pattern instead. `raw/` is immutable source
material, the wiki layer is the canonical synthesis, and `CLAUDE.md` is the
schema that keeps it consistent across sessions. Every durable subject has
exactly one home, and conversations are absorbed into canonical pages rather
than filed as transcripts.

## Consequences

- The old vault is read-only history. If something there still matters, it gets
  ported here rather than referenced in place.
- Two vaults exist on disk until the old one is deleted. That is a real risk of
  editing the wrong copy, and worth resolving.
- Every future session starts by reading `CLAUDE.md`.

## What was ported

Complete as of 2026-08-27:

- `02 Clients/Kelly` in full, including all audits and changelogs
- `03 Prompts Library` to `prompts/`, with the hardcoded old-vault output
  path in `audit-check.md` turned into a placeholder
- `04 Notes` to `research/`
- `00 Inbox/Notes.md` to [[concepts/project-notes-symlink|PROJECT_NOTES.md Symlink]];
  the stale task fragment in it was dropped
- `01 Portfolios` was empty, nothing to move

## Open

- When is the old `obsidianvault` deleted or archived? Leaving it live invites
  confusion about which one is authoritative.
