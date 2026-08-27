---
kind: changelog
client: kelly
project: avelisse-dictation-app
platform: ios
tags: [kelly, dictation-app, ios, changelog]
created: 2026-08-19
updated: 2026-08-25
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
