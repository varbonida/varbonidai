---
kind: decisions
project: homemadeeasier
tags: [homemadeeasier, decisions, affiliate-marketing, pinterest]
created: 2026-08-27
updated: 2026-08-28
---

# Home Made Easier - Decisions

Project-scoped decisions, extracted from
[[raw/projects/homemadeeasier/08-28-2026.md|the 2026-08-27 planning conversation]].
See [[projects/homemadeeasier/overview|Home Made Easier]] for current state.

---

## Distribution channel: Pinterest, not short-form video

**Date:** 2026-08-27
**Decision:** Pinterest is the primary distribution channel.
**Why:** Vergel wanted to avoid making videos. Short-form video (TikTok, Reels,
Shorts) is normally the fastest zero-audience path since it doesn't need months
to rank the way a blog does, but Pinterest achieves the same "no existing
audience needed" property without video, and Vergel was already picturing
"Amazon link → Pinterest" before this conversation started.

**Known limitation, accepted going in:** Amazon's affiliate cookie window is
only 24 hours. Pinterest users routinely save a pin and buy days later, so this
is a structural ceiling on conversion for this specific channel, not a
solvable bug. It was flagged and accepted rather than resolved.

## Never link Pinterest directly to Amazon

**Date:** 2026-08-27
**Decision:** Every pin routes to a blog post first, which then links to
Amazon. No pin ever links straight to an Amazon product page.
**Why:** Pinning bare Amazon links risks being flagged as spam by Pinterest's
own detection, and converts worse than a page with real context and a
recommendation behind it. This is also *why the blog exists at all* - without
this rule, a Linktree-style link list would have satisfied "having a site" with
far less work.

## Niche and audience: moms first, not seniors, not split

**Date:** 2026-08-27
**Decision:** Target moms as the primary audience across all three content
pillars (kitchen, garden, home). Seniors were considered and explicitly
deferred rather than folded in.
**Why rejected as a parallel audience:** Pinterest's algorithm learns who
engages with a pin and shows it to more people like them. Splitting content
50/50 between two audiences with different needs and different products
confuses that signal and slows growth for both, rather than reaching either
well.
**Why moms specifically:** Pinterest's core demographic is women 25-54, many
with kids - the platform's own traffic already matches this audience.
Kitchen/garden/home content ("kitchen hacks," "time-saving tools," "gardening
with kids") is exactly what the algorithm already surfaces well. Moms also tend
to buy across all three categories in bursts within the same week, which suits
a multi-topic niche better than a single-category one.
**Why not folded in without saying so:** most kitchen/garden/home products
already appeal to both a mom with limited time and a senior with reduced grip
strength or mobility, without the content needing to say "for seniors"
explicitly. So the audiences overlap naturally without splitting the message.
**Deferred, not dropped:** a senior-focused accessibility angle (jar openers,
non-slip mats, easy-grip tools) was identified as a genuine, underserved niche
- planned as a second board or even a second site once the moms angle has
proven traction, not attempted from day one.

## Name: Home Made Easier

**Date:** 2026-08-27
**Decision:** Site named "Home Made Easier."
**Supersedes:** "The Easier Home" was the first choice and was already taken.
Name variations were suggested and Vergel picked this one directly rather than
from that generated list.
**Caveat carried over from the conversation:** no live domain availability
check was actually done at the time of naming - it was suggested as a strong
candidate to verify on a registrar, not confirmed available. Worth checking
before any real domain purchase.

## Build it themselves on Astro + Vercel, not Blogger

**Date:** 2026-08-27
**Decision:** Code the site and deploy it to Vercel, using an agent to do the
actual implementation.
**Alternatives considered and rejected:**
- **WordPress.com free tier** - technically free but carries a wordpress.com
  subdomain, ads, and limited customisation. Vergel pushed back on calling this
  "free" and was right to.
- **Blogger** - recommended as the actual fastest free no-code path (genuinely
  free, no coding, `yourname.blogspot.com` is sufficient for Amazon's
  requirements). Not chosen.
**Why coding it anyway was accepted as the right tradeoff:** control, and
Vercel's free tier needs no domain to start (`*.vercel.app` works immediately).
The stated cost of this choice - real time and a technical learning curve on
top of everything else being learned at once (Pinterest, Amazon Associates,
content strategy) - was accepted knowingly, not overlooked.

## Feature scope: add search and categories/tags at launch, against the minimal recommendation

**Date:** 2026-08-27
**Decision:** Build client-side search and a category/tag archive page from the
start, on a `posts.json` single-source-of-truth data file, rather than shipping
posts hand-written into `index.html`.
**Recommendation this overrode:** ship posts, homepage, and an About page only
- no categories, no search, no newsletter signup - on the reasoning that
search and tagging are pointless under a dozen posts and a newsletter provider
is a distraction risk with zero payoff toward getting Amazon-approved or
getting a first click.
**Why Vergel overrode it:** explicitly planning for 100+ posts eventually, and
recognising that hand-written HTML per post becomes unmanageable well before
that point, and that search cannot work against hardcoded HTML at all. This is
the direct cause of the site's `posts.json`-driven architecture and its
archive/search page - it exists because of a deliberate scale decision, not
because it was assumed necessary from the start.
**Newsletter signup was still deferred** - accepted as a real distraction risk
this round, revisit once the site has traction.

## Design mode: Read, not Persuade

**Date:** 2026-08-27
**Decision:** The site's design foregrounds comprehension and trust; affiliate
links are a natural next step inside that, not the design's central job.
**Why not Persuade-mode (landing-page energy, foregrounded CTAs):** Pinterest
users who click through are already primed and don't need to be sold again -
a hard-sell design fights the mood they arrive in. Both Amazon's account
reviewers and Pinterest's spam detection are tuned to distrust
conversion-optimised, thin-affiliate-mill patterns, and a Persuade-mode design
reads as exactly that pattern.

## Two failure modes to avoid equally in the visual design

**Date:** 2026-08-27
**Decision:** Avoid both "corporate affiliate-farm gloss" (stock photos,
SEO-content-mill feel) and "twee mommy-blog pastel cliché" (overly precious,
condescending) as roughly equal risks, not just one of them.
**Why both, not one:** gloss undercuts the "I tried this, here's the honest
verdict" voice already established in the one live post - it reads as
optimising for clicks. The pastel-cliché failure undercuts the other half of
the positioning, "busy moms who don't have time to waste" - cutesy, precious
design signals fluff against a practical, no-nonsense audience.
**Target land zone:** clean and credible enough to feel trustworthy, warm and
human enough to not feel corporate - "a friend who's genuinely good at this."
**Palette direction named in the conversation:** sage and warm-neutral tones.
**Superseded, not implemented.** The 2026-08-28 build landed on a different
concrete direction, "The Exposed Binding" (coptic bookbinding / chain-stitch),
chosen and built out that same day. The brief above (Read mode, avoid both
failure modes, "a friend who's genuinely good at this") still holds as the
*intent*; the sage/warm-neutral palette was just an early guess at how to
satisfy it and was never built. See
[[projects/homemadeeasier/overview|Home Made Easier]] for what actually
shipped.
