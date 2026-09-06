---
type: project
tags: [automation, n8n, telegram, google-sheets, docker, self-hosted, personal-project]
created: 2026-09-03
updated: 2026-09-03
status: active
aliases: [automations, tirz sales tracker, n8n stack]
---

# Automations

Vergel's own self-hosted n8n stack and the workflows built on it. Not client
work. Repo: `C:\Users\Vergel\Documents\Automations`

Docker Compose runs n8n plus a sandbox service (API, DinD runner, mTLS
bootstrap) and a SearXNG instance for web search. Workflow JSON is kept in
`n8n/workflows/` and imported, so the repo is the source of truth rather than
whatever is loaded in the running instance.

## Tirz Sales Tracker

Telegram bot `@tirz_sales_tracker_bot` records supplement sales into a Google
Sheet. Built 2026-09-03, not yet run against live data.

Send `/sale Tirz 10mg x2 @450 Maria`. Price and customer are optional, price
falls back to the sheet. A fixed command format was chosen over free text
through an LLM: no per-sale model call, and no silent misparse writing a wrong
number into inventory.

The sheet does two things per sale, decrement stock on Inventory and append a
row to Sales. Trigger is the **Telegram Trigger** node, reached over a
Cloudflare Tunnel (not yet running) rather than n8n's built-in polling. Polling
was the first design, dropped once it became clear the Telegram credential
cannot drive a polling node at all: `TelegramApi` declares no `authenticate`
block, so an HTTP Request node using it sends no token, and the Telegram node
has no `getUpdates` operation. The Telegram Trigger node does accept the
credential directly, so switching to it also means the bot token lives only in
the n8n credential now, nowhere in `.env` and nowhere in the workflow JSON.

One decision worth remembering: **all column names live in one Code node
config block.** The Sheets nodes use `autoMapInputData`, so renaming a header
is a one-place edit. The exception is `matchingColumns` on the update node,
which is a static setting.

## The persistence risk

The n8n container has no volume mounted on `/home/node/.n8n`. Credentials,
workflows, and the encryption key live in the container's writable layer, so
`docker compose down` or any recreate erases them. `_backup/.n8n` in the repo
suggests this has already happened once. Unresolved as of 2026-09-03.

## Open

- Sheet headers never supplied, so the config block still holds guessed
  defaults and the workflow has not been run end to end.
- No Google Sheets credential exists in n8n yet. Only the Telegram one.
- The compose fix for persistence is written but not applied.
- Cloudflare Tunnel not yet running; `WEBHOOK_URL` not yet set in `.env`. The
  workflow cannot receive anything until both exist.

## Related

- [[research/n8n-automation|n8n Automation]] - the transferable patterns and
  gotchas, including the two this project produced
- [[projects/portfolio/overview|Portfolio Site]] - its Automations half needs
  automation work that belongs to nobody else. This is the first such piece.

## Revision History

- 2026-09-03 - Trigger changed from a one-minute poll to the Telegram Trigger
  node over a Cloudflare Tunnel. Old value: polling was chosen because n8n had
  no public URL, with the token read from `.env` since the Telegram credential
  cannot authenticate an HTTP Request node. New value: a tunnel gives n8n a
  public URL, so the Telegram Trigger node can be used instead, which does
  accept the credential directly - the token now lives only in n8n, not in
  `.env` or the workflow JSON. The offset-ordering decision (recorded the same
  day) no longer applies to this workflow, though it is kept on
  [[research/n8n-automation|n8n Automation]] as a general polling-loop lesson.
