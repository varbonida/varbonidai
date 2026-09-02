---
kind: changelog
client: kelly
project: avelisse-dictation-app
platform: ios
tags: [kelly, dictation-app, ios, changelog]
created: 2026-08-19
updated: 2026-09-02
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

### 2026-09-02

- Re-themed the Live Activity to Mediterranean Coastal, the first of the two screens left over from the color-system pass. Used the Impeccable skill because it wasn't a token swap: the Dynamic Island renders on Apple's fixed black canvas (left white text/icons there, that's system chrome) while the Lock Screen banner is ours, so it went from dark navy to a white card with dark text - no longer the one leftover dark surface in a light app. Tradeoff: Clay Red and Sea Teal weren't designed against black and land around 3.9-4.3:1 there, under the 4.5:1 body-text bar but over the 3:1 floor for the bold text and icons actually used.
- Completed the source-level rename (~187 paths): module `DictusCore` to `AvelisseCore` with all 78 imports, 26 files renamed, ~10 types, ~220 design tokens, the C++ `dictus::` namespace, and the user-facing name - display name, mic prompt, Settings bundle, and 13 localization keys moved with their French translations, then the French values updated too since they still said "Dictus" after the key rename.
- Three things deliberately kept as Dictus, each for a specific reason: the `LicensesView` MIT block (it credits PIVI Solutions - rebranding it would misattribute their work; the blanket replace did clobber it and I restored it with a comment), the `"dictus."` storage keys (`KeyboardMode` reads one as a legacy migration key, so renaming silently breaks upgrades), and the `DTRI` magic bytes in the trie format (renamed the constant, kept the bytes - they're in the header of every shipped `.dict` file and would fail at runtime, not compile time).
- Caught that `scripts/curate_{de,en,fr}_dictionary.py` were still writing to `DictusKeyboard/Resources/`, a path that stopped existing in the previous rename - broken since 08-31, missed then.
- Still unverified: neither rename has been opened in Xcode. They're separate commits (`229f483` is the identifier pass, this one isn't committed yet) so a failure can be bisected. Symbol misses would be build errors rather than silent bugs, and the sweeps show zero orphans, but that isn't the same as the project actually parsing.
- Killed two dead links: deleted `.github/FUNDING.yml` (its only content was a getdictus.com donate link, so a Sponsor button on our repo would have routed money to the upstream author), and removed the Settings > About GitHub row, which pointed at a nonexistent `github.com/Pivii/dictus` org. Removed rather than repointed since our own repo URL is still TBD - left a comment saying how to restore it.
- Re-themed `SwipeBackOverlayView`, the last screen on the old palette. It went light like the rest of the app: it appears transiently during cold start between two light screens, so a dark full-screen flash reads as a rendering glitch, not a design choice.
- Three parts needed real work rather than a token swap: the phone mockup gained a white surface fill (a stroke alone described the device fine on dark, but would leave it floating on light), the waveform's edge bars moved off white since they'd be invisible against that fill, and the moving dot lost its stacked glows - two zero-offset halos are a dark-mode trick that just muddies on light, so it's now solid teal with one soft offset shadow. Animation timing and layout untouched.
- The old Dictus palette is now fully retired from app, keyboard, core and widget source - zero hardcoded hex left. The one holdout is `scripts/generate-app-icon.swift`, which still generates the dark-navy icon; that needs an actual icon design decision, not a hex swap, and DESIGN.md already flags it (Android's launcher icon is where Mediterranean Coastal came from, so iOS's icon is the one out of step).
- Next focus unchanged and now the only real blocker on my side: open `Avelisse.xcodeproj` in Xcode. Three passes are stacked unverified - the identifier rename (`229f483`, committed), the source-level rename, and today's theming. Then the sound-effect license and the `[PRICING TBD]`/contact placeholders, both still waiting on decisions.
