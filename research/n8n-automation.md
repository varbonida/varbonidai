---
type: research
tags: [automation, n8n, gemini, llm, telegram, docker, skill, gotchas]
created: 2026-08-27
updated: 2026-09-03
status: active
aliases: [n8n, workflow automation, n8n gotchas]
---

# n8n Automation

Workflow automation with n8n, and the LLM-in-a-workflow patterns that go with it.

**Status: active, not aspirational.** Production workflows have been built
against Salesforce, PandaDoc, Gmail, Close CRM, and Hyros, plus Gemini-driven
classification and extraction. Mostly self-hosted n8n (2.18.7 at the time).

## Patterns worth reusing

**Let the model classify instead of pre-filtering.** On an email-processing
workflow with no sample data and no subject-line convention to filter on, the
approach that worked was to pull every email and let Gemini decide whether it
was the target document type, returning a boolean plus a confidence score and a
skip reason. Filtering by subject or sender first looks cheaper but fails
silently whenever the sender changes their template.

The tradeoff is real though: every email costs a model call. Where a reliable
keyword filter exists, filter first and classify second.

**Ask for a skip reason, not just a boolean.** Returning
`{is_receipt, confidence, skip_reason}` makes the failures debuggable. A bare
true/false gives nothing to look at when it is wrong.

**In a polling loop, decide which failure you prefer, then order the writes to
get it.** Advancing the update offset before the downstream writes loses a
message when a run crashes. Advancing it after replays the message and applies
the side effect twice. For anything decrementing a stock count the first is the
lesser evil, but it is a real choice and it should be a deliberate one.

**A poll returns a batch, so compute against a running tally.** Two sales of the
same product arriving in the same poll both read the same starting stock from
the sheet and both write the same result, so the second decrement vanishes. The
bug is invisible in single-message testing and appears the first busy day.

## Gotchas, all hit in practice

**`finishReason: max_tokens` from Gemini.** Two causes worth checking in order:
the output limit is genuinely too low, and the JSON schema is bloated. Schema
field descriptions are sent as input on every single call, so descriptions on
fields the extraction never uses are pure waste. Trimming descriptions down to
the fields actually being extracted cuts input tokens on every request, not just
once. 4096 output tokens was sufficient for structured extraction.

**"A 'json' property isn't an object [item 0]".** An n8n Code node must return
items where every `json` key points to an object. Returning a raw string, which
is what happens when a model's response is passed through without parsing,
triggers this. Parse the model's text back into an object before returning it.

**Gmail node attachments are not on `email.attachments`.** They arrive as
binary data. Look at the node output's `binary` tab, where they appear as
`attachment_0` and so on with filename, mime type, and size. Code that reads
`$json.attachments` will find nothing while the attachment is plainly there in
the UI.

**"Base64 decoding failed for 'filesystem-v2'".** Gemini's `inline_data.data`
wants actual base64. When n8n's binary data mode is filesystem-backed, passing
the binary reference hands Gemini the storage pointer string instead of the
file. Convert the binary to base64 explicitly before building the payload.

**Building Gemini payloads by hand is fragile.** Several rounds were lost to
`Invalid JSON payload received. Unknown name ...`, caused by expression syntax
breaking the surrounding JSON. Build the payload in a Code node where it can be
validated, rather than assembling raw JSON inside an expression field.

**An n8n credential only works on an HTTP Request node if it declares
`authenticate`.** `TelegramApi` declares `accessToken`, `baseUrl`, and a `test`
block, and nothing else. Setting an HTTP Request node to "Predefined Credential
Type -> Telegram API" therefore attaches the credential and injects nothing at
all, sending a tokenless request. The Telegram node has no `getUpdates`
operation either, so any polling workflow has to read the bot token from `$env`
or hardcode it. Generalise this: before assuming a credential can drive a
generic HTTP node, read its class and check for an `authenticate` block. `test`
is not the same thing, it only powers the "test connection" button.

**A self-hosted n8n container with no volume on `/home/node/.n8n` loses
everything on recreate**, and there is a catch-22 hiding behind it. `docker
compose restart` does not re-read `env_file`, so adding an environment variable
requires a recreate, which is exactly the operation that wipes the data. Back
the directory up first. It includes `config`, which holds the encryption key,
and restored credentials are undecryptable without it.

**Google Sheets `autoMapInputData` lets data own the column names.** The
mapping writes whichever input keys match existing sheet headers and silently
ignores the rest, so a Code node can hold every column name in one config block
instead of them being retyped across several nodes. Two caveats: an update
node's `matchingColumns` is still static, and spreading the original row into
the output keeps untouched columns from being blanked.

## Platform constraints

**PandaDoc's API is gated behind higher-tier plans.** Lower tiers only expose
Make.com and Zapier integrations, not direct API access, so n8n cannot call it
directly. The workaround is to run Make.com as a proxy that n8n calls into.

Worth generalising: before promising an n8n integration, check whether the
vendor gates API access by plan tier. "It has an API" and "this customer's plan
can use the API" are different claims, and the gap between them is discovered
late and expensively.

## Open

- Kelly has unfinished n8n workflows on a DigitalOcean droplet (referred to as
  1382, roughly $25/month) and an open question about whether to keep paying for
  it. See [[clients/kelly/n8n-digitalocean/overview|n8n on DigitalOcean]]. Their
  scope is still unknown.
- Self-hosted versus n8n Cloud has never been costed out properly.

## Related

- [[research/ai-automation-agency|AI Automation Agency]] - 10 project patterns
  that n8n is the delivery mechanism for
- [[clients/kelly/n8n-digitalocean/overview|Kelly's n8n workflows]] - the paying
  use waiting for this
- [[personal/job-search/overview|Job Search]] - a Fiverr gig selling n8n
  workflows exists
- [[research/ai-dropshipping|AI dropshipping]] - shares the tooling
- [[projects/automations/overview|Automations]] - Vergel's own n8n stack,
  where the Telegram credential and container persistence gotchas came from

## Revision History

- 2026-08-27 - Rewritten. The page previously said n8n was a topic Vergel
  "intends to learn", status `planned`. The Claude.ai export showed production
  workflows built months earlier. Status corrected to `active` and the gotchas
  extracted from those sessions. Client-specific detail deliberately left out;
  only the transferable technique is recorded here.
- 2026-09-03 - Added the Telegram credential, container persistence, and
  Google Sheets auto-mapping gotchas, plus two polling patterns. All came
  from building the Tirz sales tracker in
  [[projects/automations/overview|Automations]], and all were verified
  against the running container rather than assumed.
