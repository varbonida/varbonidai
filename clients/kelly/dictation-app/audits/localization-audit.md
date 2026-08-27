---
kind: audit
client: kelly
project: avelisse-dictation-app
platform: android
scope: hardcoded user-facing text and default-locale correctness
tags: [kelly, dictation-app, android, audit, localization]
created: 2026-08-21
updated: 2026-08-21
---

# Dictus/AVELISSE Android — Localization Audit

Repo: `dictus-android` (branch `develop`), audited 2026-08-21.
Scope: hardcoded user-facing text, missing/incomplete localization, and default-locale correctness across the `app`, `core`, and `ime` modules. Triggered by a user report that the **Models screen still displays French text** after English was set as the default language.

Source files modified: 0 (audit only).

---

## Hardcoded User-Facing Text

| File | Location | Text | Language | Recommended Action |
|------|----------|------|----------|--------------------|
| `app/.../model/ModelManager.kt` | `ModelInfo.qualityLabel`, lines 93,103,113,123,133,145,157 | `"Rapide"`, `"Equilibre"`, `"Precis"` (×3), `"Premium"` | French (except "Premium") | Move to `strings.xml`, resolve via `stringResource()` where `qualityLabel` is displayed |
| `app/.../model/ModelManager.kt` | `ModelInfo.description`, lines 94,104,114,124,134,146,158 | `"Rapide et leger"`, `"Precis et equilibre"`, `"Haute precision"`, `"Meilleur compromis"`, `"Meilleure precision"`, `"Anglais uniquement - Rapide et precis"`, `"25 langues - Detection automatique"` | French | Move to `strings.xml`, resolve via `stringResource()` in `ModelCard.kt` |
| `app/.../ui/models/ModelCard.kt:327` | model size label | `"~$sizeMb Mo"` | French ("Mo" = Méga-octets) | Replace with a `strings.xml` template, e.g. `model_size_mb` → `"~%1$d MB"` |
| `app/.../home/HomeScreen.kt:137` | active-model size label | `"~$sizeMb Mo"` | French | Same fix as above — reuse the same string resource |
| `app/.../ui/onboarding/ModePickerCard.kt:69,77` | `description = "Lettres"` / `"Chiffres"` | French | Move to `strings.xml` (e.g. `onboarding_mode_letters`/`_numbers`) |
| `app/.../ui/settings/LicencesScreen.kt:116` | section header | `"Vendored & Non-Maven"` | English, hardcoded | Move to `strings.xml` for translatability |
| `ime/.../ui/MicButtonRow.kt:65,94` | `contentDescription` | `"Settings"`, `"Microphone"` | English, hardcoded | Move to `strings.xml` (accessibility text should be localized) |
| `ime/.../ui/RecordingScreen.kt:174` | `contentDescription` | `"Settings"` | English, hardcoded | Same fix |
| `app/.../service/DictationService.kt:475` | `NotificationChannel.description` | `"Active recording notification"` | English, hardcoded | Move to `strings.xml` — visible in system Settings → App → Notifications |

**Reviewed and excluded (not bugs):** `"AVELISSE"` wordmark/clipboard labels (brand name, intentionally not translated), `"WK"`/`"NV"` provider badges (abbreviation codes), `"ABC"`/`"123"` keyboard layer labels (universal keyboard convention, matches AOSP/Gboard behavior), single-glyph icons (`✓`, `✗`, `⌫`), `animateFloatAsState(label = ...)` debug labels (tooling-only, never rendered), `SuggestionEngine.kt`'s bilingual FR+EN seed word list (predictive-text data, not UI chrome), `LicencesScreen.kt`'s `author = "Get Dictus"` / copyright text (attribution notice, correctly preserved per earlier explicit instruction).

---

## Models Screen

Every French string currently reaching the Models screen comes from `ModelManager.kt`'s `ModelCatalog`, not from `ModelsScreen.kt`/`ModelCard.kt` (both already use `stringResource()` correctly everywhere else):

- Quality badges: **Rapide**, **Equilibre**, **Precis** (×3 models), **Premium**
- Descriptions: **Rapide et leger**, **Precis et equilibre**, **Haute precision**, **Meilleur compromis**, **Meilleure precision**, **Anglais uniquement - Rapide et precis**, **25 langues - Detection automatique**
- Size unit: **"~77 Mo"** style labels on every model card (should be "MB")

The `qualityLabel` field also leaks into **Onboarding Step 5** (`OnboardingModelDownloadScreen.kt`), and the size-unit bug is duplicated on the **Home screen**'s active-model card — so this isn't Models-screen-only, it's a catalog-wide issue.

---

## Localization Issues

- **Root cause:** `ModelInfo` (`ModelManager.kt`) stores `qualityLabel` and `description` as plain hardcoded `String` literals baked directly into the static catalog, instead of `@StringRes` IDs resolved via `stringResource()` like every other piece of Models-screen text. This is the only place in the audited codebase where UI-facing content structurally bypasses the localization system rather than just missing a translation.
- **String-resource parity is otherwise clean:** every key in `values/strings.xml` has a matching `values-fr/strings.xml` entry across all three modules (`app`, `core`, `ime`) — confirmed via full key-diff, zero gaps. The localization *architecture* itself works; specific call sites just don't use it.
- **Unit-format inconsistency as direct evidence:** `AppNavHost.kt:199` already correctly builds `"~$modelSizeMb MB"` (English) for the onboarding recommendation card, while `ModelCard.kt` and `HomeScreen.kt` independently hardcode `"~$sizeMb Mo"` (French) for the same concept — clear copy-paste drift from unlocalized code, not a deliberate design choice.
- **Default/fallback locale itself is correct** (per prior work): system language if supported (fr/en), else English, for both interface and transcription language. This audit found no regression there — the remaining French text is unrelated to that logic; it's literal, unconditional French baked into Kotlin source that displays identically regardless of locale.

---

## Recommended Fixes

1. **Models screen (highest priority):** Move `ModelInfo.qualityLabel` and `ModelInfo.description` out of `ModelManager.kt` into `strings.xml` (7 models × 2 fields), then resolve them via `stringResource()` at each display site (`ModelCard.kt`, `OnboardingModelDownloadScreen.kt`). Fix the `"Mo"` → `"MB"` literal in `ModelCard.kt:327` and `HomeScreen.kt:137` using one shared string resource, matching `AppNavHost.kt`'s existing correct pattern.
2. **Other visible hardcoded text:** Localize `ModePickerCard.kt`'s `"Lettres"`/`"Chiffres"` (onboarding, French — user-visible on every fresh install), then the English-but-hardcoded set: `LicencesScreen.kt`'s section header, the two IME `contentDescription` strings, and the notification channel description.
3. **Architecture:** No structural change needed to the localization system itself (it's sound and fully in parity) — just eliminate the two spots (`ModelInfo` fields, and a handful of scattered literals) that bypass `stringResource()`/`strings.xml` entirely.
