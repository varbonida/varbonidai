# CLAUDE.md — Wiki Operating Manual

This vault is a persistent, compounding second brain for Vergel Arbonida,
following the LLM-wiki pattern: raw sources are immutable, the wiki is the
living canonical synthesis layer, this file is the schema. You (the agent) own
the wiki layer entirely.

Core operating loop, always:

**Conversation → extract durable knowledge → find canonical home →
create/update canonical page → link related knowledge → log the operation.**

Conversations are a source of information, not the primary unit of memory.

## Folder structure

- `raw/` — immutable source material. Raw source files must never be edited,
  renamed, moved, or deleted by the agent. The agent may read, reference, and
  link to files in `raw/`, but must treat them as permanent source-of-truth
  artifacts. Any derived knowledge belongs in the wiki layer, never by
  modifying the original source.
- `people/` — Vergel (`me.md`) and any recurring collaborators/contacts.
- `clients/` — client relationships and projects. See "Client & project
  structure" below.
- `projects/` — Vergel's own projects, the ones nobody is paying for. Same
  shape as a client project: `projects/<project>/overview.md` is canonical,
  supporting files beside it only when warranted. Anything with a paying
  client belongs under `clients/`, never here.
- `research/` — topics being actively explored in depth.
- `concepts/` — standalone ideas/terms worth their own canonical page.
- `personal/` — personal goals, self-improvement, and other durable personal
  threads. Kept separate from `people/me.md` — see "people/me.md" below.
- `questions/` — open questions being actively tracked. When answered,
  update the relevant canonical page with the answer and mark the question
  resolved. Resolved questions should normally be removed/archived unless
  the question or its history has independent future value.
- `decisions/` — significant decisions with independent future value beyond
  any single project. See "Decisions" below.
- `prompts/` — the Prompt Library. Reusable AI prompts and instructions. Sits
  beside the wiki, not inside it — see "The Prompt Library" below.
- `index.md` — catalog of canonical knowledge pages and important entry
  points.
- `log.md` — append-only operational history.
- `changelog.md` — append-only, human-facing record of major changes only.

## Canonical page principle

**Every durable subject should have one canonical home.** Other pages link to
it rather than duplicating its information.

- person → `people/`
- client → `clients/<client>/overview.md`
- client project → `clients/<client>/<project>/overview.md`
- own project → `projects/<project>/overview.md`
- research topic → `research/`
- concept → `concepts/`
- personal thread → `personal/`
- open question → `questions/`
- significant cross-cutting decision → `decisions/`

## Raw sources are immutable

`raw/` is the source-of-truth layer.

The agent must **never edit, rename, move, or delete** files inside `raw/`.
This includes source documents, clipped articles, PDFs, transcripts, images,
and other original source material.

The agent may:

- read and analyze raw sources;
- create links to raw sources;
- extract knowledge from raw sources into canonical wiki pages;
- move a file **out of `raw/inbox/`** as the final step of ingesting it, and
  only then. See "The inbox" below.

The agent must not:

- rewrite or "clean up" raw source content;
- rename raw source files;
- move raw source files that have already been filed out of the inbox;
- delete raw source files;
- overwrite a raw source with a summarized or processed version.

### The inbox

`raw/inbox/` is the drop zone. It is the only mutable part of `raw/`, and the
only place the agent may move a file out of.

```
raw/
├── inbox/                  # you drop files here
├── clients/<client>/       # filed, frozen
├── research/<topic>/       # filed, frozen
├── personal/               # filed, frozen
└── _setup-archive/         # filed, frozen
```

Filed sources mirror the wiki's top-level, so `raw/clients/kelly/` holds every
source that fed Kelly's pages. Once a file leaves the inbox it is frozen
permanently, exactly like the rest of `raw/`.

Ingestion, in this order, because the order matters:

1. Read the file in `raw/inbox/`.
2. Decide where it belongs and extract the durable knowledge.
3. **Move the file to its filed location first.**
4. **Then** write the canonical pages, linking to the filed path.

Steps 3 and 4 are that way round on purpose. Writing the links first and moving
the file afterwards leaves every link pointing at an inbox path that no longer
exists.

Notes on the inbox:

- An empty `raw/inbox/` means everything has been ingested. That is the whole
  point of the drop zone: it makes "what still needs processing" visible at a
  glance instead of something to remember.
- Never move a file out of the inbox without ingesting it. The move is what
  marks it done, so moving it early makes the inbox lie.
- Filed does not mean off-limits to read. A source can be re-read any time,
  including to extract something missed the first pass. Filed only means "this
  file has been through ingestion once", never "this file is finished with".
- Never ingest a file into a page without saying so in `log.md`. The log and the
  inbox are the two independent records of what has been processed.

If a raw source needs correction, transformation, or annotation, create a
derived file outside the original source or record the information in the
appropriate canonical wiki page. Preserve the original source unchanged.

## Client & project structure

Every client gets its own folder. Every project gets its own dedicated
folder inside that client's folder — **never** a bare file directly inside
`clients/<client>/`, and never `clients/<client>/<project>.md`:

```
clients/
└── <client>/
    ├── overview.md              # canonical client page
    └── <project>/
        ├── overview.md          # canonical project page
        ├── notes.md             # only if warranted
        ├── decisions.md         # only if warranted
        ├── todos.md             # only if warranted
        ├── meeting-notes.md     # only if warranted
        └── deliverables/        # only if warranted
```

- `clients/<client>/overview.md` is the canonical client page — contacts,
  relationship, overall status, links to every project folder.
- `clients/<client>/<project>/overview.md` is the canonical project page —
  status, summary, links to whatever supporting files exist.
- When a new project starts, create its folder and `overview.md`
  immediately, even if there's nothing else to put in it yet.
- Only add supporting files (`notes.md`, `decisions.md`, `todos.md`,
  `meeting-notes.md`, `deliverables/`, etc.) once there's real content that
  benefits from having its own file — don't pre-scaffold them speculatively.
- Project-level decisions worth a quick record live in
  `clients/<client>/<project>/decisions.md`. A decision gets promoted to its
  own canonical page in top-level `decisions/` only when it has independent
  future value beyond that one project.

## Frontmatter (every canonical page)

```yaml
---
type: person | client | project | research | concept | personal | question | decision
tags: [...]
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: active | planned | paused | completed   # clients/projects only
        open | resolved                        # questions only
aliases: [...]                        # for flexible [[wikilinks]] and search
---
```

Other page types don't need `status` unless it's genuinely useful for that
specific page.

## Search before creating — every durable subject has one home

Before creating any new page, search the existing vault first: check for
exact matches, aliases, alternative names/spellings, synonyms, and related
canonical pages that might already represent this subject (checking
`index.md` is a good first move). If an existing canonical page already
represents the subject, **update it — never create a duplicate.**

Only create a new page once you've confirmed nothing existing already
covers it.

## Don't over-file

Not everything mentioned deserves a page. Create a canonical page when the
information:

- has durable future value,
- is likely to be referenced again,
- represents a meaningful entity/topic/project/concept/question/decision,
- benefits from having a stable canonical home.

Minor facts, temporary details, casual remarks, and one-off information
should normally be absorbed into an existing page, logged in `log.md` if
operationally relevant, or simply not stored at all. The goal is a useful
second brain, not maximum documentation.

### What does not belong in this vault

Concrete cases, because the rule above is easy to agree with and hard to
apply:

- **Daily notes or a journal.** Chronological pages mean nothing is
  canonical: the same fact scatters across nine dated entries, and "what is
  the status of X" becomes "read six months of notes". `log.md` already
  records what happened when. Never create a daily-note habit here.
- **Task lists.** Where a client has their own tracker, that is where work
  lives. A second task list in the vault disagrees with it within a week,
  and the client is looking at the other one. The vault holds knowledge, the
  tracker holds work. Status checkboxes on a project page are a snapshot of
  where things stand, not a to-do list to maintain.
- **Dataview, Templater, or any community plugin's syntax.** No community
  plugins are installed and that is deliberate. A Dataview query is an
  unreadable code block in plain Markdown, on GitHub, and to any agent that
  is not rendering Obsidian. At this scale a hand-written list is better.
- **Anything the repo already tells you.** File structure, dependency lists,
  what a function does, what a commit changed. `git log` is better at that
  and never goes stale. Analysis with conclusions in it (an audit, a
  decision, a root cause) earns a page; an inventory of the codebase does
  not.
- **Binaries and deliverables.** APKs, PDFs, exported designs, video,
  archives. Git keeps every version forever, so the repo never recovers from
  them. Reference where they live instead: releases, drives, the client's
  own systems.
- **Course and tutorial notes that restate the documentation.** Write down
  what surprised you, what you decided, and what broke. Not the parts that
  can be re-read from the official docs in thirty seconds.
- **Credentials of any kind**, including bank and payout details. See
  "Vault-specific rules".

## New topics introduced through conversation

A conversation can introduce a genuinely new topic that doesn't yet exist in
the vault — e.g. you start discussing "Facebook Automation" and no relevant
page exists. When that happens:

1. Search the vault first (see "Search before creating" above).
2. Determine the appropriate canonical location based on the nature of the
   topic (a research topic goes in `research/`, a new client project goes in
   `clients/<client>/<project>/overview.md`, etc.).
3. Create the canonical page there.
4. Extract and store the useful, durable knowledge from the conversation —
   not the conversation itself.
5. Link it to relevant existing pages.
6. Update `index.md`.
7. Update `log.md`.
8. Notify the human about the new page.
9. Include a suggested Git commit message in that notification.
10. Never create a conversation page merely because the topic was
    introduced through conversation.

If a conversation introduces a genuinely new client project, this means
creating `clients/<client>/<project>/overview.md` (and the client folder
too, if the client itself is new) — never a conversation page.

If the topic already exists — a project, client, concept, or anything else —
**update the existing canonical page.** The topic becomes the memory, not
the conversation.

## The conversation-absorption rule

**Do not create standalone conversation pages by default.** A standalone
conversation page should be rare.

Never create one merely because a conversation was long, important, or
introduced a new topic. Do NOT create something like
`conversations/2026-08-27-facebook-automation.md` just because Facebook
Automation was discussed — create/update `research/facebook-automation.md`
(or whatever canonical page fits) instead.

Only create a standalone conversation page when the transcript, reasoning
process, brainstorm, negotiation, or decision-making history itself has
independent future value beyond the knowledge it produced.

## Memory update protocol

When new information relates to an existing page:

- Update the existing canonical page in place.
- Update its `updated` date.
- Maintain relevant cross-links.
- Do not create a duplicate page.

When new information **contradicts** what's already on a page:

- Do not silently overwrite important historical information.
- Update the current/live value.
- Add an entry to a `## Revision History` section at the bottom of the page,
  containing: old value, new value, date, and source/context.

## Source of truth

The vault distinguishes between source material and synthesized knowledge.

- `raw/` contains original source material and is the evidence layer.
- Wiki pages contain synthesized, interpreted, and organized knowledge.
- Never present an LLM-generated synthesis as though it were directly stated by a source.
- When a claim matters, preserve a link or reference back to its source when available.
- When sources disagree, preserve the disagreement rather than forcing a false consensus.

## Decisions

Two tiers:

- **Project-scoped decisions** live in `clients/<client>/<project>/decisions.md`.
- **Top-level decisions** live in `decisions/<decision>.md`, and are reserved
  for decisions with independent future value beyond a single project —
  e.g. a strategic business decision, a personal decision, a reusable
  policy, a decision affecting multiple projects, an important
  architectural/operational decision, or a precedent worth remembering
  independently.

Do not create a top-level decision page for every small decision — most
decisions belong at the project level or don't need their own page at all.

## Questions

Questions are for genuinely open questions that are worth tracking over
time. They are not a permanent archive of everything the human has ever
asked.

When a question is answered:

1. Update the relevant canonical page with the durable answer or conclusion.
2. Mark the question page's frontmatter `status: resolved`.
3. Add a brief note explaining how/when it was resolved and link to the
   canonical page containing the answer.
4. Remove or archive the resolved question page unless the question,
   investigation, or history itself has independent future value.
5. If the answer reveals a new durable topic, concept, decision, or research
   area, create or update its canonical page according to the normal
   canonical-page rules.
6. Update `index.md` if the question page was removed, archived, or a new
   canonical page was created.
7. Log the resolution in `log.md`.

Do not leave resolved questions indefinitely in `questions/` simply for
historical completeness. The goal is for `questions/` to represent what is
currently unresolved, while durable knowledge belongs in its canonical home.

## `index.md`

`index.md` is a catalog of **canonical knowledge pages and important entry
points** — not an exhaustive listing of every supporting file. For a project
with `overview.md`, `notes.md`, and `decisions.md`, the index references
`[[clients/<client>/<project>/overview]]`, not all three files individually.

## `log.md` format

Append-only, most-recent-last, one line per meaningful operation,
grep-friendly:

```
## [YYYY-MM-DD] type | subject
```

Types: `ingest`, `update`, `query`, `decision`, `client-log`, `lint`,
`major-change`.

Example: `grep "^## \[" log.md | tail -5` gives the last 5 operations.

Log meaningful operations: new page creation, meaningful page updates,
source ingestion, significant decisions, client updates, lint passes, major
changes. Don't create noisy log entries for every tiny edit.

## `changelog.md` format

Same date-prefixed format, but only major changes, with one line of
context:

```
## [YYYY-MM-DD] <what changed> — <why it's major>
```

Major changes: new client, new project, new person, new research topic, new
concept, new top-level decision page, a major contradiction/reversal, or a
significant structural change. Routine edits stay in `log.md` only.

## `people/me.md`

Keep it compact — an identity and working-context reference, not a journal.
It should answer "who is this person and how do they work?" Sections:
`## Role`, `## Focus Areas`, `## Voice & Style`, `## Working Preferences`,
`## Revision History`.

Durable personal threads (goals, self-improvement, ongoing personal
projects/systems) belong in `personal/`, not here. Don't turn `me.md` into a
dumping ground for personal notes.

## Voice capture

Update `## Voice & Style` on `people/me.md` **opportunistically**, only when
a strong, useful example naturally comes up. Don't mine every conversation
for voice/style signals.

## Session-start workflow

Nothing survives a session except what was written to a file. This file is the
schema; it does not tell you the current state of anything. Load that first.

At the start of every session, before doing any work or asking any questions:

1. Read `index.md`. It is the map of what exists.
2. Read the last few entries of `log.md`
   (`grep "^## \[" log.md | tail -10`) to see what was recently worked on.
3. Read the canonical page for whatever the session is about, if one exists.
   Do not rely on what `index.md`'s one-line summary says a page contains.

Do this even when the request looks self-contained. A question like "what's the
status of the dictation app" has an answer on disk that is better than anything
reconstructable from the conversation.

If the human opens with something ambiguous, steps 1 and 2 usually resolve it
without having to ask.

## Session-end workflow

At the end of every meaningful session:

1. Review what was discussed. Identify durable information.
2. Search the vault before creating anything (see "Search before creating").
3. Update existing canonical pages where appropriate.
4. Create new canonical pages only when warranted (see "Don't over-file").
5. Update relevant cross-links.
6. Update `index.md` when canonical pages are created.
7. Append meaningful operations to `log.md`.
8. Update `changelog.md` only for major changes.
9. Review the resulting changes for consistency.
10. Tell the human what was changed.
11. Tell the human if anything important was ambiguous and needs their input.
12. Provide a suggested Git commit message.
13. Do not run `git commit`. Leave changes unstaged unless staging is specifically requested. The human reviews, stages, and commits everything themselves.

## Git workflow

Claude Code **never** runs `git commit` automatically — not during
onboarding, not during a session, not during archiving. Ever.

At the end of a meaningful session or ingestion/update batch:

1. Make the necessary vault changes.
2. Review the changes.
3. Notify the human that there are uncommitted changes.
4. Give a concise summary of what changed, e.g.:
   ```
   Changes:
   - Added research/facebook-automation.md
   - Updated clients/acme/facebook-automation/overview.md
   - Updated index.md
   - Updated log.md
   ```
5. Give a suggested commit message, e.g.:
   ```
   Add Facebook automation research and update Acme project
   ```
6. Do **not** run `git commit`.

Do not require the human's approval for every individual file edit within a
session — batch the work, then surface the summary and suggested commit
message at the end. The human reviews, stages, and commits everything
themselves.

## Linting

On-demand only, when asked to "lint" or "health-check" the wiki. Check for:
contradictions, stale information superseded by newer sources, duplicate
pages, orphan pages with no inbound links, missing cross-links, concepts
that repeatedly appear but lack a canonical page, structural
inconsistencies, and gaps that could benefit from research. Report
findings; do not automatically make potentially meaningful fixes without
confirmation. Log the lint pass in `log.md` as type `lint`.

## Tooling

Keep the system intentionally simple. Required: Obsidian, Markdown, Claude
Code, Git. Do not introduce RAG, embeddings, databases, qmd, MCP servers, or
other automation as *required* infrastructure — the vault must work without
them. Search/index tooling can be added later if the vault grows enough to
justify it (`index.md` is sufficient at this scale).

## Working from a code repo instead of the vault

A session running inside a code repo should not crawl the vault. The
session-start workflow above is for vault sessions.

Repos are linked to the vault with a hard link: `PROJECT_NOTES.md` in the repo
root is the *same file* as the project's changelog page in the vault. Writing
from either side writes to both, with no copying and no sync step.

```
mklink /H "<repo>\PROJECT_NOTES.md" "<vault>\projects\<project>\updates.md"
```

`/H` makes a hard link rather than a symlink, which survives editors that save
by replacing a file. The command needs an elevated prompt, so the human runs it,
not the agent.

From inside a repo:

- Read `PROJECT_NOTES.md` at session start. That is one file read, and it is
  already the current vault state.
- Read the project's `overview.md` in the vault only when the *why* behind a
  decision actually matters. It is not session-start reading.
- Log progress by appending to `PROJECT_NOTES.md`. It lands in the vault for
  free.
- Never copy vault context into the repo. A copy goes stale and then there are
  two versions of the truth.

If a repo has no `PROJECT_NOTES.md`, say so rather than guessing where to log.

## The Prompt Library

`prompts/` holds reusable AI prompts and instructions. It is deliberately not
part of the wiki layer: a wiki page answers "what do I know about X", a prompt
answers "how do I make an AI do X". Filing prompts under `research/` or
`concepts/` would break the canonical-page principle, so they get their own
folder instead.

Rules:

- One prompt per file, kebab-case filename.
- Each file is frontmatter (`kind: prompt`, `category`, `tags`, `created`,
  `updated`), then an H1, then a short description of what the prompt does and
  when to use it, then the prompt itself inside a code fence.
- The fenced block must be self-contained and copy-ready. Anything
  situation-specific is a `<PLACEHOLDER>` the user fills in, never a hardcoded
  path or client name.
- `prompts/index.md` catalogs everything by category and keeps a "Recently
  Added" list. Update it whenever a prompt is added or renamed.
- `prompts/` is not listed page-by-page in `index.md`; the root index links to
  `prompts/index.md` only.
- Never file a prompt here just because it worked once. It belongs here when it
  is genuinely reusable across projects.

## Vault-specific rules

Established during onboarding on 2026-08-27. These are as binding as
everything above.

**Never store bank or payment credentials.** Account numbers, card details,
and payout credentials do not go in this vault under any circumstances.
Invoicing facts — platform, billing period, what was billed, paid or unpaid —
are fine.

**Editable personal documents live in `personal/`, never `raw/`.** Resumes,
cover letters, and anything else the agent is expected to revise go in the
relevant `personal/` subfolder, because `raw/` is immutable and the agent may
never edit a file inside it.

**Supporting files use `kind:`, not `type:`.** Changelogs, audits, scratch
notes, and billing records are not canonical pages, so they use a `kind:`
field (`changelog`, `audit`, `scratch`, `decisions`, `billing`,
`asset-source`) to keep the canonical `type:` enum unambiguous.

**Every named client project gets a folder immediately, at `status: planned`.**
As soon as a client names a project, create `clients/<client>/<project>/overview.md`
with `status: planned`, even if all that is known is the one line they said.
A planned project's `overview.md` records three things: what is known verbatim,
what is unknown, and the next question that has to be asked. It is not a stub
and it is not empty. The old vault's problem was twelve genuinely empty
placeholder notes, not the folders themselves.

Promote to `status: active` when work actually starts. The client's
`overview.md` keeps a backlog table linking every planned project, so the
client page stays the single place to see the whole relationship.

**Writing style, for everything drafted in this vault.** Direct, plain, and
short. No filler intros, no restating a question before answering it, no
marketing language. Never use em-dashes or double dashes in newly written
prose; use a single hyphen or a comma. Avoid: delve, tapestry, realm,
leverage as a verb, unlock as a verb, foster, elevate, robust, seamless,
powerful, cutting-edge. This applies to client messages, log entries, commit
messages, and page content alike. Text ported verbatim from an older source
is left as written.
