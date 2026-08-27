---
kind: audit
client: kelly
project: avelisse-dictation-app
platform: android
scope: leftover Dictus/PIVI Solutions references after technical identity rebrand to AVELISSE
tags: [kelly, dictation-app, android, audit, branding]
created: 2026-08-24
updated: 2026-08-24
---

# Dictus / PIVI Solutions Reference Audit — AVELISSE Android

Read-only audit. No files modified. Repo: `avelisse-android` (branch `develop`).

Search patterns: `dictus`, `Dictus`, `DICTUS`, `pivisolutions`, `PIVI`, `getdictus`, `dev.pivisolutions.dictus` (case-insensitive).

**165 git-tracked files** contain at least one match, **5,133 total occurrences** (case-insensitive count across tracked files). Two additional matches exist outside version control (`.idea/workspace.xml`, `app/release/app-release.apk`) — both gitignored, noted separately below, not part of the tracked repository.

The technical identity rebrand (`dev.pivisolutions.dictus` → `dev.avelissesolutions.avelisse`, package dirs, class names, JNI symbols, `LicencesScreen.kt` colors) is confirmed complete and correct in live source (`app/`, `core/`, `ime/`, `asr/`, `whisper/`). Everything found in this audit is either (a) prose/config/docs never touched by that pass, or (b) intentionally-preserved third-party attribution.

---

## 1. Safe to Replace

| File | Reference | Recommended Replacement | Reason |
|------|-----------|--------------------------|--------|
| `app/src/main/java/dev/avelissesolutions/avelisse/ui/settings/SettingsScreen.kt:236` | `url = "https://github.com/Pivii/avelisse"` | `https://github.com/<actual-avelisse-org>/avelisse-android` (or correct current repo URL) | **Live in-app bug from the partial rebrand** — this is neither the old identity nor the new one; it mixes the old GitHub org (`Pivii`) with the new repo name (`avelisse`), producing a link that almost certainly 404s. This is the highest-priority item in this audit since it's user-facing, not historical. |
| `README.md` (31 refs: title, badges, links, comparison table, roadmap, community section, footer credit) | "Dictus", `getdictus/dictus-android`, `getdictus.com`, `t.me/getdictus`, `hello@getdictus.com`, `pivi.solutions` | AVELISSE name, new repo URL, new website/contact | Root README is 100% outward-facing product branding — describes the *current* product, not history. Every reference here describes what the app is *now*, so all should read AVELISSE. Does not touch the required License section wording itself. |
| `CONTRIBUTING.md` (5 refs) | "Dictus" project name, `github.com/getdictus/dictus-android.git`, `DictusImeService.kt` reference | AVELISSE name, new clone URL, `AvelisseImeService.kt` | Build/contribution instructions for the live repo — should reflect current class/repo names post-rename. |
| `CLAUDE.md` (project root, 5 refs) | "Dictus Android", `design/dictus-android-design.pen` | "AVELISSE Android" title; update path if design files are renamed (see §2) | Project instructions describing the current app; not historical. |
| `design/README.md` (6 refs) | "Dictus Android — Design Reference", `dictus-android-design.pen`, `dictus-keyboard-design.pen` filenames | "AVELISSE Android — Design Reference"; update filenames if `.pen` files are renamed | Design-doc title/prose describing current app; not itself licensed content. |
| `.github/workflows/release.yml:56` | `name: Dictus ${{ steps.version.outputs.version_name }}` | `name: AVELISSE ${{ steps.version.outputs.version_name }}` | Cosmetic GitHub Release title text, purely CI config, zero legal weight. |
| `.github/FUNDING.yml:1` | `custom: ["https://getdictus.com/donate"]` | Replace with AVELISSE's own funding link, or remove (see §2) | Points to the *original maintainer's own* donation page — routing new-project donations there would be actively wrong, not just stale branding. Not an attribution requirement (funding links aren't part of MIT's notice-preservation clause). |
| `PRD.md` (40 refs throughout) | "Dictus Android" title/body text, `Author: Pierre / PIVI Solutions`, internal class-name references (`DictusIME.kt`, `DictusColors.kt`, etc.), `github.com/Pivii/dictus-android` | AVELISSE naming throughout; note the iOS-parity sections (§2, §13) reference the *iOS* Dictus app for architecture comparison — see §4, those specific mentions should stay as historical/reference context even if the doc title changes | This is a living planning document for *this* Android app's requirements, not a historical record — but it also contains legitimate "ported from iOS Dictus" comparison content (see §4) that shouldn't be scrubbed, just not conflated with the product's own name. |

## 2. Safe to Remove

| File | Reference | Reason |
|------|-----------|--------|
| `app/release/app-release.apk` (gitignored, not tracked) | Old package identity baked into a compiled binary | Stale pre-rebrand build artifact sitting on disk; not part of the git repo (matches `.gitignore` line 8 `*.apk`). Rebuild and discard rather than "fix" — it's disposable output, not source. |
| `.idea/workspace.xml` (gitignored, not tracked) | `dictus-android.app` module name, `dictus-release-key.jks` keystore alias, `dev.pivisolutions.dictus` run-config entries | Already flagged in the prior rebrand session — IDE-local, machine-specific, regenerated by Gradle sync. Not part of the repository; no action needed here beyond the sync/reselect-run-config step already recommended. |
| `.github/FUNDING.yml` | `getdictus.com/donate` | Alternative to replacing (see §1): if AVELISSE has no funding page yet, simplest correct action is deleting this file entirely rather than leaving a dead or misdirected link. |
| `design/dictus-android-design.pen`, `design/dictus-keyboard-design.pen` filenames | "dictus" in filename | Obsolete branding in filenames of internal design-tool reference files (Pencil MCP tool source files, not shipped in the app, not license-bearing). Safe to rename to `avelisse-android-design.pen` / `avelisse-keyboard-design.pen` — just remember to update the frame-ID paths in `design/README.md` and the project `CLAUDE.md` reference to match (see §1). |

## 3. MUST PRESERVE

| File | Reference | Why It Must Remain |
|------|-----------|---------------------|
| `LICENSE` (root) | `Copyright (c) 2024 Pierre Viviere` + full MIT permission text | **Hard legal requirement.** MIT License requires "The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software." AVELISSE may add its *own* copyright line for its own modifications alongside this one, but must not remove or replace Pierre Viviere's original notice. |
| `app/src/main/java/dev/avelissesolutions/avelisse/ui/settings/LicencesScreen.kt:158-162` | `author = "Get Dictus"`, `url = "https://github.com/getdictus/dictus"`, `licenceText = mitLicence("Copyright (c) 2026 Get Dictus")` | Required MIT attribution block for the original codebase this Android app derives from, surfaced in-app per the license's "included in all copies" clause. This was correctly and deliberately preserved during the earlier rebrand pass in this session — confirm it stays untouched in any future pass. |
| `LicencesScreen.kt:41` (doc comment) | `"...(whisper.cpp, sherpa-onnx, Parakeet, Dictus)"` | Not itself a legal requirement (it's a code comment), but describes the *purpose* of the attribution block immediately below it (which is legally required). Recommend leaving as-is or updating to say "the original Dictus project" for clarity — cosmetic either way, doesn't carry legal weight on its own. Listed here rather than §1 because changing it carelessly right next to the real attribution block invites someone to also "clean up" the required lines below it. |

## 4. Third-Party / Historical References

| File | Reference | Reason to Preserve |
|------|-----------|----------------------|
| `PRD.md` §2, §13 ("iOS App Recap — What Dictus Is", "Glossary — iOS to Android Mapping") | `DictusApp`, `DictusKeyboard`, `DictusCore` (iOS target names), Dictus iOS architecture description | These describe the **original iOS Dictus app** that this Android app was ported from — legitimate historical/reference context for engineering decisions (e.g., "iOS Dictus uses Liquid Glass; Android cannot replicate this"). Rewriting these to say "AVELISSE" would misrepresent which codebase actually made those design choices. Keep, but could optionally be prefixed "iOS Dictus (original project)" for clarity when the doc title changes. |
| All `.planning/**/*.md` (approx. 150 files — see §6) | `Dictus`, `dev.pivisolutions.dictus`, `DictusImeService`, etc. throughout milestone plans, summaries, research, validation, and debug docs from v1.0 and v1.1 development | Point-in-time historical build record — plans, summaries, and debug logs written *while the app was still called Dictus*. Confirmed via spot-check (8 files across `PROJECT.md`, `ROADMAP.md`, milestone audits, phase plans/summaries, research docs, and a "quick task" doc) that every reference is either prose describing the app's name at the time of writing, or a pasted file path/class name from that era's source tree. Rewriting history here would make these docs inaccurate records of what actually happened at each point in time. Not part of the shipped product. |
| `third_party/whisper.cpp/**` | (not directly matched by this audit's grep, but flagged for completeness) | Vendored MIT-licensed upstream submodule (Georgi Gerganov / ggml authors). Nothing inside it is project-owned; do not touch regardless of what strings it contains. |
| `asr/src/main/java/com/k2fsa/sherpa/onnx/**` | (not matched by this audit's grep) | Vendored Apache-2.0 sherpa-onnx Kotlin API source (k2-fsa / Next-gen Kaldi). Third-party, not project-owned. |

## 5. Needs Manual Review

- **`SettingsScreen.kt:236` GitHub link** (also listed in §1 as "safe to replace" in direction, but the *correct target URL* needs a human decision) — is there an actual `avelisse-android` GitHub repo yet, and under what org? The current string is broken/mixed-identity regardless, but I can't determine the right replacement URL without knowing AVELISSE's actual GitHub org name.
- **`.github/FUNDING.yml`** — replace with AVELISSE's own funding link, or delete outright? Depends on whether AVELISSE intends to accept donations at all; either resolution is legally fine, this is a business decision not a compliance one.
- **`PRD.md` title and authorship line** (`Author: Pierre / PIVI Solutions`) — this is a *requirements document for the Android port*, arguably now superseded/historical in its own right (the port it specifies is done and rebranded). Worth asking whether this file should be updated in place (retitled to AVELISSE) or left as a dated historical record like the `.planning/` tree, since it currently sits in a middle ground — it's not in `.planning/` but reads like a point-in-time spec rather than living documentation.
- **`design/*.pen` file renames** — renaming these (§2) will break the `design/README.md` usage examples and the project `CLAUDE.md` path reference unless updated together; also unclear whether the Pencil MCP tool's own external references/cache key off the filename in a way that matters. Recommend testing that the Pencil tools still resolve the files correctly after any rename before treating this as done.
- **App-facing string resources**: this audit searched file content for the literal strings requested; it did NOT separately re-verify every `strings.xml` value display string (e.g., "About Dictus"-style UI copy) beyond what the content grep already caught — none were found by the grep, which is a good sign, but a final manual skim of `app/src/main/res/values*/strings.xml` and `core/src/main/res/values*/strings.xml` for anything sounding like leftover Dictus copy (not matching the literal search strings, e.g. a paraphrase) is worth a quick human pass since string content wasn't the previous rebrand pass's literal focus beyond the identifier strings.

## 6. README / Markdown Files

| File | Recommendation | Reason |
|------|------------------|--------|
| `README.md` (root) | **Replace** | Current product-facing description; all 31 references are outward branding, not history. |
| `CONTRIBUTING.md` | **Replace** | Live build/contribution guide for the current repo. |
| `PRD.md` | **Replace title/branding; Preserve the iOS-Dictus comparison sections** (§2, §13) | Mixed document — see §1 and §4 above. Needs a human decision on whether to retitle in place or archive (see §5). |
| `CLAUDE.md` (project root) | **Replace** | Describes the current project for AI-assisted development; should match current identity. |
| `design/README.md` | **Replace** | Describes current design-reference files; update alongside any `.pen` filename changes. |
| All `.planning/**/*.md` (~150 files: `PROJECT.md`, `ROADMAP.md`, both `v1.0-*` and `v1.1-*` milestone trees, `research/*.md`, `debug/*.md`, `quick/*.md`) | **Preserve as-is** | Historical planning/build record — confirmed via spot-check of 8 representative files across different subfolders and milestones; every occurrence is either era-accurate prose ("Dictus is a custom keyboard...") or a pasted old file path/class name from that period's source tree. No outlier found: no live legal statement, no still-actionable checklist referencing a currently-relevant URL, nothing contradicting the "historical record" pattern. Not in scope of the technical rebrand and rewriting them would falsify the historical record of what the app was called when each decision was made. |

No other `.md` files in the repo contain matches beyond the ones listed above and the `.planning/` tree.

---

## Final Summary

- **References found:** 5,133 occurrences (case-insensitive, git-tracked files only)
- **Files affected:** 165 tracked files (+ 2 untracked/gitignored: `.idea/workspace.xml`, `app/release/app-release.apk`)
- **Safe to replace:** 8 files (`SettingsScreen.kt`, `README.md`, `CONTRIBUTING.md`, `CLAUDE.md`, `design/README.md`, `.github/workflows/release.yml`, `.github/FUNDING.yml`, `PRD.md` — partial)
- **Safe to remove:** 4 items (`app-release.apk`, `.idea/workspace.xml` — both already gitignored/no action needed, `.github/FUNDING.yml` as an alternative to replacing, 2 `design/*.pen` filenames as a rename)
- **Must preserve:** 3 items (root `LICENSE`, `LicencesScreen.kt`'s "Get Dictus" MIT attribution block, its adjacent doc comment)
- **Third-party / historical:** ~152 files (`PRD.md`'s iOS-comparison sections + the entire `.planning/` tree of ~150 files)
- **Needs manual review:** 4 open questions (correct new GitHub URL, FUNDING.yml disposition, PRD.md's own status as living vs. historical, `.pen` rename follow-through)

Files modified: 0
