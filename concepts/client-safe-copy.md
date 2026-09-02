---
type: concept
tags: [tooling, client-sharing, workflow, redaction]
created: 2026-08-31
updated: 2026-09-02
aliases: [client-safe copy, redacted client export]
---

# Client-Safe Copy

A standalone, redacted export of a client's project folder, meant to actually
be shared with that client - as opposed to the vault's own copy, which is
written for internal use and assumes the client will never read it.

First instance: `C:\Users\Vergel\Documents\Obsidian\kelly`, exported from
[[clients/kelly/overview|Kelly]]'s folder in this vault on 2026-08-31.

## Why it's a separate folder, not a link

The vault's client pages contain internal working notes - how to communicate
with the client, candid assessments of their own dictated requests, vault
maintenance history - none of which belongs in front of the client. A hard
link or live sync would copy that content unreviewed the moment it's written.
The two copies are deliberately different documents serving different readers,
not two views of the same data. See
[[concepts/project-notes-symlink|PROJECT_NOTES.md Symlink]] for the opposite
case, where two paths *should* be the exact same file.

## How it stays updated

**On request only - say "sync the kelly folder" (or name the client).** Never
automatically. Each sync:

0. **Pull the client-safe repo's remote first, before touching anything.**
   Once any file in the copy is two-way (see
   [[clients/kelly/communications/index|Communications]]), the client may have
   committed directly on GitHub since the last sync. Skipping this step risks
   overwriting or silently missing something she wrote herself.
1. Diffs the vault's client folder against the existing safe copy - in both
   directions. Vault-authored changes flow out to the copy as before; anything
   new in a two-way file that isn't yet in the vault flows back in.
2. Re-applies the known redaction rules below to anything that changed on the
   vault side. **This includes files that already had a redaction applied
   last time** - re-pushing the vault's raw version over an already-redacted
   file silently reverts the redaction (hit and fixed live on 2026-09-02, with
   [[clients/kelly/chronic-patient-audience/overview|Chronic Patient
   Audience]]'s "Handle with care" heading). Check the redaction checklist
   against every file being pushed, not just files that look new.
3. Flags anything newly written that looks like it needs a fresh judgment
   call - a new backlog item with blunt internal commentary, a new relationship
   note, anything that reads like it was written for the agent rather than the
   client - rather than silently deciding for the human.
4. Re-flattens paths and rewrites links to match the standalone folder's
   structure (no `clients/<client>/` prefix).

A mechanical script could do steps 0, 1 (one direction), 2, and 4. It cannot
safely do step 3 - recognizing genuinely new sensitive content requires
judgment, not a fixed rule list. That is why this is an on-request process,
not a script handed off to run unattended.

## Redaction rules applied for Kelly (2026-08-31)

Reusable checklist for this client's future syncs, and a starting template for
the next client that needs one:

- Remove any "Relationship & Working Style" section, or equivalent - internal
  notes about how the client communicates, written for the agent's reference.
- Remove "Revision History" sections that document vault-maintenance events
  (page creation, what a page used to say) rather than actual project
  decisions. A Revision History that tracks real project decisions (e.g.
  [[clients/kelly/dictation-app/overview|the dictation app's]]) is fine to
  keep - the distinction is "vault bookkeeping" versus "project history."
  Also known to overlap here: an "Outcome" section on
  [[clients/kelly/dictation-app/meeting-notes|meeting notes]] written in third
  person as a note-to-self for after a call - dropped for the same reason.
- Reword headings/framing that sound like a warning about the client rather
  than professional advice - e.g. "Handle with care" read as being about her,
  reframed as "Compliance and reputational considerations," which is about the
  work.
- Soften characterizations of the client's own communication as unreliable,
  even when accurately sourced - state the practical fact (an instruction was
  ambiguous) without the personal framing (attributing that to her).
- Drop any link or section that points to unrelated internal material - e.g. a
  reference to the agent's own side-income research had no reason to be
  reachable from the client's project page.
- Exclude any exported PDF snapshot made before redaction was applied - it
  can't be edited after the fact, so it either gets regenerated from the
  cleaned source or left out.

## What was not touched

Everything factual and already written the way the client would see it:
engineering changelogs, technical decisions, licence audits, invoices, and any
page built from the client's own dictated words presented back to them for
confirmation. Most of a well-written project page needs no redaction at all -
only the sections written explicitly *about* the client, for the agent's
benefit, need review.

## Supporting-file patterns worth knowing before they show up elsewhere

Added for Kelly starting 2026-09-01, and worth reusing as a pattern for any
future client:

- **A client-facing running log** ([[clients/kelly/daily-updates/index|Daily
  Updates]]) - written in plain language from the moment it's created, because
  it's meant for the client to read. Needs no redaction pass on sync; it just
  gets copied straight across. Restructured on 2026-09-02 from one
  accumulating file into one note per week (Wednesday to the following
  Tuesday, matching how Vergel actually thinks about a work week), each still
  holding one dated heading per day worked - same reasoning as the
  communications log below, applied before the file grew large enough for
  anyone to complain about it.
- **A communications log** ([[clients/kelly/communications/index|
  Communications]]) - a running record of what's been discussed and agreed.
  Started as one internal-only file, made client-facing on 2026-09-01 at
  Vergel's explicit request, then restructured again the same day into
  **one dated, titled note per folder entry** (`YYYY-MM-DD - Descriptive
  Title.md`) instead of a single accumulating file, at Kelly's own request -
  she wanted to find a specific past conversation again without scrolling.
  Two lessons worth carrying to the next client:
  - **This kind of file needs an explicit visibility decision recorded in its
    own header, not an assumption carried over from a similar file.** A file
    that logs what a client says can reasonably go either way depending on the
    client and what's actually in it - check the file's own stated visibility
    before syncing it, don't assume by analogy.
  - **A single accumulating log file is not the only shape this can take, and
    the client's own preference should win.** If a client says they want to
    find things again, a folder of dated, titled notes searches and browses
    better than scrolling one long file - ask, or watch for the same
    complaint Kelly raised, rather than defaulting to one file because that's
    how the first version was built.
