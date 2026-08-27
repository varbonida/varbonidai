# SETUP.md — One-Time Onboarding

> **To the agent running this:** this file is a script, not a reference doc. Run it once, top to bottom, with the human in the loop. At the end you will have (1) a bootstrapped Obsidian vault and (2) a new `CLAUDE.md` file that becomes the permanent operating manual for every future session. Once `CLAUDE.md` exists and the vault is bootstrapped, this file is done — archive it per Step 4 and never run it again. Do not treat this file as a place to keep adding rules later; ongoing rules live in `CLAUDE.md`.
>
> **This file never runs `git commit`.** Neither will `CLAUDE.md`. Every step below that changes the vault ends by telling the human what changed and suggesting a commit message — the human stages and commits everything themselves.

## Philosophy (read this first)

This vault is not a RAG dump. It's a persistent, compounding second brain. Three layers:

- **`raw/`** — immutable source material (articles, transcripts, PDFs). You read from it, never edit it.
- **The wiki** (`people/`, `clients/`, `research/`, `concepts/`, `personal/`, `questions/`, `decisions/`) — the living, canonical layer. You own it entirely: create pages, update them as new information arrives, maintain cross-links, keep it internally consistent.
- **`CLAUDE.md`** — the schema. It tells you (future-session you) how the wiki is structured and what the rules are.

The core operating loop, always:

**Conversation → extract durable knowledge → find canonical home → create/update canonical page → link related knowledge → log the operation.**

Conversations are a *source* of information, not the primary unit of memory. Don't file transcripts — extract what's durable and integrate it into canonical pages. The full rule for this is written into `CLAUDE.md` in Step 3.

---

## Step 0 — Bootstrap the folder structure

Create, if not already present:

```
raw/
people/
clients/
research/
concepts/
personal/
questions/
decisions/
index.md
log.md
changelog.md
```

If a git repo doesn't already exist at the vault root, `git init` it now — but do **not** commit anything yet. Leave the initial state uncommitted; you'll surface a suggested first commit message at the end of Step 2.

---

## Step 1 — Interview the human

Ask these conversationally, in your own words, not as a rigid form. Don't ask everything in one wall of text — go section by section, let the answers inform follow-ups. Take real notes as you go; you'll turn them into pages in Step 2.

### Identity & role
- What's your name, and what do you do? (role, company/independent, industry)
- What are the 3–5 things that make up most of your working life right now? (This becomes the initial shape of `clients/`, `research/`, `personal/`.)
- Anything about how you think or work that's useful context — e.g. "I context-switch across a lot of small clients" or "I go deep on one thing for months."

### Voice & style
- Ask for 2–3 short samples of their actual writing (an email, a Slack message, notes — whatever's natural) rather than asking them to *describe* their voice abstractly. Voice is easier to show than tell.
- Ask: when you draft things on my behalf, what should I lean toward or avoid? (tone, formality, length, quirks)

### Clients & projects
- Walk through each active client by name. For each: what's the relationship, what project(s) are live, what's the current status of each, anything urgent or overdue.
- Ask if there are past/paused clients worth a page now, or if those can be added later as they come up.

### Research & personal threads
- Any topics they're currently going deep on (research, in the philosophy-doc sense)?
- Any personal threads worth tracking from day one — goals, health, self-improvement — or should `personal/` start empty and fill in as it comes up?

### Working preferences
- Confirm: file things at session end, flagging anything ambiguous for a quick confirm rather than filing it silently (this is the default — see the session-end workflow in `CLAUDE.md`). Any exceptions they want called out now?
- Confirm: Claude Code never runs `git commit` on its own, ever — the human always reviews and commits manually. Confirm this matches their expectations.
- Anything they explicitly do NOT want tracked in the vault (sensitive topics, specific clients, etc.)?

---

## Step 2 — Bootstrap the vault from the interview

1. Create `people/me.md` — the human's own identity page. Keep it compact (this is a reference profile, not a journal):
   ```yaml
   ---
   type: person
   tags: [self]
   created: <date>
   updated: <date>
   aliases: [<name>]
   ---
   ```
   Sections: `## Role`, `## Focus Areas`, `## Voice & Style` (include the 2-3 sample snippets + notes), `## Working Preferences`, `## Revision History`.

2. For each client mentioned: create the client folder `clients/<client>/` with its canonical `overview.md` (contacts, relationship, status, links to each project). Then, for **every** project under that client, create a **dedicated project folder** — never a bare file directly inside `clients/<client>/` — containing at minimum its own `overview.md`:
   ```
   clients/
   └── <client>/
       ├── overview.md
       └── <project>/
           ├── overview.md
           └── ...              # notes.md, decisions.md, etc. only as warranted
   ```
   `clients/<client>/<project>/overview.md` is the canonical project page. Give every project its own folder even if `overview.md` is the only file in it at first. Don't pre-create `notes.md`, `decisions.md`, or other supporting files speculatively — add them once there's real content that belongs in them (see the "don't over-file" rule in `CLAUDE.md`).
   Standard frontmatter on all of these: `type: client` / `type: project`, `tags`, `created`, `updated`, `status: active|paused|completed`, `aliases`.

3. For research/personal threads mentioned: create stub pages in `research/` or `personal/` with what's known so far — it's fine if these are short.

4. Create `index.md` as a catalog of canonical pages and important entry points. Add each canonical page once, grouped by folder/category. Do not treat `index.md` as a historical record of page creation.

5. Create `log.md` with the first entries, one per page created, using the format from `CLAUDE.md` Step 3 below (e.g. `## [2026-08-27] ingest | Bootstrapped vault from onboarding interview`).

6. Create empty `changelog.md` with just a header — it starts accumulating from the first real major change onward.

7. Do **not** run `git commit`. Instead, show the human:
   - the resulting folder tree and `people/me.md`, for a sanity check;
   - a summary of every file created;
   - a suggested commit message: `Bootstrap vault from onboarding interview`.

   The human stages and commits it themselves.

---

## Step 3 — Write `CLAUDE.md`

Generate a new file, `CLAUDE.md`, at the vault root, using the template below. Fill in the `<...>` placeholders from the interview. This file — not `SETUP.md` — is what every future session reads first.

````markdown
# CLAUDE.md — Wiki Operating Manual

This vault is a persistent, compounding second brain for <name>, following the
LLM-wiki pattern: raw sources are immutable, the wiki is the living canonical
synthesis layer, this file is the schema. You (the agent) own the wiki layer
entirely.

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
- `people/` — <name> (`me.md`) and any recurring collaborators/contacts.
- `clients/` — client relationships and projects. See "Client & project
  structure" below.
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
- `index.md` — catalog of canonical knowledge pages and important entry
  points.
- `log.md` — append-only operational history.
- `changelog.md` — append-only, human-facing record of major changes only.

## Canonical page principle

**Every durable subject should have one canonical home.** Other pages link to
it rather than duplicating its information.

- person → `people/`
- client → `clients/<client>/overview.md`
- project → `clients/<client>/<project>/overview.md`
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
- organize newly added raw sources when explicitly instructed, provided the
  original files themselves are not modified.

The agent must not:

- rewrite or "clean up" raw source content;
- rename raw source files;
- move raw source files between folders;
- delete raw source files;
- overwrite a raw source with a summarized or processed version.

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
status: active | paused | completed   # clients/projects only
        open | resolved               # questions only
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
````

Save this file at the vault root as `CLAUDE.md`. Show it to the human — do not commit it. Include it in the same uncommitted-changes summary as the rest of Step 2/3's output, with a suggested commit message covering both, e.g. `Bootstrap vault and write CLAUDE.md operating manual`.

---

## Step 4 — Archive this file

Once `CLAUDE.md` exists, the vault is bootstrapped, and the human has confirmed both look right:

```
mkdir -p raw/_setup-archive
mv SETUP.md raw/_setup-archive/SETUP-completed-<YYYY-MM-DD>.md
```

Do **not** run `git commit`. Notify the human that `SETUP.md` has been archived and suggest the commit message: `Complete onboarding and archive SETUP.md`. The human commits it themselves.

From this point on, every session starts by reading `CLAUDE.md`, not this file. `SETUP.md` is not a place for ongoing rules — if something needs to change permanently, it changes in `CLAUDE.md`, not here.
