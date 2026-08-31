---
type: project
tags: [kelly, dictation-app, avelisse, android, ios, mobile]
created: 2026-08-04
updated: 2026-08-31
status: active
aliases: [Avelisse Dictation App, AVELISSE, Dictation App, Dictus rebrand]
---

# Avelisse Dictation App

Canonical page for Kelly's dictation app. Client: [[clients/kelly/overview|Kelly]].

A private, accurate, on-device dictation app for Kelly's own use, built by
rebranding an existing open-source project rather than writing one from scratch.
Named "Avelisse Dictation App" for now, borrowing the name of her Avelisse
property. Final brand name is still unconfirmed.

## Status

- **Current phase:** Android rebrand largely complete and in alpha; iOS design
  and technical identity rebrand both done at the source level, but nothing on
  iOS has been built, run, or verified - still unbuildable locally.
- **Android:** v1.0.0-alpha released 2026-08-25, awaiting Kelly's test.
  Repo: https://github.com/varbonida/avelisse-android (branch `develop`)
- **iOS:** repo forked, docs and colour system rewritten, technical identity
  rebrand (bundle ID, App Group) completed 2026-08-31. None of it has been
  compiled, run, or verified yet - that still needs a Mac.
  Repo: https://github.com/varbonida/avelisse-ios
- **Desktop:** research only. [Handy](https://handy.computer/) selected.
- **Blocker:** iOS cannot be built or verified from a Windows machine. See
  [[questions/ios-build-without-mac|the open question on iOS builds]].

Base projects being rebranded:

| Platform | Base | License | Repo |
|---|---|---|---|
| Desktop | Handy | - | https://github.com/cjpais/Handy |
| Android | Dictus Android | MIT | https://github.com/getdictus/dictus-android |
| iOS | Dictus iOS | MIT | https://github.com/getdictus/dictus-ios |

Upstream author: Pierre Viviere / PIVI Solutions. Mentions of "Pierre" in the
audits and changelogs refer to the upstream author, not a collaborator.

## Supporting Files

- [[clients/kelly/dictation-app/decisions|Decisions]] - what was decided and why
- [[clients/kelly/dictation-app/meeting-notes|Meeting Notes]] - call prep and outcomes
- [[clients/kelly/dictation-app/updates-android|Android updates]] - engineering changelog
- [[clients/kelly/dictation-app/updates-ios|iOS updates]] - engineering changelog
- [[clients/kelly/dictation-app/audits/android-audit|Android Audit]] (2026-08-19) - commercial distribution
- [[clients/kelly/dictation-app/audits/ios-audit|iOS Audit]] (2026-08-25) - commercial distribution
- [[clients/kelly/dictation-app/audits/localization-audit|Localization Audit]] (2026-08-21) - hardcoded text
- [[clients/kelly/dictation-app/audits/rebrand-reference-audit|Rebrand Reference Audit]] (2026-08-24) - leftover Dictus references
- [[clients/kelly/dictation-app/branding-notes|Branding Notes]] - palette and hook scratch
- [[clients/kelly/dictation-app/logo-animation-source|Logo Animation Source]] - canvas source for the animated logo

## Requirements

From Kelly, across the engagement:

- Runs on her own machine and phone, not a web app.
- Fully private and secure. On-device processing, no cloud.
- Highly accurate transcription.
- Must cover both her computer and her phone. Two separate systems is
  acceptable if one cannot cover both.
- Apple ecosystem is her primary environment.
- **Right-arrow key triggers dictation** on desktop, chosen to avoid clashing
  with Apple's own shortcuts (requested 2026-08-05).
- Should improve itself over time. Custom vocabulary and modes were raised as
  the mechanism for this.
- Rebranded as her own product: custom name, logo, icons, colours, with no
  visible Dictus references remaining.

Technical requirements:

- Android: custom package/application ID, custom IME service, own keystore,
  Google Play App Signing, signed `.aab`, Google Play developer account.
- iOS: custom bundle IDs, own App Group identifier, Apple Developer signing,
  App Store Connect, Apple Developer account.
- Compliance: Open Source Licences screen, required attribution, dependency and
  AI model licence audits, privacy policy, permission/network/telemetry audits.

## Android Workflow

Repository and branding

- [x] Fork Dictus Android, create own repo (`varbonida/avelisse-android`)
- [x] Choose brand (AVELISSE), change app name
- [x] Replace icons and assets, including the animated waveform logo
- [x] Change colours and theme to the Mediterranean Coastal palette
- [x] Replace Dictus references in UI

Application identity

- [x] Change package ID and application ID (`dev.pivisolutions.dictus` to `dev.avelissesolutions.avelisse`)
- [x] Verify package references, including JNI symbols and class renames

Keyboard / IME

- [x] Rename and rebrand the IME service and module
- [x] Re-theme the keyboard onto the Avelisse palette
- [ ] Verify the keyboard appears correctly in Android settings on device
- [ ] Test keyboard activation and switching

Signing

- [ ] Configure own signing key/keystore
- [ ] Securely store the keystore
- [ ] Document signing configuration
- [ ] Configure Google Play App Signing

Testing

- [x] First working local build produced (2026-08-25)
- [ ] Stress-test the recording flow, including rapid repeated stop taps, to
      confirm the concurrency race is closed
- [ ] Verify the transcript-logging privacy fix on device
- [ ] Visually verify the Mediterranean Coastal palette across app and keyboard
- [ ] Test microphone, transcription, permissions
- [ ] Test across multiple Android devices and versions

Audits and compliance

- [x] Dependency, AI model, and licence audit ([[clients/kelly/dictation-app/audits/android-audit|Android Audit]])
- [x] Permission, network, and telemetry audit
- [x] Licences screen present, MIT attribution preserved
- [x] Leftover-branding sweep ([[clients/kelly/dictation-app/audits/rebrand-reference-audit|Rebrand Reference Audit]])
- [x] Localization pass ([[clients/kelly/dictation-app/audits/localization-audit|Localization Audit]])
- [ ] Write and publish a privacy policy
- [ ] Document where transcription data is processed and what is collected

Google Play

- [ ] Create listing, description, screenshots, graphics
- [ ] Complete required declarations
- [ ] Build and upload a signed `.aab`
- [ ] Internal and closed testing
- [ ] Submit under Kelly's Google Play developer account

## iOS Workflow

Repository and branding

- [x] Fork Dictus iOS, create own repo (`varbonida/avelisse-ios`)
- [x] Rewrite all nine repo docs to drop the inherited "free, open-source, MIT"
      framing and stale getdictus.com links
- [x] Write `DESIGN.md` translating the Android design system into iOS terms
- [x] Implement the colour system across screens and components
- [ ] Re-theme the Live Activity widget and the cold-start swipe-back overlay,
      both deliberately left on the old palette
- [ ] Replace app name, icons, and remaining Dictus references in UI - display
      name is still "Dictus"; file/type names (`DictusApp.swift`, `DictusCore`,
      etc.) also untouched, deliberately kept out of the 2026-08-31 identity
      pass

Application identity

- [x] Change bundle IDs (`com.pivi.dictus*` to `dev.avelissesolutions.avelisse*`, 2026-08-31)
- [x] Create and configure own App Group identifier (`group.dev.avelissesolutions.avelisse`, 2026-08-31)
- [x] Change the URL scheme (`dictus://` to `avelisse://`, matching the domain
      root Android already uses) and rename the Xcode project, targets, and
      schemes (`Dictus.xcodeproj` to `Avelisse.xcodeproj`), 2026-08-31
- [ ] Verify keyboard/app communication actually works under the new identifiers
      - needs a real build, which needs a Mac

Apple Developer and testing

- [ ] Configure Apple Developer signing, certificates, provisioning, capabilities
- [ ] Verify the colour-system change actually compiles in Xcode
- [ ] Test keyboard, microphone, transcription, permissions, app/keyboard comms
- [ ] Test supported iOS versions and devices

Audits and compliance

- [x] Dependency, AI model, and licence audit ([[clients/kelly/dictation-app/audits/ios-audit|iOS Audit]])
- [x] Resolve the Parakeet/NVIDIA model licence question (confirmed CC-BY-4.0)
- [x] Fix two shipped licence bugs
- [ ] Resolve the sound-effect files' licence and provenance
- [ ] Add Open Source Licences screen with required notices

App Store

- [ ] Listing, description, screenshots, graphics
- [ ] App Store Connect configuration
- [ ] Submit under Kelly's Apple Developer account

## Desktop Workflow

Research complete, nothing built. Handy selected.

- [ ] Determine whether Handy requires rebranding
- [ ] Review Handy's licence, dependencies, and AI models
- [ ] Review privacy and data processing
- [ ] Implement the right-arrow dictation trigger Kelly asked for
- [ ] Determine distribution method
- [ ] Build and test a branded version if required

## Open Decisions

- [ ] Confirm the final brand name with Kelly
- [ ] Confirm logo and visual identity sign-off
- [ ] Fill in the `[TBA]` website, Telegram, email, and funding links once real
      ones exist
- [ ] Decide the `[PRICING TBD]` and contact placeholders in the iOS docs
- [ ] Determine transcription processing architecture
- [ ] Determine privacy and data retention policy
- [ ] Determine Android, iOS, and desktop distribution strategies

## Revision History

- 2026-08-27 - Page created during vault bootstrap. Consolidated from the
  previous vault's Dictation App hub, with all workflow checkboxes updated to
  reflect what the Android and iOS changelogs actually show as done.
- Desktop app selection changed. On 2026-08-04 VoiceInk was reported to Kelly as
  the choice; by 2026-08-14 the selection had become Handy. The reason for the
  change was not recorded at the time.
- Brand name changed. The Android repo was first created as `dictus-android`,
  renamed to `avelisse-android` on 2026-08-21.
