---
kind: changelog
client: kelly
project: avelisse-dictation-app
platform: ios
tags: [kelly, dictation-app, ios, changelog]
created: 2026-08-19
updated: 2026-08-31
---

# Avelisse Dictation App - iOS Updates

Changelog for `varbonida/avelisse-ios`. See [[clients/kelly/dictation-app/overview|Avelisse Dictation App]] for project overview, status, and decisions.

---

# 📝 Updates

### 2026-08-19

- Started log.
- Next focus: begin Dictus iOS rebranding (repo forked, own Git repo created).

### 2026-08-25

- Ran a full commercial-distribution audit (license, AI models, privacy, security, branding, App Store/keyboard, localization) and saved it to [[clients/kelly/dictation-app/audits/ios-audit|iOS Audit]]; resolved the Parakeet/NVIDIA model license question (confirmed CC-BY-4.0) and fixed two shipped license bugs.
- Rewrote all nine repo docs (README, PRD, PRIVACY, CONTRIBUTING, CONTEXT, DEVELOPMENT, KEYBOARD_BRIEFING, DEVELOPMENT_AUDIO, CLAUDE.md) to drop the inherited "free, open-source, MIT" framing and stale getdictus.com/PIVI links — pricing/contact info are explicit `[TBD]` placeholders, not false claims.
- Wrote `DESIGN.md` — translated the Android app's Mediterranean Coastal design system into native iOS terms — then implemented it across the app's color system (`DictusColors.swift` and every screen/component referencing it). The Live Activity widget and the cold-start swipe-back overlay were deliberately left on the old palette pending a dedicated re-theme pass, not a token swap.
- Next focus: verify the color-system change actually builds in Xcode (not possible from this environment), re-theme the two flagged leftover screens, resolve the sound-effect files' license/provenance, decide the `[PRICING TBD]`/contact placeholders, and complete the technical rebrand (new Bundle ID/App Group).

### 2026-08-31

- Completed the technical identity rebrand: Bundle ID `com.pivi.dictus` to `dev.avelissesolutions.avelisse` (+`.keyboard`/`.widgets`), App Group `group.solutions.pivi.dictus` to `group.dev.avelissesolutions.avelisse`, and URL scheme to `avelisse://` - matched to the domain root the Android app already committed to, so both platforms now share one identity.
- Renamed the Xcode project itself (`Dictus.xcodeproj` to `Avelisse.xcodeproj`), all three targets/schemes, and the six top-level folders (`DictusApp` to `AvelisseApp`, `DictusCore` to `AvelisseCore`, `DictusWidgets` to `AvelisseWidgets`, sound assets, CI workflow, lint config), hand-editing `project.pbxproj` since there's no Mac/Xcode available here.
- Caught and fixed three regressions the rename would've caused silently: two "is our keyboard installed" checks and a unit test still comparing against the old identifiers, plus six `dictus://` deep links (app, keyboard, Live Activity) that would've stopped opening.
- Left file/type names inside the code alone (`DictusApp.swift`, `import DictusCore`, `DictusColors.swift`, etc.) and the display name ("Dictus") - that's a separate source-level rebrand, not part of this pass.
- This is a source-level rename only, not a build - still cannot compile, run, or verify keyboard/app communication from this environment, since that still requires Xcode on a Mac. The no-Mac blocker is unchanged; what changed is how much is ready to verify once it clears.
- Next focus: open `Avelisse.xcodeproj` in Xcode to confirm it still parses and the App Group re-picks up under the dev team (unverifiable from this environment), then the sound-effect license, the `[PRICING TBD]`/contact placeholders, and the two flagged re-theme screens.
