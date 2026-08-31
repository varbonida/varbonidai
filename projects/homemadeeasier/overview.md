---
type: project
tags: [homemadeeasier, astro, affiliate-marketing, blog, own-project]
created: 2026-08-27
updated: 2026-08-28
status: active
aliases: [Home Made Easier, homemadeeasier.vercel.app]
---

# Home Made Easier

Vergel's own project. See [[people/me|me]]. Repo:
`C:\Users\Vergel\Documents\development\portfolio\homemadeeasier`

A blog of practical, tested product recommendations for the kitchen, garden,
and home, monetised through Amazon affiliate links. This is
[[research/affiliate-marketing|the affiliate marketing research]] put into
practice in a physical-goods niche, alongside
[[projects/redflagger/overview|Redflagger]]'s AdSense/software-niche attempt.

## Status

Early build. One post live (kitchen shears, electric kettle, instant-read
thermometer), placeholder hero image, `site` in `astro.config.mjs` still set to
the default `homemadeeasier.vercel.app` rather than a real domain. Not yet
deployed for real, not yet indexed by anyone.

## Stack

Astro 7 (Content Layer API, static output), Tailwind CSS v4 via
`@tailwindcss/vite`, Pagefind for static search, deployed on Vercel with no
adapter needed since output is fully static.

Posts are Markdown in `src/content/posts/`, validated against a schema
(`title`, `description`, `pubDate`, `category`, `tags`, `heroImage`, `verdict`)
with `category` locked to an enum: `kitchen`, `garden`, `home`.

## Origin

First choice for a name was "The Easier Home" - already taken, so the name
shifted to Home Made Easier. Distribution channel, niche, feature scope, and
design direction were all decided in one planning conversation on 2026-08-27,
before any of the code existed. Full reasoning for each:
[[projects/homemadeeasier/decisions|Decisions]].

## Monetisation

Amazon affiliate links, with a standing `AffiliateDisclosure` component shown
on posts ("we only recommend things we've actually tried," linking to a full
disclosure on `/privacy`). Disclosure-first from the start, not bolted on later.

Real constraints on this specific setup, not general affiliate-marketing facts:

- **Amazon requires ~10 original pieces of content live** before it will
  approve an Associates application. A handful of bare links is not enough.
- **Payouts run NET-60** - roughly 60 days after the month a sale happens, so
  a sale in week one does not turn into money for about two months.
- **3 qualifying sales are required within the first 180 days** of approval or
  the account gets closed (reapplying afterward is possible).
- **The affiliate cookie window is only 24 hours.** Since the traffic strategy
  is Pinterest-driven and Pinterest users often save now, buy later, this is a
  real structural ceiling on conversion for this specific channel - see
  [[projects/homemadeeasier/decisions|Decisions]].

Directly informed by [[research/affiliate-marketing|the affiliate marketing
research]]: one narrow niche rather than "home stuff" broadly, comparison and
verdict-driven content over generic listicles, and the stated 3-6 month wait
before meaningful search traffic applies here too.

## Growth strategy

Pinterest is the intended distribution channel, chosen specifically because it
needs no video and no existing audience. The path is deliberately **Pinterest →
a blog post → Amazon**, never Pinterest straight to an Amazon link - direct
linking risks a spam flag and converts worse than a page with real context
behind it. Every pin needs a visible disclosure line
("As an Amazon Associate I earn from qualifying purchases").

Audience is **moms, deliberately not split with seniors** at this stage, even
though the same kitchen/garden/home products often suit both. A senior-focused
accessibility angle (jar openers, non-slip mats, easy-grip tools) was
identified as a real, underserved niche and deliberately parked as a phase-two
board or site once the moms angle has traction. Reasoning for both calls is in
[[projects/homemadeeasier/decisions|Decisions]].

## Content pillars

Three categories, matching the `content.config.ts` enum, each with a defined
job rather than being a loose bucket:

- **Kitchen** - tools and small systems that cut time or friction at mealtimes.
- **Garden** - low-effort growing for people without time to fuss with a hobby.
- **Home** - organisation and decluttering that reduces daily decision-making.

The through-line across all three: "does this actually make life easier, or is
it just another thing to own" - honest, lived-in verdicts, explicitly not
"best of 2026" listicle framing.

The `verdict` field is mandatory in the schema, not optional editorial flourish
- every post has to commit to an opinion. The one live post's structure is worth
keeping as the template: a real-use framing ("does this save real time on a real
weeknight"), explicit "where it doesn't help" sections per product, and a single
clear verdict at the end. That's the opposite of an AI-slop listicle, which the
affiliate research explicitly flags as a failure mode Google now penalises.

## Architecture: built for scale on purpose

Posts are meant to scale past 100 eventually, which is why the site has a
`posts.json`-style single source of truth and a client-side archive/search page
rather than hand-written post cards in `index.html` - that approach was chosen
deliberately, overriding an initial recommendation to ship posts-only with no
search or categories until the site had more content. See
[[projects/homemadeeasier/decisions|Decisions]] for why. Worth checking that the
built site actually reflects this, since the coding was handed to a separate
agent from the one that made this call.

## Design direction

The site is meant to read as **comprehension/trust-first, not conversion-first**
- affiliate links follow naturally from a real recommendation rather than being
the design's central job. Visual failure modes to avoid, treated as equally
dangerous: looking like a slick affiliate-content-mill, and looking like a
twee, condescending "mommy blog." Target feel: "a friend who's genuinely good
at this." See [[projects/homemadeeasier/decisions|Decisions]] for the full
reasoning behind that brief.

**What actually got built is different from the brief.** The planning
conversation named a sage/warm-neutral palette direction, but that was never
implemented. The real design pass (2026-08-28) landed on **"The Exposed
Binding"** instead - a coptic bookbinding / chain-stitch visual direction,
built out across the sidebar nav, post cards, a key-rail of facts, a verdict
stamp, and the affiliate disclosure. `PRODUCT.md` and `DESIGN.md` in the repo
document it. This is the current design system; the sage/warm-neutral note is
historical only.

One real bug caught after that pass looked finished: the sidebar was pinned to
the true viewport edge, so on an actual desktop monitor the content floated in
a dead void - it had only been checked at 1440px and on mobile. Fixed. Worth
remembering as a screenshot-check gap on this project specifically.

## Open

- Real domain not yet chosen; `site` in `astro.config.mjs` is a placeholder and
  feeds the sitemap, RSS feed, and Open Graph tags, so it needs setting before
  launch, not after. "Home Made Easier" itself was never checked for live
  domain availability, only picked as a strong candidate name.
- Amazon Associates account status unknown: applied, approved, pending, or not
  yet started. The 180-day / 3-sale clock only starts once approved, so this is
  worth confirming rather than assuming it hasn't started.
- Whether the site actually has the planned `posts.json` + search/archive
  architecture, or something else emerged during the build - still
  unverified, unlike the design direction question, which is now answered.
- Hero images are still placeholder SVGs.
- Repo has a GitLab remote (a merge conflict against it was resolved
  2026-08-28); no GitHub remote confirmed.
- Nine more posts needed to clear Amazon's ~10-content minimum for approval;
  only one exists.

## Repo housekeeping

Same ownership issue found on the portfolio repo: `.git` is owned by
`BUILTIN/Administrators` while the working user is `VBA/Vergel`, so plain git
commands fail with "detected dubious ownership." Fix with `takeown`, not with
`git config --add safe.directory`, which only silences the warning rather than
fixing the underlying ownership.

`PROJECT_NOTES.md` is already listed in this repo's `.gitignore`, matching the
portfolio repo's pattern - the hard link stays untracked by this repo's own git
history since the vault already tracks it.

## Related

- [[projects/homemadeeasier/decisions|Decisions]] - the full reasoning behind
  every call summarised above
- [[research/affiliate-marketing|Affiliate Marketing]] - the research this
  project is the physical-goods application of
- [[projects/redflagger/overview|Redflagger]] - the other live affiliate/ad
  attempt, different niche and monetisation model
- [[projects/portfolio/overview|Portfolio Site]] - a second live, real
  case-study candidate once this has real traffic or revenue to point to

## Revision History

- 2026-08-27 - Page created from the repo's README, package.json, and its one
  live post.
- 2026-08-28 - Rewrote Monetisation, added Origin, Growth strategy, Content
  pillars, Architecture, and Design direction sections, and created
  [[projects/homemadeeasier/decisions|Decisions]], all from
  [[raw/projects/homemadeeasier/08-28-2026.md|the 2026-08-27 planning
  conversation]]. Several "Open" items from the previous version (niche
  reasoning, why this stack) are now answered; new open items surfaced instead
  (whether the design direction and planned architecture actually made it into
  the build, since a separate agent did the coding).
