---
type: project
tags: [redflagger, nextjs, pwa, adsense, side-income, own-project, live]
created: 2026-04-22
updated: 2026-08-27
status: active
aliases: [Redflagger, redflagger.online, toxicity meter]
---

# Redflagger

Vergel's own project, and the only one currently live to the public. See
[[people/me|me]].

**Live at redflagger.online.**

A web tool that scores text for toxicity, aimed at people trying to work out
whether a relationship is unhealthy. Built as a deliberately simple, viral,
ad-monetised web tool rather than an app.

## Origin

Came out of a 2026-04-22 ideation pass for low-competition, high-traffic web
tools monetisable through Google AdSense. Ten ideas generated, filtered to
three, then to one. The toxicity meter won.

Known going in: `toxicitymeter.com` already exists. The idea was picked anyway,
so differentiation is on execution rather than novelty.

## Stack

Next.js with TypeScript, Tailwind, App Router, deployed to Vercel. Upstash Redis
for rate limiting, Supabase, OpenAI for the "healthy rewrite" feature,
`html-to-image` and `@vercel/og` for shareable result images. Built with an
Antigravity IDE agent.

Two constraints shaped this: zero spend at the start, and AdSense compatibility.
A component library was deliberately avoided because AdSense's auto-placement
injects into the DOM and conflicts with component styles.

## Monetisation

AdSense is the current model. A later strategy pass also recommended a BetterHelp
therapy affiliate on high-toxicity results and a Beehiiv newsletter opt-in.
**Those were recommendations, not confirmed as implemented** - verify before
treating either as live.

This is the only place a real affiliate-revenue attempt exists. See
[[research/affiliate-marketing|Affiliate Marketing]], whose page needed
correcting because of it.

## Open risks

- **Perspective API is sunsetting.** Toxicity scoring depends on it and a free
  replacement was raised but not settled. This is a live dependency risk on a
  shipped product, not a future problem.
- **No traffic figures recorded.** AdSense revenue is a function of traffic and
  nothing here says what the site actually gets. Without that, every
  monetisation decision is guesswork.
- **The affiliate angle deserves a deliberate decision, not a default.** The
  proposal is to show therapy affiliate links to someone immediately after
  telling them their relationship is toxic. It converts precisely because those
  people are distressed. That can be done well or badly, and the difference is
  whether the recommendation would still be right if it paid nothing. Worth
  deciding on purpose rather than because a strategy doc suggested it.

## Why it matters beyond itself

Live, public, entirely Vergel's own, with a real product decision trail behind
it. Along with [[projects/mycentimo/overview|MyCentimo]], it is one of the two
strongest real case studies available to
[[projects/portfolio/overview|the portfolio]].

## Revision History

- 2026-08-27 - Page created from the 2026-04-22 conversation in the Claude.ai
  export. Ideation, stack selection, and marketing strategy all happened in that
  one thread; only the durable outcomes were extracted.
