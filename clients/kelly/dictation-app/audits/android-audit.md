---
kind: audit
client: kelly
project: avelisse-dictation-app
platform: android
scope: commercial distribution (license, dependencies, AI models, privacy, branding)
tags: [kelly, dictation-app, android, audit, licensing]
created: 2026-08-19
updated: 2026-08-19
---

# Dictus Android — Commercial Distribution Audit

Repo: `dictus-android` (branch `develop`), audited 2026-08-19.
Origin: open-source project by Pierre Viviere / PIVI Solutions (`github.com/getdictus/dictus-android`), MIT licensed. This is a keyboard app (IME) that does on-device Whisper/Parakeet speech-to-text.

---

### 🟢 Safe

- **Root license is MIT** (`LICENSE`, Copyright (c) 2024 Pierre Viviere) — commercial use, modification, rebranding, and closed-source redistribution are all permitted. Only requirement: keep the MIT copyright + permission notice included "in all copies or substantial portions" — i.e. it must still ship somewhere in the app (see Files to Preserve).
- **All 154 Maven/AndroidX dependencies resolve to Apache-2.0, MIT, or BSD-3-Clause** (verified via the `app.cash.licensee` Gradle plugin output, `app/build/reports/licensee/androidDebug/artifacts.json`) — all permissive, all commercial-safe, no copyleft (GPL/LGPL/AGPL) found anywhere in the dependency graph.
- **whisper.cpp** (vendored as git submodule `third_party/whisper.cpp`, pinned `v1.8.4-1-g7668414`): MIT, "Copyright (c) 2023-2026 The ggml authors". Commercial use/redistribution allowed.
- **sherpa-onnx** (Kotlin API source vendored under `asr/src/main/java/com/k2fsa/sherpa/onnx/`): Apache-2.0. Commercial use allowed; Apache-2.0 requires the license text + any NOTICE be retained (see below).
- **No analytics/telemetry/crash-reporting SDKs present** — no Firebase, Crashlytics, Sentry, Mixpanel, Amplitude, AppsFlyer, Bugsnag, etc. anywhere in the dependency list or source. The "no telemetry" claim in the README is accurate for network egress.
- **No hardcoded secrets/API keys** found in source. Release signing is via environment variables (`SIGNING_KEYSTORE_PATH`, etc.), nothing committed.
- **Network usage is scoped**: the only outbound HTTP traffic found is `ModelDownloader`/`ModelManager` pulling Whisper models from Hugging Face and Parakeet models from GitHub Releases. No other HTTP client instantiation exists in the codebase.
- Project already ships an in-app **Licences screen** (Settings → Licences) that auto-lists Maven deps via the licensee-generated `artifacts.json`, plus manual entries for whisper.cpp, sherpa-onnx, and the Parakeet model. This is a solid foundation to keep and just re-skin.
- `licensee { allow(...) }` in `app/build.gradle.kts` already gates the build to only the license types above — if a future dependency introduces a restrictive license, the build fails. Keep this.

### 🟡 Check

- **DM Sans font files** (`core/src/main/res/font/dm_sans_*.ttf`) are bundled with no accompanying `OFL.txt`/license file in the repo. DM Sans is normally SIL Open Font License 1.1 (permits commercial use/embedding, but reserves the font name and requires the OFL text travel with the font). Confirm the license and add the OFL text to the repo/NOTICE before shipping, since it's currently undocumented here.
- **NVIDIA Parakeet model** (`parakeet-tdt-0.6b-v3`, downloaded at runtime from `huggingface.co/nvidia/parakeet-tdt-0.6b-v3`) is declared in-app as CC-BY-4.0. CC-BY-4.0 permits commercial use but legally requires attribution to NVIDIA wherever the model is used/distributed — the in-app Licences screen currently provides this, so just carry that entry (or equivalent) into the rebrand; don't drop it in a redesign. Independently verify the current Hugging Face model card still states CC-BY-4.0 before shipping (upstream licenses do change).
- **Parakeet CTC-110M model** (`sherpa-onnx-nemo-parakeet_tdt_ctc_110m-en`, downloaded from the sherpa-onnx GitHub Releases) has no license statement anywhere in this repo (not in `ModelManager.kt`, not in `LicencesScreen.kt`). Verify its license/provenance on the sherpa-onnx / NeMo side before commercial redistribution — it may also be NVIDIA CC-BY-4.0, but this repo doesn't currently assert that.
- **Vendored prebuilt binaries with no source in this repo**: `asr/src/main/jniLibs/{arm64-v8a,armeabi-v7a}/libonnxruntime.so` and `libsherpa-onnx-jni.so` are precompiled `.so` blobs, not built from source here. onnxruntime is MIT, sherpa-onnx is Apache-2.0, both compatible — but confirm you can trace these specific binaries back to an official sherpa-onnx release (for supply-chain/provenance, not just license) before shipping a paid product built on them.
- **`org.checkerframework:checker-qual` (MIT)** and **`androidx.datastore:datastore-preferences-external-protobuf` (BSD-3-Clause)** are the only non-Apache-2.0 entries in the auto-generated Maven list — fine to ship, just make sure their notices land wherever you consolidate OSS notices.
- **Whisper GGML model weights** (downloaded from `huggingface.co/ggerganov/whisper.cpp`) trace back to OpenAI's original Whisper weights. OpenAI's Whisper is MIT-licensed (code and, per OpenAI, the released model weights), but this repo does not itself assert or display a license for the Whisper *model* the way it does for Parakeet — worth adding an explicit entry for consistency and to close the gap if OpenAI's position is ever challenged.
- **`third_party/whisper.cpp`** is a live git submodule pointed at the upstream `ggml-org/whisper.cpp` repo. Before a commercial release, vendor/pin it deliberately (already pinned to a tag+commit, good) and decide whether you keep pulling upstream or fork it, since upstream could change license/content later.

### 🔴 Blockers

- **Dictated text is written to a persistent, unencrypted log file in production (release) builds, not just debug.** `TimberSetup.init()` (`core/src/main/java/dev/pivisolutions/dictus/core/logging/TimberSetup.kt:27-34`) always plants `FileLoggingTree`, regardless of `BuildConfig.DEBUG` — only the Logcat `DebugTree` is gated to debug builds. `DictationService.kt:350` logs `Timber.d("Transcription result: raw='%s', processed='%s'", rawText, processedText)`, meaning every dictated sentence a user speaks (which could include passwords, financial info, private messages — this is a system-wide keyboard) is appended in plaintext to `filesDir/dictus.log` with no rotation, no size cap, and no expiry. That file is then user-exportable via Settings → "Export debug logs" (`LogExporter.kt`), which zips it and hands it to the Android share sheet (any app, e.g. email/Slack).
  - This directly undercuts a "100% on-device, no data retention" privacy claim if you intend to make one for a paid/rebranded product — the data never leaves the device *automatically*, but it is retained indefinitely on-disk and is one user tap away from leaving the device.
  - **Resolve before rebranding**: at minimum, gate transcript-content logging out of release builds (only gate the DebugTree currently), or strip transcript text from the log line, or add rotation/expiry and a clear in-app disclosure before shipping this as a commercial "privacy-first" product.

### Before Rebranding

1. **Fix the transcript logging issue above** — this is the one item that actively contradicts a "private/on-device" marketing claim and should be resolved before any public-facing release, paid or not.
2. **Verify DM Sans font licensing** and bundle the OFL license text (or swap fonts) — currently undocumented in-repo.
3. **Verify the Parakeet CTC-110M model's license** independently (not currently asserted anywhere in-app or in this repo).
4. **Change `applicationId`/`namespace`** off `dev.pivisolutions.dictus` (and the `ime`/`core`/`asr`/`whisper` module namespaces `dev.pivisolutions.dictus.*`) to your own package before publishing — required for Play Store regardless of license status, and avoids namespace collision with the original app if it's ever published under `dev.pivisolutions.dictus`.
5. **Replace all outward-facing branding**: app name "Dictus", GitHub links (`github.com/getdictus/dictus-android`, `github.com/Pivii/dictus`), website links (`getdictus.com`, `pivisolutions.dev/legal`), Telegram/email contacts, and the wordmark/icon assets (`app/src/main/res/mipmap*/ic_launcher*`). Full list of hit files is in the Dependency/branding grep below — search the codebase for `Dictus`, `getdictus`, `pivisolutions`, `PIVI` before your final build to confirm you got everything (124+ source files reference the `dev.pivisolutions.dictus` package alone).
6. **Do not remove or alter the MIT/Apache-2.0/CC-BY-4.0 attribution content** in the Licences screen while rebranding the UI shell around it — see Files to Preserve.
7. **Write your own privacy policy** rather than reusing `getdictus.com/en/privacy` or `pivisolutions.dev/legal` — the current in-app link points at PIVI's own site.
8. Confirm your release signing pipeline supplies its own keystore via the existing env-var mechanism (`SIGNING_KEYSTORE_PATH` etc. in `app/build.gradle.kts`) — nothing to fix here, just don't reuse PIVI's signing identity.

### Files to Preserve

These are legally-required attribution/license content, not "Dictus branding" — keep the substance even if you redesign the screen:

- `LICENSE` (root MIT) — you may add your own copyright line for your modifications alongside Pierre Viviere's original notice, but the original notice must remain somewhere in the distributed product (commonly an in-app "Open Source Licenses" or "About" screen — which this app already has).
- `third_party/whisper.cpp/LICENSE` (MIT, ggml authors).
- The Apache-2.0 license text/attribution for **sherpa-onnx**.
- The CC-BY-4.0 attribution for **NVIDIA Parakeet** models.
- The auto-generated Maven OSS notices (`app/cash/licensee/artifacts.json`, surfaced via `LicencesScreen.kt`) — keep the generation pipeline (the `licensee` Gradle plugin + the asset-copy task in `app/build.gradle.kts`), just restyle the screen.
- Whatever license file you obtain for **DM Sans** once confirmed (OFL.txt).

### Dependency Summary

| Dependency | License | Commercial use | Notes |
|---|---|---|---|
| All AndroidX / Jetpack Compose libs (~140 artifacts: Activity, Lifecycle, Navigation, DataStore, Compose UI/Material3, etc.) | Apache-2.0 | ✅ | Auto-verified via licensee plugin |
| Kotlin stdlib, kotlinx-coroutines | Apache-2.0 | ✅ | |
| Dagger / Hilt | Apache-2.0 | ✅ | |
| Timber (Jake Wharton) | Apache-2.0 | ✅ | |
| OkHttp (Square) | Apache-2.0 | ✅ | Used only for model downloads |
| Apache Commons Compress | Apache-2.0 | ✅ | Used to extract Parakeet `.tar.bz2` archives |
| Robolectric (test-only) | MIT | ✅ | Not shipped in APK |
| `org.checkerframework:checker-qual` | MIT | ✅ | Transitive |
| `androidx.datastore:datastore-preferences-external-protobuf` | BSD-3-Clause | ✅ | Transitive |
| whisper.cpp (vendored submodule, native STT engine) | MIT | ✅ | Attribution notice must stay in app |
| sherpa-onnx (Kotlin API vendored as source; `libsherpa-onnx-jni.so`, `libonnxruntime.so` vendored as prebuilt `.so`) | Apache-2.0 (onnxruntime: MIT) | ✅ | Verify binary provenance |
| DM Sans (font, `core/src/main/res/font/`) | Presumed SIL OFL 1.1 — **unconfirmed in-repo** | 🟡 Likely ✅ | No license file bundled; confirm and add |

### AI/Model Summary

| Model | Provider/Source | License (as declared in-app) | Commercial use | Notes |
|---|---|---|---|---|
| Whisper GGML (tiny/base/small/small-q5_1/medium-q5_0) | Downloaded at runtime from `huggingface.co/ggerganov/whisper.cpp` | Not explicitly asserted in-app; upstream OpenAI Whisper is MIT | 🟡 Likely ✅ | Add an explicit in-app entry for consistency; verify current HF repo terms |
| Parakeet TDT 0.6B v3 | Downloaded at runtime from sherpa-onnx GitHub Releases; original weights from `huggingface.co/nvidia/parakeet-tdt-0.6b-v3` | CC-BY-4.0 (NVIDIA) — declared in `LicencesScreen.kt` | ✅ with attribution | Attribution UI already exists — keep it |
| Parakeet CTC 110M int8 | Downloaded at runtime from sherpa-onnx GitHub Releases | **Not declared anywhere in-repo** | 🟡 Unverified | Confirm license/provenance before shipping |
| STT inference engines (whisper.cpp native, sherpa-onnx/onnxruntime native) | See Dependency Summary | MIT / Apache-2.0 | ✅ | Engines, not weights — distinct from the model files above |

All models are downloaded on first use over plain HTTPS from the vendor's own hosting (Hugging Face, GitHub Releases) directly by the end user's device — none are bundled in the APK, and none are proxied through PIVI/Dictus infrastructure. No custom/proprietary Dictus-trained model exists in this repo.

---

Source files modified: 0
Audit saved: Android Audit.md
