---
type: question
tags: [kelly, dictation-app, ios, tooling, blocker]
created: 2026-08-27
updated: 2026-08-27
status: open
aliases: [iOS build blocker, no Mac]
---

# How will iOS builds be produced without a Mac?

## The question

The [[clients/kelly/dictation-app/overview|Avelisse Dictation App]] has to ship
on iOS. Kelly is on the Apple ecosystem and that is her primary environment.
Vergel works on Windows, so nothing iOS can be compiled, run, signed, or
verified locally.

This is not theoretical. It is already causing real consequences:

- Android was chosen first purely because of this constraint (2026-08-15).
- The iOS colour-system rewrite was written and committed but has never been
  confirmed to compile in Xcode.
- Bundle IDs and the App Group are still the upstream Dictus identifiers,
  because changing them without being able to build and test is risky.
- App Store submission requires Apple Developer signing, certificates, and
  provisioning, none of which can be done from Windows.

## Options not yet evaluated

- A cloud Mac service (MacStadium, MacinCloud, Scaleway Mac minis) rented for
  the build and verification phases.
- GitHub Actions macOS runners for CI builds and signing, with no interactive
  Xcode access.
- Kelly's own Mac, used for builds. She travels constantly with unreliable power
  and connectivity, so this is fragile.
- Buying a used Mac mini. Highest cost, removes the problem permanently.

## Why it needs answering soon

Every iOS task remaining is blocked behind it, and the iOS half is not optional
for this client.

## Resolution

Unresolved. When answered, record the decision in
[[clients/kelly/dictation-app/decisions|the project's decisions]], update the
project page, and remove this page unless the reasoning is worth keeping.
