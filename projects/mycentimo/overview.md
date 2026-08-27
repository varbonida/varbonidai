---
type: project
tags: [mycentimo, pwa, nextjs, supabase, personal-finance, own-project]
created: 2026-06-30
updated: 2026-08-27
status: active
aliases: [MyCentimo, money tracking PWA, finance tracker]
---

# MyCentimo

Vergel's own project. See [[people/me|me]].

An offline-capable money and budget tracking PWA. Started 2026-06-30 as
something to use himself, with launching to other users as a stated later goal.

Reference point at the start was tarsi.cloud, with the offline-first PWA angle
as the deliberate difference from other finance apps.

## Status

Shipped through three versions and restructured onto Next.js. No public launch
recorded. No repo path captured in the source conversation, so that needs
filling in.

## Stack

Next.js App Router, deployed to Vercel. Supabase for auth and data, with
separate `mycentimo_dev` and `mycentimo` databases so production is not being
developed against. Server-side rendering for public pages, client-side for the
app screens.

UI came out of Google Stitch (`stitch_mycentimo_minimal_finance_tracker`), built
with an Antigravity coding agent. Secrets moved to `.env` as an explicit pass.

## How it got here

- **v1** - local-only storage, no backend, clean and minimal. Deliberately
  shipped before deciding on sync.
- **v2** - budgets, recurring transactions, CSV export covering transactions,
  accounts, and goals. Over-budget warns at the point of adding the transaction
  that breaks it, rather than after the fact.
- **v3** - Supabase sync across phone and laptop. Email/password and Google
  sign-in. Existing local data auto-migrates to the account on first login.
- **Restructure** - moved onto Next.js App Router for Vercel.

## Design decisions worth keeping

- **Guest mode is first-class.** Someone can use the whole app without an
  account, stored locally, and gets prompted to sign up only when they try to
  sync or close the app. Their local data migrates automatically if they do.
  That removes the signup wall that kills most finance-app trials.
- **Recurring transactions confirm rather than auto-post.** The app asks on
  open instead of silently creating entries, and the amount is editable at
  confirmation time because real recurring bills vary.
- **One level of subcategories, and a subcategory belongs to exactly one
  category.** Chosen over arbitrary nesting to keep budgeting coherent.
- **Mark-as-paid resets monthly**, with the month's recurring set written into
  the Supabase recurring table at the start of each month.

## Open

- Where is the repo, and is it public or private?
- Is it deployed anywhere public, or still local and Vercel-preview only?
- Launching to other users was the stated goal. Nothing about pricing, hosting
  cost at scale, or handling other people's financial data has been decided,
  and that last one carries real obligations.

## Why it matters beyond itself

This is a genuine, finished, publicly showable piece of work that is entirely
Vergel's own, with no client confidentiality attached. That makes it one of the
two strongest candidates for a real case study on
[[projects/portfolio/overview|the portfolio]], which currently ships six
placeholder entries.

## Revision History

- 2026-08-27 - Page created from the 2026-06-30 build conversation in the
  Claude.ai export. The conversation itself was not filed; only the durable
  decisions were extracted.
