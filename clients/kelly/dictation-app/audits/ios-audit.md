---
kind: audit
client: kelly
project: avelisse-dictation-app
platform: ios
scope: commercial distribution (license, AI models, privacy, security, branding, App Store)
tags: [kelly, dictation-app, ios, audit, licensing]
created: 2026-08-25
updated: 2026-08-31
---

# AVELISSE iOS — Commercial Distribution Audit

Repository: https://github.com/varbonida/avelisse-ios (fork of https://github.com/getdictus/dictus-ios)
Audit date: 2026-08-25

Method: read-only static audit of the local checkout (origin=varbonida/avelisse-ios, upstream=getdictus/dictus-ios, HEAD=`c49cb89`, one commit ahead of upstream — a `.gitignore`-only change). The initial pass was read-only; three follow-up fixes were applied afterward at the user's request (see "Fixed since audit" below) — flagged separately from the original findings, not silently merged in. License claims for external dependencies/models were cross-checked against their public GitHub/Hugging Face pages where possible; anything not independently confirmable is marked **NEEDS VERIFICATION**.

**Update, same day**: the Parakeet/NVIDIA license ambiguity noted below as a blocker has since been resolved, and README.md/PRD.md have been rewritten to remove the false "free, open-source, MIT" framing — see "Fixed since audit."

**Update, 2026-08-31**: the technical rebrand (Bundle ID, App Group, URL scheme, Xcode project/targets/schemes, top-level folders) has been completed — see "Fixed since audit," item 13. The Application Identity Audit, Keyboard & App Group Audit, and Recommended Pre-Release Actions sections below still describe the *pre-rebrand* state where explicitly marked; treat item 13 as the current source of truth for identifiers.

---

## Executive Summary

This fork was, as of the initial 2026-08-25 snapshot, **byte-for-byte identical in substance** to the upstream open-source "Dictus" project — no rebrand had happened yet. All internal identifiers (bundle IDs `com.pivi.dictus*`, App Group `group.solutions.pivi.dictus`, URL scheme `dictus://`, Xcode targets, folder names) and all documentation (README, PRD, PRIVACY, CLAUDE.md, etc.) were still 100% "Dictus"/"PIVI Solutions" branded, including live links to `getdictus.com`, `github.com/getdictus`, and `hello@getdictus.com`.

**As of 2026-08-31, the technical identifiers have been rebranded** (Bundle ID, App Group, URL scheme, Xcode project/targets/schemes, top-level folders — see "Fixed since audit," item 13). What's still "Dictus"-branded today is narrower: source-level symbol/file names (`DictusApp.swift`, `import DictusCore`, etc.), `CFBundleDisplayName`/on-device keyboard name, and the documentation prose/placeholders described below.

The good news: the app's core privacy claim — 100% on-device, no telemetry, no cloud — checks out under code inspection. No analytics/crash-reporting SDK exists anywhere, no transcript history is persisted, and audio is processed in memory without ever touching disk. No hardcoded secrets were found.

The real risk for commercial distribution is **not security, it's license accuracy and unfinished rebrand mechanics**:

1. ~~The Parakeet (NVIDIA) speech model's license was ambiguous~~ — **resolved, see "Fixed since audit."** The self-contradicting Hugging Face model card is a documentation error, not a real conflict: NVIDIA's own upstream card and the converted model's structured license metadata both say CC-BY-4.0.
2. ~~Every doc in the repo described this as a "free, open-source, MIT" project~~ — **README.md and PRD.md rewritten, see "Fixed since audit."** `PRIVACY.md`, `CONTRIBUTING.md`, `CONTEXT.md`, `DEVELOPMENT.md`, and `KEYBOARD_BRIEFING.md` are still untouched and still carry the old framing.
3. ~~A code path hardcoded the App Group identifier as a literal string~~ — **fixed, see below.**

None of this is unfixable. It's a punch list, not a dead end.

---

## Fixed since audit

Five changes were applied after the initial read-only pass, at the user's explicit request across follow-up turns. Each is described below with what was actually changed.

**Code (3 changes, small targeted diffs, nothing else touched):**

1. **`DictusKeyboard/TextPrediction/AOSPTrieEngine.swift:207`** — replaced the hardcoded `"group.solutions.pivi.dictus"` literal with `AppGroup.identifier`. Same value today, removes the rebrand landmine described below.
2. **`DictusApp/Views/LicensesView.swift`** — corrected FluidAudio's credited author from "NVIDIA Corporation" to "FluidInference," matching its actual Apache-2.0 code license.
3. **`DictusApp/Views/LicensesView.swift`** — added a new attribution entry for "Parakeet TDT 0.6B v3" crediting NVIDIA Corporation under CC BY 4.0, with a note that FluidInference converted it to CoreML format. This resolves the Parakeet blocker: independent verification (below) confirmed CC-BY-4.0 is the governing license, so the app now carries the attribution that license requires.

**Parakeet license verification**: checked both NVIDIA's own model card (`nvidia/parakeet-tdt-0.6b-v3`) and FluidInference's converted CoreML repo (`FluidInference/parakeet-tdt-0.6b-v3-coreml`) directly. NVIDIA's card is unambiguous — "Use of this model is governed by the CC-BY-4.0 license," explicitly cleared for commercial use. FluidInference's repo has a body-text line reading "Apache 2.0," but its structured Hugging Face metadata (the machine-readable `license` field, not just page prose) also says `cc-by-4.0` — the "Apache 2.0" sentence is a stale copy-paste from FluidAudio's project-wide README, not a deliberate relicense of the model weights. Two independent sources agree; the one contradicting data point is a documentation bug on a third party's page, not a real legal fork. CC-BY-4.0 requires attribution to NVIDIA, which the app now provides.

**Documentation (2 changes):**

4. **`README.md`** — full rewrite. Product name changed to Avelisse; "Free & open source — MIT licensed, no subscription" and all "free"/"no subscription" claims removed, replaced with an explicit `[PRICING TBD]` placeholder rather than asserting anything false. Dead upstream links (getdictus.com, old TestFlight link, `github.com/getdictus/dictus-ios`, support email) replaced with clearly marked placeholders (`[WEBSITE_URL]`, `[TESTFLIGHT_LINK]`, `[GITHUB_REPO_URL]`, `[SUPPORT_EMAIL]`, `[PRIVACY_POLICY_URL]`) per the user's explicit choice, rather than guessed real values. Acknowledgments section corrected: dropped the inaccurate "Parakeet by slingshot-ai" credit, added FluidAudio/FluidInference, NVIDIA/Parakeet (CC BY 4.0), and OpenAI/Whisper. Added a line preserving attribution that Avelisse is "built on Dictus (PIVI Solutions, MIT)." Technical/architecture references (Xcode target names `DictusApp`/`DictusKeyboard`/`DictusCore`/`DictusWidgets`) were deliberately left unchanged since those reflect the actual current codebase, not marketing copy.
5. **`PRD.md`** — targeted edits only, not a full rewrite (this is a 600+ line implementation-planning document; Sections 5–10 and 12–13, covering architecture/feature specs/design system/roadmap/risks/references, were left untouched and flagged as historical planning content not re-validated against the current build — rewriting those wasn't part of what this audit flagged, and there's no basis to invent new technical/roadmap content). Edited: title/metadata block, Executive Summary, Section 2.1 (name/origin), the competitor-comparison table, the vision statement, the target-user table, and Section 11 (renamed "Distribution & Open Source" → "Distribution & Licensing," split into a separate "Pricing & distribution model" subsection marked `[PRICING TBD]` and a "Codebase licensing" subsection correctly describing the MIT chain as distinct from the product's pricing decision), the trademark-risk line, and the footer.

**Documentation (2 more changes, same day, follow-up request):**

6. **`PRIVACY.md`** — rewritten (bilingual FR/EN, structure preserved). Product name changed to Avelisse throughout; contact email `pierre@pivi.solutions` replaced with `[SUPPORT_EMAIL]` placeholder; last-updated date bumped to 2026-08-25; added FluidAudio/Parakeet alongside WhisperKit in the "what it does" and "data stored locally" sections (previously only mentioned WhisperKit, which undersold what's actually running). The substantive privacy claims (100% offline, no analytics/tracking/third-party SDKs, Full Access used only for microphone) were **not** changed — the privacy audit above already verified these are true, so they were left as-is.
7. **`CONTRIBUTING.md`** — rewritten. Product name changed to Avelisse; technical content (project structure, App Group ID, testing commands, CI description) left unchanged since it reflects the actual current codebase. The "No CLA Required" section, which asserted contributions are "licensed under the same MIT license as the project," was flagged rather than asserted as fact — whether this fork accepts public contributions at all, and under what license, depends on the still-undecided `[PRICING TBD]` distribution model, so the clause now says that explicitly instead of stating it as settled.

**Documentation (2 more changes, same day, second follow-up request):**

8. **`CONTEXT.md`** — light touch. This is a pure technical glossary (language onboarding, STT engine, layout type definitions) with no pricing/license claims and no dead links, so there was very little to fix: title changed to Avelisse, one prose mention updated, and a note added clarifying the file paths/module names (`DictusCore`, `DictusApp`) intentionally still reflect the actual codebase rather than the marketing name.
9. **`DEVELOPMENT.md`** — targeted edits, not a full rewrite, because a large portion of this 634-line guide is literal step-by-step Xcode/App Store Connect/iOS Settings instructions that are **still technically accurate today** — the actual bundle ID (`com.pivi.dictus`), App Group (`group.solutions.pivi.dictus`), and on-device keyboard display name are still "Dictus" since the technical rebrand hasn't happened. Renaming those literal instructional values to "Avelisse" would have made the guide actively wrong for anyone following it right now. Instead: added a scoping note at the top explaining this explicitly; updated the title, intro, and footer to Avelisse; updated the forward-looking App Store Connect app-creation step (a *new* app record that doesn't exist yet, so no reason to keep it as "Dictus") with a note that a new Bundle ID is needed; updated the App Store reviewer-notes template (also forward-looking, for a submission that hasn't happened) to say Avelisse and to add FluidAudio alongside WhisperKit; flagged the "open source" App Store differentiator claim as pending the same `[PRICING TBD]` decision as the other docs; replaced the git clone example with the same `[GITHUB_REPO_URL]` placeholder used elsewhere. Left untouched: the historical "how this Xcode project was originally created" section (Name: Dictus, Bundle ID: com.pivi.dictus) and the "add the Dictus keyboard in Settings" instructions, both of which accurately describe what exists today.

**Documentation (1 more change, same day, third follow-up request):**

10. **`KEYBOARD_BRIEFING.md`** — light touch, same reasoning as `CONTEXT.md`. This is a pure technical implementation spec for Claude Code (keyboard feature checklist), no pricing/license claims, no dead links. Title and footer updated to Avelisse; the intro line now explains that the `DictusKeyboard` Xcode target name is inherited from the Dictus codebase rather than pretending it's already renamed. The literal `process DictusKeyboard` reference in the memory-profiling instructions (line ~287) was left unchanged since that's the actual current Instruments process name.

**Documentation (2 more changes, same day, fourth follow-up request):**

11. **`DEVELOPMENT_AUDIO.md`** — light touch, same reasoning as `CONTEXT.md`/`KEYBOARD_BRIEFING.md`. Pure technical architecture doc (audio pipeline, STT engine abstraction), no pricing/license claims, no dead links. Title, intro line, and one table header changed to Avelisse; all file paths and code references left untouched since they're real.
12. **`CLAUDE.md`** — different in kind from every other doc rewritten so far: this is live operational config actually loaded and acted on by Claude Code sessions working in this repo, not just descriptive documentation, so it got more scrutiny rather than a mechanical branding pass. Changes: title and project description updated to Avelisse (and now correctly mentions FluidAudio/Parakeet, which the original line omitted despite the Stack section below listing it); fixed a **pre-existing path bug** unrelated to the rebrand — the asset-generation instructions pointed to `Dictus/Assets.xcassets/AppIcon.appiconset/`, which doesn't exist, the real path is `DictusApp/Assets.xcassets/AppIcon.appiconset/` (confirmed against the actual repo structure in the Assets & Fonts Audit above); added a note that the brand kit (`assets/brand/dictus-brand-kit.html`) is the inherited Dictus visual identity, not yet an Avelisse-specific one. **Two items flagged rather than silently changed or left alone**, since guessing wrong here would misdirect a future agent session, not just read oddly: (a) the issue-tracker repo was changed from `getdictus/dictus-ios` to `varbonida/avelisse-ios` (matching this fork's actual git `origin`) with an inline note to revert if Avelisse issues are actually still tracked upstream; (b) the "Contexte utilisateur" section assuming the developer is "Pierre" (the original Dictus author) was left as-is but flagged with a note that this should be reconfirmed if someone else is now driving Avelisse's development — I have no way to know who that is.

**Technical rebrand (1 change, 2026-08-31, fifth follow-up request):**

13. **Completed the technical rebrand** flagged as unfinished throughout this audit (Executive Summary, 🟡 Check, Application Identity Audit, Keyboard & App Group Audit, Recommended Pre-Release Action #6). All internal identifiers were changed together as one coordinated pass, matching the identifier root the sibling Android app (`avelisse-android`) had already committed to:
    - **Bundle IDs**: `com.pivi.dictus` → `dev.avelissesolutions.avelisse` (app), `.keyboard`, `.widgets` (suffixes unchanged).
    - **App Group**: `group.solutions.pivi.dictus` → `group.dev.avelissesolutions.avelisse`, updated in all 3 entitlements files and the single source of truth (`AppGroup.swift`).
    - **URL scheme**: `dictus://` → `avelisse://`, including the app's `onOpenURL` scheme gate, the keyboard's cold-start deep-link trigger, and all Live Activity/widget links.
    - **Xcode project**: `Dictus.xcodeproj` → `Avelisse.xcodeproj`; all three targets and schemes renamed (`DictusApp`/`DictusKeyboard`/`DictusWidgets` → `AvelisseApp`/`AvelisseKeyboard`/`AvelisseWidgets`), hand-edited directly in `project.pbxproj` — there's no Mac/Xcode in this environment to do it through the IDE. Brace/paren balance was checked as a structural sanity check, but **the user still needs to open it in Xcode to confirm it actually parses** before trusting this is fully correct.
    - **Top-level folders**: all renamed (`DictusApp/`, `DictusKeyboard/`, `DictusWidgets/`, `DictusCore/`, plus the loose `Dictus/Sounds/` folder → `Avelisse/Sounds/`).

    Three regressions the rename would otherwise have caused silently were caught and fixed in the same pass: the two `identifier.contains("com.pivi.dictus")` keyboard-installed detection checks flagged in the Keyboard & App Group Audit below (`KeyboardSetupPage.swift`, `GlobeKeyTutorialPage.swift`), a unit test asserting the old App Group string, and six `dictus://` deep-link URLs (app, keyboard, Live Activity) that would have silently stopped opening once `Info.plist` no longer registered that scheme. `.github/workflows/ci.yml`, the language-onboarding dev tooling (`tools/onboard_language.py`, `tools/ngram_builder.py`), `.swiftlint.yml`, and the copy-pasteable setup commands in `README.md`/`DEVELOPMENT.md`/`docs/agents/language-onboarding.md` were also updated to match.

    **Deliberately not touched** (separate from this pass, not part of what was requested): source-level symbol/file names still say "Dictus" (`DictusApp.swift`, `import DictusCore`, `DictusColors.swift`, the `dictus_trie.cpp` engine, etc.), and `CFBundleDisplayName`/the on-device keyboard name is still literally "Dictus" — that's a cosmetic source rebrand, distinct from the identifier change made here. Apple Developer Portal / App Store Connect registration of the new bundle IDs and App Group (a manual account-level action, not doable from a repo checkout) is still outstanding — see Apple/App Store Audit below.

**Not fixed by this pass** — the sound-effect files' license/provenance remains the sole 🔴 blocker (see below). Every doc originally flagged in the Documentation Audit has now been addressed. The placeholders across README/PRD/PRIVACY/CONTRIBUTING/DEVELOPMENT (`[PRICING TBD]`, `[WEBSITE_URL]`, `[SUPPORT_EMAIL]`, `[TESTFLIGHT_LINK]`, `[GITHUB_REPO_URL]`, `[PRIVACY_POLICY_URL]`) still need real values, and the two flagged CLAUDE.md items above still need a human answer — the fix here was removing false/stale/wrong claims, not finalizing the decisions behind them. The technical rebrand itself is done in source (item 13 above), but Apple Developer Portal/App Store Connect registration is a separate, still-pending manual step.

---

## 🟢 Safe

- No hardcoded API keys, tokens, or secrets found anywhere in the repository (full regex sweep across all file types).
- No `.p12`/`.p8`/`.mobileprovision` files committed; no CI token exposure (`.github/workflows/ci.yml` disables code signing entirely).
- Entitlements are minimal and consistent across all 3 targets (App Group only — no Keychain sharing, no associated domains, no push).
- No telemetry, analytics, or crash-reporting SDK anywhere (Firebase/Crashlytics/Sentry/Mixpanel/Amplitude/TelemetryDeck/PostHog/AppCenter — zero hits).
- No transcript/dictation history is ever persisted; recorded audio lives only as an in-memory `[Float]` buffer and is never written to disk.
- Keyboard extension makes zero network calls; all model-download network activity is confined to the main app.
- No Keychain usage anywhere (nothing sensitive stored there to begin with).
- WhisperKit (MIT/Argmax), DeviceKit (MIT/Dennis Weissmann), and giellakbd-ios (dual Apache-2.0/MIT/UiT Arctic University of Norway) are all correctly licensed for commercial use, correctly attributed in `LicensesView.swift`, and safely vendored/referenced.
- SymSpell (previously vendored, disputed license lineage) has been fully removed from the codebase — confirmed zero remaining files.
- No CocoaPods, no XCFrameworks/static or dynamic binary blobs, no custom fonts bundled (system fonts only) — nothing hiding in a binary dependency.
- App icon and brand SVGs (`assets/brand/`) appear to be original artwork matching the documented brand kit.
- `RequestsOpenAccess=true` is correctly set on the keyboard extension (required for microphone access); minimum iOS version (17.0) is consistent across all targets.

## 🟡 Check

- **`CLAUDE.md` has two flagged operational items needing a human decision**: whether the issue tracker should point at `varbonida/avelisse-ios` (changed) or stay on upstream `getdictus/dictus-ios`, and whether the "Contexte utilisateur" section's assumption that the developer is "Pierre" (the original Dictus author) still holds for Avelisse. Both were flagged inline in the file rather than guessed.
- **README.md, PRD.md, PRIVACY.md, CONTRIBUTING.md, and DEVELOPMENT.md now contain explicit placeholders** (`[PRICING TBD]`, `[WEBSITE_URL]`, `[SUPPORT_EMAIL]`, `[TESTFLIGHT_LINK]`, `[GITHUB_REPO_URL]`, `[PRIVACY_POLICY_URL]`, and a new Bundle ID placeholder in DEVELOPMENT.md) instead of false claims — correct as an interim state, but these need real values decided and filled in before public launch.
- **`DEVELOPMENT.md`'s historical "how this Xcode project was originally created" and "add the keyboard in Settings" sections still describe `com.pivi.dictus`/"Dictus"** — these were deliberately left untouched during the earlier doc pass as *accurate to the app's then-current state*, but that's no longer true now that the technical rebrand (item 13) has actually happened. They now need a pass to either update them to the new identifiers or explicitly mark them as describing the pre-rebrand history — currently stale, not yet fixed.
- **FluidAudio's own LICENSE file is an unfilled Apache-2.0 template** (`Copyright [yyyy] [name of copyright owner]`), with no NOTICE file in the upstream repo — the copyright holder is genuinely undocumented upstream. Get this clarified directly with FluidInference before finalizing your own third-party-license document.
- **Dictionary/n-gram resource files** (`DictusKeyboard/Resources/*_frequency.json`, `*_ngrams.dict`, `*_spellcheck.dict`) are built from Lexique 3.83 (French academic lexicon) and Google 1T/COCA (English) via in-repo tools (`tools/dict_builder.py`, `tools/ngram_builder.py`). Redistribution terms of these *source corpora* for the derived, filtered word lists were not independently re-verified.
- **HeliBoard (GPL-3.0)** is named in `.planning/phases/24.1-*` docs as a design/architecture reference for the AOSP-style trie engine (`DictusKeyboard/Vendored/AOSPTrie/`). Project docs describe this as an explicit clean-room reimplementation, not copied code — worth one more manual pass given HeliBoard is copyleft.
- No `Package.resolved` is committed — WhisperKit, FluidAudio, and DeviceKit are all pinned only to minimum-version floors in `project.pbxproj`, not exact commits. Fine for licensing, but a reproducibility/supply-chain risk for consistent commercial builds.
- OpenAI (original Whisper model author) is not credited anywhere in-app or in docs — only Argmax/WhisperKit (the CoreML conversion) is. Not legally required under MIT, but worth adding for accuracy.
- Hugging Face's Terms of Service for unauthenticated, in-app `resolve/main` model downloads at commercial-app scale were not verified.
- **29 sound-effect `.wav` files** in `Dictus/Sounds/` have no license, attribution, or sourcing documentation anywhere in the repo (checked `DEVELOPMENT.md`, `DEVELOPMENT_AUDIO.md`, `README.md` — nothing).
- No German UI localization exists despite German being marketed as a supported language (`CLAUDE.md`, `README.md`) — German is supported for STT transcription and keyboard layout only, not the interface itself. `DictusApp/Localizable.xcstrings` and `DictusKeyboard/Localizable.xcstrings` only localize to French; 17 keys are marked `"extractionState": "stale"` (translation may be outdated vs. current source string).
- User-facing "Dictus" branding is baked directly into translated strings (not just source identifiers) — e.g. "Dictus is set up and ready to use", "switch to the Dictus keyboard", "Enable Full Access in Settings > Keyboards > Dictus" — roughly 15+ occurrences across both English source and French translations in the `.xcstrings` catalogs.
- `DictationCoordinator.swift:498` logs the actual transcribed text via `os_log(..., privacy: .private)`. The `.private` tag redacts it to `<private>` in Console/sysdiagnose on non-debug-provisioned devices, but this is the one code path where dictated speech content touches a logging call in Release builds — verify this meets your privacy bar (vs. the rest of the logging system, which is metadata-only by design).
- `DebugLogView.swift` ships in Release builds and is reachable by any end user via Settings — not a secrets leak (the underlying log contains no dictated text), but confirm this is intentional support tooling, not leftover dev scaffolding.
- `PrivacyInfo.xcprivacy` (both app and keyboard) declares no `NSPrivacyCollectedDataTypes` despite the app processing microphone audio — likely fine since audio never leaves the device or gets linked to identity, but this should be a deliberate compliance decision, not a silent omission.
- Missing `ITSAppUsesNonExemptEncryption` key in `DictusApp/Info.plist` — not fatal, but App Store Connect will prompt the export-compliance question on every submission without it.
- Legacy `UIRequiredDeviceCapabilities: armv7` key in Info.plist — harmless dead weight on an iOS 17+/arm64-only app, worth cleaning up.
- Version-string duplication: `Info.plist` hardcodes `CFBundleShortVersionString=1.7.2` / `CFBundleVersion=22`, while `project.pbxproj`'s `MARKETING_VERSION=1.4` / `CURRENT_PROJECT_VERSION=6` are stale and unused (since `GENERATE_INFOPLIST_FILE=NO`) — two disconnected sources of truth for version bumps.
- `DictusApp/Views/SettingsView.swift:147` — GitHub link button points to `https://github.com/Pivii/dictus`, which is already a stale/incorrect URL (wrong org name, not even matching the real upstream `getdictus/dictus-ios`) — a pre-existing bug independent of the rebrand.
- Bundle IDs, App Group ID, and URL scheme are all still "Dictus"/"pivi" branded and will require a coordinated technical rebrand (see App Store & Keyboard sections below) — changing these breaks continuity for any existing installs.

## 🔴 Blockers

- **Sound effect files have zero documented license or provenance** (`Dictus/Sounds/*.wav`, 29 files) — cannot confirm commercial-use safety until sourced; if these came from a paid or restrictively-licensed sound pack, they cannot ship in a commercial product without a license. Investigated further (commit history, PR text, `.planning` docs, filename search) with no result — provenance is untraceable from the repo itself; needs either tracking down the original human source or replacing the files outright.

Resolved since the initial audit — no longer blockers, see "Fixed since audit" above: the Parakeet/NVIDIA model license ambiguity, the FluidAudio/NVIDIA misattribution in `LicensesView.swift`, the hardcoded App Group identifier in `AOSPTrieEngine.swift`, the false "free, open-source, MIT" framing across every doc in the repo (`README.md`/`PRD.md`/`PRIVACY.md`/`CONTRIBUTING.md`/`CONTEXT.md`/`DEVELOPMENT.md`/`KEYBOARD_BRIEFING.md`/`DEVELOPMENT_AUDIO.md`/`CLAUDE.md`), and the technical rebrand of Bundle ID/App Group/URL scheme/Xcode project/top-level folders (2026-08-31, item 13).

Downgraded to 🟡 Check: the `[PRICING TBD]`/placeholder values spread across README/PRD/PRIVACY/CONTRIBUTING/DEVELOPMENT still need real answers, and `CLAUDE.md` has two flagged operational items (issue-tracker repo, developer persona) that need a human decision — see 🟡 Check.

---

## License Audit

**Root LICENSE**: MIT, `Copyright (c) 2026 PIVI Solutions`. Unchanged since the repo's first commit; the fork has made no LICENSE or copyright edits. MIT permits commercial use, modification, sublicensing, and resale — the only hard requirement is that the original copyright notice and license text remain included somewhere in the distribution (they currently do, both in the root `LICENSE` file and in the in-app `LicensesView.swift`). **The MIT attribution chain is currently fully intact** — nothing has been stripped. A commercial Avelisse release may add its own copyright line for its own modifications alongside the original PIVI Solutions notice; it does not need to (and per MIT, should not) remove it.

| Dependency | Version/Commit | Source | License (verified) | Commercial Safe? | Attribution Required? | Redistribution Notes | Risk |
|---|---|---|---|---|---|---|---|
| WhisperKit | SPM, floor 0.16.0 (unpinned) | github.com/argmaxinc/WhisperKit | MIT, Argmax, Inc. | Yes | Yes | Standard MIT notice | 🟢 |
| FluidAudio | SPM, floor 0.12.3 (unpinned) | github.com/FluidInference/FluidAudio | Apache 2.0 (code) — LICENSE file is an unfilled template, no true copyright line, no NOTICE file upstream | Yes (code) | Yes (Apache §4) | Parakeet *weights* are separately CC-BY-4.0/NVIDIA — now attributed, see "Fixed since audit" | 🟡 |
| DeviceKit | SPM, floor 5.8.0 (unpinned) | github.com/devicekit/DeviceKit | MIT, Dennis Weissmann | Yes | Yes | Standard MIT notice | 🟢 |
| giellakbd-ios | Vendored into `DictusKeyboard/Vendored/` | github.com/divvun/giellakbd-ios | Dual Apache-2.0 OR MIT, UiT Arctic University of Norway | Yes | Yes | App uses MIT text, correctly attributed in-app | 🟢 |
| Dictus (upstream project itself) | N/A | github.com/getdictus/dictus-ios | MIT, PIVI Solutions | Yes (MIT permits resale/relicense) | Yes — must preserve notice | See attribution-chain note above | 🟢 |

No CocoaPods, no `Package.resolved` (deps pinned only to floor versions), no `.xcframework`/`.framework`/`.a`/`.dylib` binaries checked in, no custom fonts. No GPL/LGPL/AGPL code is incorporated; the one copyleft project touched anywhere (HeliBoard, GPL-3.0) was used only as a design reference per project docs, not as a code source — see 🟡 Check above for the recommended second look.

**Vendored source**: `DictusKeyboard/Vendored/{Views,Models,Controllers,GiellaUtils.swift}` — explicitly documented as stripped-down giellakbd-ios code (Sentry/DivvunSpell/RxSwift/SQLite dependencies removed), MIT-compatible. `DictusKeyboard/Vendored/AOSPTrie/` — headers marked "AOSP-inspired trie engine... Apache 2.0," documented in `.planning/phases/24.1-*` as a clean-room reimplementation, not a port.

## Dependency Audit

See table above — this project has an unusually small, clean dependency surface: 3 SPM packages, 1 vendored source tree, no CocoaPods, no binary frameworks. The main hygiene gap is the absence of a committed `Package.resolved`, meaning builds aren't reproducible to an exact dependency commit — a build/ops concern more than a license concern.

## AI / Model Audit

Both STT engines download model weights at runtime from Hugging Face; **nothing is bundled in the app binary** (confirmed — no `.mlmodelc`/`.mlmodel`/weight files anywhere in the repo). This is a materially favorable legal posture: the app links to the rightsholders' own hosting rather than redistributing weights itself.

| Model | Provider | Source | License | Commercial OK? | Attribution Required? | Currently Attributed Correctly? |
|---|---|---|---|---|---|---|
| WhisperKit SDK | Argmax, Inc. | github.com/argmaxinc/WhisperKit | MIT | Yes | Yes (notice) | Yes |
| Whisper CoreML weights (tiny/base/small/medium/large-v3-turbo, multilingual) | Argmax, Inc. (HF hub), derived from OpenAI Whisper | huggingface.co/argmaxinc/whisperkit-coreml | MIT | Yes | Not legally required, good practice | Partial — Argmax credited, OpenAI (original model author) is not |
| FluidAudio SDK | FluidInference | github.com/FluidInference/FluidAudio | Apache-2.0 | Yes | Yes | **Fixed** — `LicensesView.swift` now credits FluidInference, not NVIDIA |
| Parakeet CoreML weights (`parakeet-tdt-0.6b-v3`) | NVIDIA (original), converted by FluidInference | huggingface.co/FluidInference/parakeet-tdt-0.6b-v3-coreml (base: huggingface.co/nvidia/parakeet-tdt-0.6b-v3) | **CC-BY-4.0** (confirmed on both NVIDIA's card and the converted repo's structured metadata; the converted repo's body-text "Apache 2.0" line is a stale copy-paste error, not a real conflict) | Yes | Yes — NVIDIA credit required | **Fixed** — new entry added to `LicensesView.swift` |

There are no separate FR/EN/DE Whisper models — all sizes are the standard multilingual OpenAI Whisper conversions; language is a decode-time parameter, not a model choice.

**Must be verified before commercial distribution**: Hugging Face ToS for unauthenticated commercial-scale in-app downloads; whether any additional OpenAI-specific terms apply beyond the MIT relicense on the Argmax-converted weights (not found, but not independently confirmed on the HF card itself). The Parakeet license question itself is resolved — see "Fixed since audit."

**README.md's Acknowledgments section is inaccurate**: it credits "Parakeet by slingshot-ai" linking to `github.com/slingshot-ai/captions-ios` — this is not the actual source; the real dependency is FluidInference/FluidAudio, and the underlying model is NVIDIA's. This should be corrected regardless of the license question, since it currently misleads readers about where the code and model actually come from.

## Privacy & Telemetry Audit

**Verdict: the "100% on-device / no telemetry / no cloud" claim is TRUE**, verified by code inspection, not just marketing copy:

- Zero analytics/crash-reporting/telemetry SDKs anywhere in the repo.
- No CloudKit, no iCloud sync, no `NSUbiquitousKeyValueStore`.
- No Keychain usage at all.
- The keyboard extension itself makes zero network calls.
- No transcript-history feature exists anywhere in the codebase — dictated text is inserted directly into the host app's text field and never stored by Dictus/Avelisse.
- Recorded audio is held only as an in-memory `[Float]` array and passed straight to the transcription engine — no `.wav`/`.caf`/`.m4a` file is ever written, so there is nothing to "clean up" after transcription.
- The App Group container stores only preferences, model-download bookkeeping, and structured debug-log metadata — never transcript text or raw audio (enforced by `LogEvent.swift`'s typed schema, which the code comments explicitly note "must not contain transcription text or keystrokes").
- The one raw-text logging exception (`DictationCoordinator.swift:498`, `os_log` with `.private` tag) is flagged in 🟡 Check above.
- "Shake to send feedback" (mentioned in README) is Apple's own OS-level TestFlight feature — confirmed no custom feedback-upload code exists in the app.

`PRIVACY.md`'s claims are consistent with what the code actually does — no contradictions found between the documented policy and the implementation, beyond the one logging exception noted above.

## Network Audit

| URL/Host | Purpose | User data included? | Required? | Third-party? | Concern |
|---|---|---|---|---|---|
| huggingface.co/api/models/.../tree/main, .../resolve/main/... | Download WhisperKit/Parakeet model weights (main app only) | No | Yes (for STT) | Yes (Hugging Face) | 🟢 |
| github.com, getdictus.com, testflight.apple.com | User-initiated link-outs (About, Licenses, website, TestFlight) | No | No | Yes/N/A | 🟢 (will need URL updates for rebrand, see Identity section) |

No telemetry, analytics, or crash-reporting endpoint exists anywhere. All live network traffic is confined to the main app process for on-demand, disclosed speech-model downloads.

## Security Audit

- No hardcoded secrets, API keys, or tokens found in a full repo-wide sweep. No signing material (.p12/.p8/.mobileprovision) committed.
- Entitlements are minimal and identical in shape across all 3 targets — App Group only, no Keychain sharing, no associated domains, no push.
- `project.pbxproj` commits a real Apple Development Team ID (`9B8B36C2FA`) — not a secret, fine to have committed, but worth knowing it's there if the repo becomes public.
- `DictusApp/Views/TestDictationView.swift` and `DictusApp/Views/DebugLogView.swift` are **not** gated behind `#if DEBUG` and are reachable in Release/App Store builds via normal UI navigation. Neither exposes secrets or dictated content (the underlying log is metadata-only), but confirm this is the intended shipped UX rather than leftover dev tooling.
- No explicit file-protection attributes (`NSFileProtectionKey`) are set on the App Group log file — informational, low severity, since no audio/transcript content is ever written to disk in the first place.
- CI (`.github/workflows/ci.yml`) uses only standard, pinned actions; code signing is explicitly disabled for CI builds; no embedded tokens.

## Application Identity Audit

**Identifiers as of the 2026-08-25 snapshot** (all still "Dictus"/"PIVI" branded at that point):

| Item                       | Value at initial audit (2026-08-25)                                                 |
| -------------------------- | ------------------------------------------------------------------------------------ |
| Bundle ID — DictusApp      | `com.pivi.dictus`                                                                    |
| Bundle ID — DictusKeyboard | `com.pivi.dictus.keyboard`                                                           |
| Bundle ID — DictusWidgets  | `com.pivi.dictus.widgets`                                                            |
| App Group                  | `group.solutions.pivi.dictus`                                                        |
| URL scheme                 | `dictus://`                                                                          |
| Xcode project / schemes    | `Dictus.xcodeproj`; `DictusApp`/`DictusKeyboard`/`DictusWidgets` schemes and targets |
| Top-level folders          | `DictusApp/`, `DictusKeyboard/`, `DictusCore/`, `DictusWidgets/`                     |

**Current identifiers, since 2026-08-31** (see "Fixed since audit," item 13):

| Item                          | Current value                                                                                     |
| ------------------------------ | --------------------------------------------------------------------------------------------------- |
| Bundle ID — AvelisseApp        | `dev.avelissesolutions.avelisse`                                                                    |
| Bundle ID — AvelisseKeyboard   | `dev.avelissesolutions.avelisse.keyboard`                                                           |
| Bundle ID — AvelisseWidgets    | `dev.avelissesolutions.avelisse.widgets`                                                            |
| App Group                      | `group.dev.avelissesolutions.avelisse`                                                              |
| URL scheme                     | `avelisse://`                                                                                       |
| Xcode project / schemes        | `Avelisse.xcodeproj`; `AvelisseApp`/`AvelisseKeyboard`/`AvelisseWidgets` schemes and targets        |
| Top-level folders              | `AvelisseApp/`, `AvelisseKeyboard/`, `AvelisseCore/`, `AvelisseWidgets/`                             |

Not yet done: Apple Developer Portal/App Store Connect registration of these new identifiers (new app record, new provisioning) — a manual account-level step, separate from the source-level rename above.

**1. Safe to replace** (cosmetic branding, no legal weight): UI-visible strings across `Onboarding/`, `SettingsView.swift`, `DictusLiveActivity.swift`; all "Dictus"-branded keys in both `Localizable.xcstrings` catalogs; Swift symbol names (`DictusColors`, `DictusLogo`, `DictusTypography`, `.dictusAccent` etc. — mechanical rename); brand SVG/HTML asset files; product-name mentions across README/PRD/CLAUDE.md/etc.

**2. Safe to remove** (dead/community links once rebranded): README's Telegram, website, donate, GitHub badge/stargazer links, sibling-project links (dictus-android/desktop), support email, old TestFlight link; `SettingsView.swift:147`'s already-stale `github.com/Pivii/dictus` link; historical issue-number links in `docs/WHISPERKIT_TUNING.md`.

**3. Must preserve for legal attribution** (MIT requirement, distinct from marketing branding): the `LICENSE` file's "Copyright (c) 2026 PIVI Solutions" notice; the "Dictus"/"PIVI Solutions"/`github.com/getdictus/dictus-ios` block inside `LicensesView.swift`. These may sit alongside new Avelisse copyright/branding but should not be deleted.

**4. Third-party references** (never touch — not Dictus branding, separate attribution): DeviceKit, FluidAudio, giellakbd-ios, WhisperKit entries in `LicensesView.swift`; SPM package names in `project.pbxproj`.

**5. Historical/documentation references** (low priority, not shipped): the entire `.planning/` tree (milestones, phases, retrospectives) — hundreds of incidental "Dictus"/"pivi" mentions, purely internal project history.

**6. Needs manual review — done in source, 2026-08-31** (technical consequences beyond branding): bundle IDs, App Group identifier, `dictus://` URL scheme, and the Xcode project/scheme/target names have all been changed in source — see "Fixed since audit," item 13. What's still outstanding is the account-level side: registering the new bundle IDs and App Group in the Apple Developer Portal, new App Store Connect app records (bundle ID cannot be changed on an existing app after first submission), and regenerated provisioning profiles — none of that is doable from a repo checkout.

## Apple / App Store Audit

- `NSMicrophoneUsageDescription` is present and filled in with real text on the main app; absent on the keyboard extension, which is fine since microphone capture actually happens in the containing app process, not the extension.
- `RequestsOpenAccess=true` is correctly set on the keyboard extension.
- `ITSAppUsesNonExemptEncryption` key is absent — not fatal, but App Store Connect will ask the export-compliance question manually on every submission until it's added.
- Legacy `UIRequiredDeviceCapabilities: armv7` key present — harmless but should be cleaned up (32-bit ABI flag on an arm64-only app).
- `LSApplicationQueriesSchemes` (WhatsApp, SMS, Telegram, Messenger, Signal, Slack, Discord, Teams, Instagram, Notes) is duplicated verbatim across both the app's and keyboard's Info.plist — a sync risk if one is updated without the other.
- Minimum iOS version (17.0) is consistent across all 3 targets.
- Version strings are duplicated across two disconnected sources of truth (Info.plist literals vs. unused `MARKETING_VERSION`/`CURRENT_PROJECT_VERSION` build settings) — confusing for future version bumps, not a functional bug today.
- `PrivacyInfo.xcprivacy` (app + keyboard) declares `NSPrivacyTracking: false` and only `UserDefaults`/`FileTimestamp`/`ActiveKeyboards` required-reason API categories — consistent with actual usage, but declares no `NSPrivacyCollectedDataTypes` despite the app processing microphone audio; this should be a deliberate compliance decision.

**Manual Apple Developer Portal / App Store Connect actions required for a rebrand**: register new bundle IDs for all 3 targets; register a new App Group ID and re-enable the App Groups capability on the new bundle IDs; regenerate provisioning profiles; create a new App Store Connect app record (bundle ID cannot be changed on an existing app after first submission); answer the export-compliance question (or add the Info.plist key to avoid re-answering each time); update category/screenshots/metadata in ASC; decide whether to also change the `dictus://` URL scheme.

## Keyboard & App Group Audit

The keyboard extension cannot run WhisperKit directly (its ~50MB memory ceiling), so it delegates recording/transcription to the containing app via `DarwinNotificationCenter` (start/stop/cancel pings) with payloads exchanged through the shared App Group `UserDefaults`. If the app doesn't acknowledge within ~500ms (e.g., not running), the keyboard falls back to force-launching the app via the `dictus://dictate?source=keyboard` URL scheme. This is a reasonable but inherently fragile architecture — it depends on the app being backgrounded rather than fully suspended/killed for the fast path, and on the URL scheme staying correctly wired for the cold-start fallback.

**Rebrand landmine — fixed**: `AvelisseKeyboard/TextPrediction/AOSPTrieEngine.swift:207` (then `DictusKeyboard/...`) previously hardcoded `UserDefaults(suiteName: "group.solutions.pivi.dictus")` directly, bypassing the shared `AppGroup.identifier` constant used everywhere else in the codebase. This was the single call site most likely to be missed during a rebrand (silent failure — a disconnected, orphaned App Group container — rather than a crash). Now fixed to reference `AppGroup.identifier`, see "Fixed since audit." Two other locations (`KeyboardSetupPage.swift`, `GlobeKeyTutorialPage.swift`) checked for `identifier.contains("com.pivi.dictus")` for keyboard-installed detection — flagged here as lower-risk informational checks, and now fixed in the same technical-rebrand pass (item 13) to check for `dev.avelissesolutions.avelisse` instead. Without that fix they'd have silently and permanently reported "keyboard not installed" once the bundle ID actually changed.

## Localization Audit

- Full UI localization exists only for English (source) and French. `Dictus.xcodeproj`'s `knownRegions` is `en, fr, Base` — no German UI strings exist, despite German being marketed as a supported language; German support today is limited to speech transcription and keyboard layout only.
- 17 keys in `DictusApp/Localizable.xcstrings` are marked `"extractionState": "stale"` (source string changed since the French translation was last updated).
- Roughly 15+ occurrences of hardcoded "Dictus" branding inside the actual translated string catalogs (both English source and French translations), not just source-code identifiers — these require rebrand edits in both languages, not just a global find-and-replace on Swift source.
- Keyboard layout mapping is correct and intentional: French → AZERTY, English/German → QWERTY (QWERTZ for German explicitly deferred per a documented follow-up issue).

## Logging Audit

- The primary logging system (`PersistentLog.swift`) is metadata-only by design — durations, memory, model names, status transitions — with an explicit code-level invariant that log events must never contain transcription text or keystrokes. This was verified true in practice.
- One exception: `DictationCoordinator.swift:498` passes the actual transcribed text into `os_log` with a `.private` privacy tag, which OS-level redaction hides on non-debug-provisioned devices, but this is not gated by `#if DEBUG` and does run in Release builds.
- A separate, unrelated debug-only logger (`AutocorrectDebugLog.swift`) that does log raw typed words is fully wrapped in `#if DEBUG` and physically absent from Release/App Store/TestFlight binaries, with explicit opt-in required even in Debug.
- `DebugLogView.swift`/`DiagnosticDetailView.swift` expose the persistent log to end users via Settings in Release builds — safe given the log's metadata-only content, but worth confirming this is intended.

## Assets & Fonts Audit

- App icon and brand SVG assets (`assets/brand/`) match the documented brand-kit spec in `CLAUDE.md` and appear to be original artwork.
- No custom fonts are bundled or referenced anywhere (no `UIAppFonts` key, no `.ttf`/`.otf` files, no `Font.custom` calls) — system fonts only, no font-licensing exposure.
- **29 `.wav` sound-effect files** (`Dictus/Sounds/`) have no license, attribution, or sourcing documentation anywhere in the repo — flagged as a blocker above pending verification of their origin.

## Documentation Audit

At the time of the initial pass, every top-level doc — `README.md`, `PRD.md`, `CONTEXT.md`, `DEVELOPMENT.md`, `DEVELOPMENT_AUDIO.md`, `PRIVACY.md`, `CONTRIBUTING.md`, `KEYBOARD_BRIEFING.md`, `CLAUDE.md` — was verbatim-inherited from upstream Dictus with zero fork-specific edits (zero mentions of "Avelisse" anywhere in the repository).

**Since then, six docs have been rewritten** (see "Fixed since audit"): `README.md`, `PRD.md`, `PRIVACY.md`, `CONTRIBUTING.md`, `CONTEXT.md`, and `DEVELOPMENT.md` all now use "Avelisse" as the product name in narrative/forward-looking text, the false "free, open-source, MIT" framing is gone (replaced with an explicit `[PRICING TBD]` placeholder where applicable), dead upstream links/contact email are replaced with placeholders, and the inaccurate Parakeet/slingshot-ai acknowledgment in README is corrected. `PRD.md`'s deep technical content (Sections 5–10 and 12–13) and `DEVELOPMENT.md`'s literal, still-accurate Xcode/Settings instructions (bundle ID, App Group, on-device keyboard name) were both deliberately left untouched, for the same reason in each case: they describe the actual current codebase/environment state, not marketing copy, and rewriting them wasn't part of the license/branding remediation this audit flagged. `PRIVACY.md`'s substantive privacy claims were also left unchanged since the Privacy & Telemetry Audit above already verified them true — only branding/contact info changed there.

**All docs originally flagged in this audit have now been rewritten** — see "Fixed since audit" for the full list and what was (and deliberately wasn't) changed in each. `CLAUDE.md`, being live operational config rather than descriptive documentation, got two items flagged inline for human confirmation instead of a guessed change — see 🟡 Check.

---

## Files to Preserve

- `LICENSE` (root) — MIT text, PIVI Solutions copyright notice.
- `DictusApp/Views/LicensesView.swift` — the "Dictus"/"PIVI Solutions" attribution block specifically.
- Third-party attribution entries for DeviceKit, WhisperKit, giellakbd-ios, FluidAudio, and (now) Parakeet/NVIDIA within the same file.

## Files/References Safe to Replace or Remove

See the six-category breakdown in the **Application Identity Audit** section above — categories 1 and 2 specifically ("Safe to replace" and "Safe to remove").

---

## Commercial Release Checklist

- [x] License verified — MIT chain intact; Apache-2.0 (FluidAudio) confirmed for code
- [x] Third-party licenses verified — WhisperKit/DeviceKit/giellakbd-ios confirmed; FluidAudio LICENSE template gap noted
- [x] Attribution preserved — FluidAudio/NVIDIA entry corrected, Parakeet/NVIDIA entry added
- [x] AI/model licenses verified — Parakeet/NVIDIA resolved as CC-BY-4.0, attribution added
- [ ] Fonts/assets licensed — fonts clear (none used); **sound effects unverified, still blocking**
- [ ] No unwanted telemetry — confirmed clean
- [ ] No transcript/audio leakage — confirmed clean, one `.private`-tagged text log to review
- [ ] Network traffic audited — confirmed clean, all traffic is model downloads + user-initiated links
- [ ] Secrets checked — none found
- [x] Bundle ID reviewed — rebranded in source (`dev.avelissesolutions.avelisse` + suffixes, 2026-08-31); still needs new ASC app record + Developer Portal registration
- [x] App Group reviewed — rebranded in source (`group.dev.avelissesolutions.avelisse`), hardcoded bypass in `AOSPTrieEngine.swift` fixed
- [x] Keyboard extension reviewed — architecture sound; App Group/URL scheme/bundle ID now consistent post-rebrand, including the two keyboard-detection checks
- [ ] Entitlements reviewed — minimal, no issues
- [ ] Privacy manifest reviewed — present, minor gap on collected-data-types declaration
- [ ] Permission descriptions reviewed — present and filled in
- [ ] Localization reviewed — no German UI strings; branding baked into FR/EN catalogs needs rebrand edits
- [ ] Branding reviewed — extensive, unfinished rebrand across code, assets, and docs
- [x] README/documentation reviewed — all repo docs rewritten (README.md, PRD.md, PRIVACY.md, CONTRIBUTING.md, CONTEXT.md, DEVELOPMENT.md, KEYBOARD_BRIEFING.md, DEVELOPMENT_AUDIO.md, CLAUDE.md); false framing removed, placeholders in place, two CLAUDE.md operational items flagged for human confirmation
- [x] Privacy policy reviewed — accurate to code behavior (verified in Privacy & Telemetry Audit); rewritten for branding/contact info, substantive claims unchanged since already correct
- [ ] App Store requirements reviewed — minor Info.plist cleanup items, no blockers
- [ ] Release build reviewed — DebugLogView/TestDictationView ship in Release by design, confirm intentional

## Recommended Pre-Release Actions

1. ~~Get the Parakeet/NVIDIA model license conflict resolved~~ — done, see "Fixed since audit."
2. ~~Fix `LicensesView.swift`'s FluidAudio/NVIDIA misattribution and add a correct NVIDIA/Parakeet entry~~ — done.
3. Source or replace the 29 sound-effect files with something license-documented.
4. ~~Rewrite every repo doc for the actual commercial Avelisse product~~ — done for all nine (README, PRD, PRIVACY, CONTRIBUTING, CONTEXT, DEVELOPMENT, KEYBOARD_BRIEFING, DEVELOPMENT_AUDIO, CLAUDE.md). ~~Complete the actual technical rebrand (new Bundle ID/App Group)~~ — done in source 2026-08-31, item 13. Still open: decide and fill in the real values behind the `[PRICING TBD]`/`[WEBSITE_URL]`/`[SUPPORT_EMAIL]`/`[TESTFLIGHT_LINK]`/`[GITHUB_REPO_URL]`/`[PRIVACY_POLICY_URL]` placeholders; confirm the two flagged `CLAUDE.md` operational items (issue-tracker repo, developer persona); update `DEVELOPMENT.md`'s now-stale historical Xcode-creation section (see 🟡 Check).
5. ~~Fix the hardcoded App Group string in `AOSPTrieEngine.swift:207`~~ — done.
6. ~~Plan the bundle ID / App Group / URL scheme rebrand as one coordinated change~~ — done in source, 2026-08-31 (see "Fixed since audit," item 13), including the previously-flagged hardcoded locations (`KeyboardSetupPage.swift`, `GlobeKeyTutorialPage.swift`). Still open: new ASC app record, new provisioning, and Apple Developer Portal registration of the new bundle IDs/App Group — account-level steps, not doable from a repo checkout.
7. Decide whether the `.private`-tagged transcript logging in `DictationCoordinator.swift:498` should be removed entirely rather than relying on OS-level redaction.
8. Add German UI localization if German is going to remain a marketed language, or adjust marketing claims to match actual UI language support.

---

Source files modified (2026-08-25, post-audit fixes 1–12, applied at user request across follow-up turns — see "Fixed since audit"): 12
- `DictusKeyboard/TextPrediction/AOSPTrieEngine.swift`
- `DictusApp/Views/LicensesView.swift` (two edits: FluidAudio correction, Parakeet/NVIDIA addition)
- `README.md` (full rewrite)
- `PRD.md` (targeted edits: title block, Executive Summary, Sections 2.1/3.1/4/11, trademark line, footer)
- `PRIVACY.md` (full rewrite: branding/contact only, substantive claims unchanged)
- `CONTRIBUTING.md` (full rewrite: branding + flagged the MIT contribution clause as pending the distribution decision)
- `CONTEXT.md` (light touch: title + one prose mention)
- `DEVELOPMENT.md` (targeted edits: scoping note added, narrative/forward-looking sections updated, literal current-state Xcode/Settings instructions left untouched)
- `KEYBOARD_BRIEFING.md` (light touch: title, intro line, footer)
- `DEVELOPMENT_AUDIO.md` (light touch: title, intro line, one table header)
- `CLAUDE.md` (branding + a genuine path-bug fix + two operational items flagged inline rather than guessed)

**Technical rebrand (2026-08-31, item 13)**: ~226 paths touched (git-tracked renames + edits) — 6 top-level folders/project renamed, `project.pbxproj` and 3 `.xcscheme` files rewritten, 3 entitlements files, `Info.plist`, `AppGroup.swift`, `Logger.swift`, `DarwinNotifications.swift`, `PersistentLog.swift`, `DictusApp.swift`, `DictationStatus.swift`, `KeyboardState.swift`, `DictusLiveActivity.swift`, `KeyboardSetupPage.swift`, `GlobeKeyTutorialPage.swift`, a unit test, `.github/workflows/ci.yml`, `.swiftlint.yml`, `tools/onboard_language.py`, `tools/ngram_builder.py`, plus copy-pasteable path/command references in `README.md`, `DEVELOPMENT.md`, and `docs/agents/language-onboarding.md`. Full detail in "Fixed since audit," item 13 — not enumerated file-by-file here given the volume.

Audit saved: `clients/kelly/dictation-app/audits/ios-audit.md` (this file).
