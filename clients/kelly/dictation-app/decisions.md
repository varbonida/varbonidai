---
kind: decisions
client: kelly
project: avelisse-dictation-app
tags: [kelly, dictation-app, decisions]
created: 2026-08-04
updated: 2026-08-27
---

# Avelisse Dictation App - Decisions

Project-scoped decisions. See [[clients/kelly/dictation-app/overview|Avelisse Dictation App]]
for status. Anything here that turns out to matter beyond this project gets
promoted to a page in `decisions/`.

---

## Rebrand an existing open-source app rather than build from scratch

**Date:** 2026-08-04
**Decision:** Fork a permissively licensed on-device dictation app and rebrand it.
**Why:** Kelly's own suggestion on day one, and it is the fastest route to a
working private dictation app. On-device transcription is the hard part and
already solved upstream.

## Android and iOS base: Dictus

**Date:** 2026-08-12, agreed by Kelly the same day
**Decision:** Use Dictus for both Android and iOS.
**Alternative rejected:** AIDictation. Feature-richer, but its free tier caps at
2,000 words/month and the codebase carries cloud API and user-account
infrastructure that contradicts the privacy requirement.
**Why Dictus:** 100% offline, privacy-first system keyboard, unlimited local
usage, zero telemetry, no accounts, and it covers both iOS and Android. Known
tradeoff: it is early and in public beta.

## Desktop base: Handy

**Date:** ~2026-08-14
**Decision:** Use Handy for the desktop app.
**Supersedes:** VoiceInk, which was reported to Kelly on 2026-08-04 as the
desktop choice. The reason for the change was not recorded at the time and is
worth reconstructing before any desktop work starts.

## Android first

**Date:** 2026-08-15
**Decision:** Build and ship Android before iOS.
**Why:** Vergel works on a Windows machine and cannot build for iOS. This is a
tooling constraint, not a product preference. See
[[questions/ios-build-without-mac|the open question on iOS builds]].

## Brand name: AVELISSE

**Date:** 2026-08-21
**Decision:** Rebrand from Dictus to AVELISSE. Repo renamed `dictus-android` to
`avelisse-android`; technical identity moved from `dev.pivisolutions.dictus` to
`dev.avelissesolutions.avelisse`.
**Status:** Working name. Kelly has not formally confirmed the final brand name,
logo, or visual identity, and she originally floated names like "Dr Citizen
Dictation App".

## Visual identity: Mediterranean Coastal

**Date:** 2026-08-19
**Decision:** Sea teal, terracotta, sun amber, whitewash. Applied across all
screens and the keyboard/IME module, and ported to iOS.
**Why:** Kelly approved the initial designs drawn with this palette on
2026-08-19 ("All looks fabulous").
**Follow-through:** `DESIGN.md` is the source of truth on both platforms, and
was written from the actual implementation rather than from intent. Semantic
token names (`Primary`, `Secondary`, `Accent`, `Background`, `Surface`) replaced
screen-named ones like `HomeAccent`.
**Related:** hook line "your voice stays yours"; talking-mouth logo animation.
See [[clients/kelly/dictation-app/branding-notes|Branding Notes]].

## Preserve required upstream attribution, mark unknowns as placeholders

**Date:** 2026-08-24 to 2026-08-25
**Decision:** Keep the MIT copyright notice, the Licences screen, and the "Get
Dictus" attribution exactly as the licence requires. Keep `PRD.md` untouched as
a historical record. Mark website, Telegram, email, donate, and pricing links as
`[TBA]` or `[TBD]` rather than inventing plausible values.
**Why:** MIT permits commercial rebranding and closed-source redistribution, but
requires the notice ship with the app. Guessing at contact and pricing details
would put false claims in a shipping product.

## Do not ship the inherited "free, open-source, MIT" framing

**Date:** 2026-08-25
**Decision:** Rewrite the iOS repo docs to remove the upstream project's
self-description and its stale getdictus.com/PIVI links.
**Why:** The fork is intended for commercial distribution under Kelly's brand.
Carrying over the upstream framing would misrepresent what is being shipped.
