---
type: project
tags: [kelly, handy, privacy, bug, macos]
created: 2026-09-01
updated: 2026-09-01
status: planned
aliases: [Handy pre-roll bug, Handy buffer bug]
---

# Handy Pre-Roll Buffer Bug

Client: [[clients/kelly/overview|Kelly]]. Separate from
[[clients/kelly/dictation-app/overview|Avelisse Dictation App]] - a distinct
task on Kelly's own desktop dictation tool, Handy, not the app being built for
her. Requested 2026-09-01, scheduled for "next week," source:
[[clients/kelly/communications/index|Communications]].

## What is known

From Kelly, verbatim: "The dictation app I use on my Mac, Handy, has a
pre-roll buffer problem: it grabs audio from before I press the button and
carries fragments between sessions. I've had words from a video playing in
the background land inside my transcript."

- Handy captures audio from *before* the record button is pressed (a
  "pre-roll" buffer), and that buffer appears to leak across sessions rather
  than resetting.
- She has personally observed background audio (a video playing) ending up
  inside a dictated transcript.
- Her framing: for a normal keyboard this is an annoyance; for an app that
  will hold medical notes, it's a privacy defect, since audio she never meant
  to capture is being recorded and stored.

## What's actually being asked

**Not a fix - an explanation.** Her exact words: "I don't need you to invent
one. I need you to understand it well enough to explain to me in plain
English what it does." She's aware other people are hitting the same bug
publicly and says to use an existing fix if one is found, rather than
building one from scratch.

## Next

- Check Handy's GitHub issues/discussions for existing reports of this
  pre-roll/cross-session leak.
- Understand the actual mechanism (likely a rolling audio buffer that isn't
  cleared between recordings).
- Report back in plain English - what causes it, whether it's already fixed
  upstream, and if not, roughly how it would need to be fixed.

## Revision History

- 2026-09-01 - Page created from Kelly's communications log entry.
