---
type: project
tags: [kelly, dictation-app, avelisse, android, ios, mobile]
created: 2026-08-04
updated: 2026-09-02
status: active
aliases: [Avelisse Dictation App, AVELISSE, Dictation App, Dictus rebrand]
---

# Avelisse Dictation App

Canonical page for Kelly's dictation app. Client: [[clients/kelly/overview|Kelly]].

A private, accurate, on-device dictation app, built by rebranding an existing
open-source project rather than writing one from scratch. Named "Avelisse
Dictation App" for now, borrowing the name of her Avelisse property. Final
brand name is still unconfirmed.

**Scope expanded significantly on 2026-09-01.** What started as Kelly's own
private tool is now explicitly a product for chronic illness patients - see
"Chronic Patient Requirements (Android)" below. Both app stores reject a pure
rebrand with no added value, so this expansion is also the thing that makes
submission possible, not an optional extra. Full source:
[[clients/kelly/communications/2026-09-01 - Specs for the App|Communications, 2026-09-01]].

## Status

- **Current phase:** Android rebrand largely complete and in alpha; iOS design
  and technical identity rebrand both done at the source level, but nothing on
  iOS has been built, run, or verified - still unbuildable locally.
- **Android:** v1.0.0-alpha released 2026-08-25, awaiting Kelly's test.
  Repo: https://github.com/varbonida/avelisse-android (branch `develop`)
- **iOS:** repo forked, docs and colour system rewritten and now fully
  applied (old palette completely retired except the app icon, which needs a
  design decision), technical identity rebrand (bundle ID, App Group, URL
  scheme, and the full source-level rename including the display name,
  2026-08-31 to 2026-09-02) complete. None of it has been compiled, run, or
  verified yet - that still needs a Mac.
  Repo: https://github.com/varbonida/avelisse-ios
- **Desktop:** research only. [Handy](https://handy.computer/) selected.
- **Blocker:** iOS cannot be built or verified from a Windows machine. See
  [[questions/ios-build-without-mac|the open question on iOS builds]].
- **Android ship date:** Friday, 2026-10-23, to Google Play (excludes Play's
  review queue). Given by Vergel 2026-09-02 per Kelly's request for one firm
  date, not a range. See per-section estimate table below.

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

## Chronic Patient Requirements (Android)

From Kelly, 2026-09-01, verbatim source in
[[clients/kelly/communications/index|the communications log]]. This is a real
requirements document, not a summary - build against it directly.

**Why:** app store review rejects a pure rebrand with no added value. This is
also the actual product decision: the target user is a chronic illness
patient who can't reliably recall weeks of symptoms in a short appointment,
often can't type well (dry mouth, tremor, fatigue, brain fog), and needs the
app to ask nothing of them beyond talking.

**1. Medical vocabulary, loaded in advance**
- Load RxNorm (US National Library of Medicine, free, immediate download) -
  drug names, brand and generic, with the mapping between them.
- Load SNOMED CT (diagnoses, symptoms, procedures) - free in Germany and the
  US, but requires license registration first, 1-2 day turnaround. **Start
  this registration immediately, it's a scheduling dependency, not a coding
  task.**
- Surface the existing personal-dictionary feature more visibly (make it easy
  to find and add to), and document it in the app's own instructions/store
  description. Kelly explicitly asked to be told if either dictionary choice
  is a problem - that hasn't been answered yet.

**Clarified by Vergel, 2026-09-02**, after estimating the work:
- "Loaded in advance" isn't possible offline - offline speech recognition has
  no mechanism to accept a vocabulary before transcription starts (that's a
  cloud-only feature). Instead, RxNorm/SNOMED are applied as a post-recognition
  correction pass: transcribe, then repair anything close-but-wrong against the
  medical lists. Same result for Kelly, different mechanism than she described.
- The personal-dictionary feature Kelly is thinking of is the keyboard's
  autocomplete dictionary, not something wired to speech - it can't be reused.
  A real speech-correction personal dictionary (tap a wrong word, say the
  right one, it sticks) is new work, built on the same correction pass above.
- SNOMED risk: the free registration covers download and use, not necessarily
  redistribution inside an app across countries the licence doesn't name.
  Waiting on Kelly to forward the actual licence text once the account clears.
  Fallback to protect the ship date: if not resolved by **2026-09-20**, ship
  2026-10-23 with RxNorm and personal corrections only, add SNOMED later as a
  file swap.
- RxNorm may need an account rather than being an instant download as Kelly's
  brief stated - unverified as of 2026-09-02.

**2. Two single-button logs**
- **Symptom log** - one button, opens, records, auto-dates and auto-titles
  the entry, files it locally. No forms, no fields, no decisions required of
  the user mid-entry.
- **Post-visit capture** - same interaction, meant for immediately after a
  medical appointment.
- Both: browsable and searchable by date. An export button exists but export
  is never automatic - the user always chooses to send a copy.
- **Decided 2026-09-03, both revisitable:** an entry stores the transcript
  only, not the audio (keeping audio grows storage fast and makes delete
  matter more), and export writes a plain `.txt` file. PDF stays open as a
  later option if Kelly wants it.
- **Clarified 2026-09-02:** "auto-titled" means the trimmed opening line of
  what was said, not an AI-generated summary - summarization needs a
  data-centre-scale model, which would break requirement 5 (nothing leaves
  the phone).

**3. No timeouts, anywhere** - not on recording, not on the app itself.
Someone pausing mid-thought must not lose what they already said. Kelly calls
this the single biggest differentiator from a free keyboard.
- **Found while estimating, 2026-09-02:** two real bugs in this area, both
  being fixed as part of this section's work. A two-minute cap on
  transcription after recording stops (hits on longer recordings on older
  phones). And the app holds the entire recording in working memory rather
  than writing to storage as it records - past roughly half an hour of audio
  (~115MB) Android kills the app and the recording is lost, which is exactly
  the failure this requirement exists to prevent.

**4. Accessibility as a first-class requirement, not a later pass** - every
control large, usable one-handed, usable lying down. Designed in from the
start.

**5. Nothing leaves the phone, reinforced** - no cloud, no server, no account,
ever, already a requirement above. New framing: not claiming HIPAA compliance,
but built with HIPAA-level care throughout, since the data involved is exactly
what HIPAA exists to protect and users will expect that level of care whether
or not the law technically requires it here.

### What Kelly asked for, answered 2026-09-02

Her own words: two things needed *before* building continues, not after.

- [x] **A single, firm ship date.** Friday, 2026-10-23, to Google Play
      (excludes Play's review queue). Sits in the middle of the 31-39 day
      range the five sections add up to, so it isn't padded.
- [x] **Per-section time estimates**, plus which one is hardest and why:

  | Section | Days |
  |---|---|
  | 1. Medical words | 10-14 |
  | 2. Two places to talk | 6-8 |
  | 3. Speech that forgives | 3-4 |
  | 4. Bad hands and no energy | 4-5 |
  | 5. Nothing leaves the phone | 1 |
  | Integration and device testing | 4 |
  | Google Play prep and the three write-ups | 3 |

  Section 1 is hardest and carries roughly two-thirds of the risk - if the
  date slips, it will be flagged in the first three weeks, not near the end.

Full reply, verbatim:
[[clients/kelly/communications/2026-09-01 - Specs for the App|Communications, 2026-09-02]].

Now blocking on Kelly's side:

- [ ] Complete/confirm the RxNorm and SNOMED registrations - the only open
      item that can still move the ship date.
- [ ] Forward the SNOMED licence text once the account clears, so the
      redistribution question can be resolved (target 2026-09-20).

Later, not blocking now: a technical description of the app and its build
tools, a user-facing description written for a tired chronic patient deciding
whether this is worth their energy, and a step-by-step Google Play submission
plan.

**Where the work is tracked:** the spec is broken into actual tasks in Kelly's
own copy, at `00 Tasks/Avelisse Dictation Android Build.md`, tagged
`#vergel`/`#kelly` for her Tasks dashboard. That is the tracker; this page
stays the knowledge. It deliberately does not exist in this vault - see
[[concepts/client-safe-copy|Client-Safe Copy]].

### Related

- [[clients/kelly/chronic-patient-audience/overview|Chronic Patient Audience]]
  - the marketing/audience-research backlog item this directly connects to.
  The product itself is now built for this audience, not just marketed to it.
- [[clients/kelly/handy-preroll-bug/overview|Handy Pre-Roll Buffer Bug]] - a
  separate task from the same message, not part of this scope.

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
- [x] Re-theme the Live Activity widget (2026-09-02)
- [x] Re-theme the cold-start swipe-back overlay (2026-09-02) - the old
      Dictus palette is now fully gone from the app, keyboard, core, and
      widgets. One holdout: the app icon still generates in the old colours,
      which needs an actual icon design decision, not a code fix.
- [x] Replace app name and remaining Dictus references in UI, including the
      display name, mic prompt, and localisation strings (2026-09-02). Three
      things kept as-is on purpose: the MIT attribution block (renaming it
      would misattribute the original developer's work), one legacy storage
      key that lets existing installs upgrade cleanly, and a file-format
      marker inside the dictionary files that would break them if changed.

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
- [ ] Both app stores reject a pure rebrand with no added value - the
      "Chronic Patient Requirements" section above is what clears this gate.
      Submission should not proceed until real progress against that section
      exists, regardless of how ready the technical rebrand looks.

## Revision History

- 2026-09-02 - Vergel answered Kelly's two blocking asks: ship date
  (2026-10-23) and per-section estimates, sent via
  [[clients/kelly/communications/2026-09-01 - Specs for the App|Communications]].
  Estimating the work surfaced real scope clarifications, recorded above: the
  medical vocabulary can't be "loaded in advance" offline (post-recognition
  correction instead), the personal dictionary needs new work rather than
  reuse, SNOMED redistribution rights are unconfirmed, "titled" means the
  trimmed opening line rather than a summary, and two bugs (a 2-minute
  transcription cap, audio held in memory instead of written to storage) were
  found and folded into the section 3 estimate.
- 2026-09-01 - Scope expanded from "Kelly's private tool" to an explicit
  chronic-patient product, per her own detailed requirements document. Added
  the full "Chronic Patient Requirements (Android)" section and three open
  asks (ship date, per-section estimates, a green light to proceed) she wants
  answered before more building happens. Source:
  [[clients/kelly/communications/2026-09-01 - Specs for the App|Communications, 2026-09-01]].
- 2026-08-27 - Page created during vault bootstrap. Consolidated from the
  previous vault's Dictation App hub, with all workflow checkboxes updated to
  reflect what the Android and iOS changelogs actually show as done.
- Desktop app selection changed. On 2026-08-04 VoiceInk was reported to Kelly as
  the choice; by 2026-08-14 the selection had become Handy. The reason for the
  change was not recorded at the time.
- Brand name changed. The Android repo was first created as `dictus-android`,
  renamed to `avelisse-android` on 2026-08-21.
