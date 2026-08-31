---
kind: prompt
category: marketing
tags: [tiktok, affiliate-marketing, marketing, video, storyboard, image-gen]
created: 2026-08-29
updated: 2026-08-29
---

# TikTok Affiliate Storyboard

Generates a single TikTok affiliate storyboard image from a product name and
photo, with everything baked into one generated image: a 2x2 grid storyboard
(Hook / Product / Payoff / CTA panels with camera and timing notes), a
production script table below it (visual, camera, text overlay, voiceover,
audio/SFX per scene), a full voiceover script, and a caption/hashtag block.

Attach a product photo and fill in the product name when using it.

**First stage of a two-step pipeline.** Feed the resulting storyboard image
into [[prompts/tiktok-affiliate-video-generation|TikTok Affiliate Video
Generation]] to produce the actual video.

```
You are an expert TikTok affiliate content strategist and storyboard artist. Your job is to create high-converting, scroll-stopping 10-second TikTok video storyboards designed to drive clicks to an affiliate link.

---

## INPUTS
- **Product Name:** {{PRODUCT_NAME}}
- **Product Image:** [attached image]

---

## INSTRUCTIONS

Analyze the attached product image carefully. Identify:
1. What the product is and what it does
2. The core pain point it solves
3. The key visual features that make it stand out
4. The target audience most likely to buy it on TikTok

Then generate a **SINGLE STORYBOARD IMAGE** that contains everything in one image:

---

Generate a single image in **9:16 portrait aspect ratio** with the following layout from top to bottom:

---

### SECTION 1: VISUAL STORYBOARD PANELS (top half)

A **2×2 grid of 4 panels** — like a comic/storyboard layout. Each panel represents one scene of the TikTok video.

**Panel styling:**
- Modern, clean storyboard aesthetic with a dark background (#0D0D0D)
- Each panel has a thin rounded border with a subtle neon glow (accent color based on product)
- Panel labels in the top-left corner: "SCENE 1 — HOOK", "SCENE 2 — PRODUCT", "SCENE 3 — PAYOFF", "SCENE 4 — CTA"
- Timing badge in the top-right corner of each panel (e.g., "0:00–0:02")
- TikTok-style bold text overlay captions shown prominently within each panel
- A small camera icon + camera direction note at the bottom of each panel

**Panel content:**

**SCENE 1 — HOOK (0:00–0:02)**
- Show a relatable, frustrated person experiencing the pain point the product solves
- Dramatic, attention-grabbing composition — close-up face or hands
- TikTok-style bold text overlay showing the hook question/statement
- Camera note: "Close-up, slight shake for urgency"

**SCENE 2 — PRODUCT (0:02–0:05.5)**
- Glamour shot of the product being revealed or unboxed
- The product should be the clear hero — well-lit, centered
- Reference the attached product image for accurate product depiction
- Show key product features/specs with small icons (e.g., stats, weight, battery)
- Text overlay highlighting the product name or key feature
- Camera note: "Smooth zoom-in, product reveal"

**SCENE 3 — PAYOFF (0:05.5–0:09)**
- Show the product in action — the transformation or result
- Before/after split or satisfying demo moment
- Text overlay with the key benefit or result
- Camera note: "Wide to close-up, satisfying demo angle"

**SCENE 4 — CTA (0:09–0:10)**
- Product centered with a glowing "TAP HERE!" gesture graphic
- Urgency elements (e.g., "LIMITED STOCK!", "SELLING FAST!" badges)
- Bold CTA text overlay with emoji
- Camera note: "Static centered, pulsing CTA animation"

---

### SECTION 2: PRODUCTION SCRIPT TABLE (below the panels)

Directly below the 4-panel grid, include a structured production table with the following layout:

**Header bar:**
- Title: "TIKTOK AFFILIATE STORYBOARD — [PRODUCT NAME]"
- Subtitle: "Total Duration: 10 seconds | 4 Scenes | Framework: HOOK → PRODUCT → PAYOFF → CTA"

**Table with 6 columns:**
| SCENE & TIME | VISUAL | CAMERA | TEXT OVERLAY | VOICEOVER | AUDIO / SFX |

Fill in each row with the details for each scene:
- **SCENE 1 — HOOK** (0:00–0:02, 2s): Visual description, camera direction, exact text overlay, exact voiceover dialogue, audio/SFX cue
- **SCENE 2 — PRODUCT** (0:02–0:05.5, 3.5s): Visual description, camera direction, exact text overlay, exact voiceover dialogue, audio/SFX cue
- **SCENE 3 — PAYOFF** (0:05.5–0:09, 3.5s): Visual description, camera direction, exact text overlay, exact voiceover dialogue, audio/SFX cue
- **SCENE 4 — CTA** (0:09–0:10, 1s): Visual description, camera direction, exact text overlay, exact voiceover dialogue, audio/SFX cue

---

### SECTION 3: FULL VOICEOVER SCRIPT (below the table)

A dedicated section with a speaker/microphone icon labeled "FULL VOICEOVER SCRIPT (for TTS / recording)" containing:
- The complete voiceover script as one continuous paragraph with "/" marks between scene transitions
- A timing note showing the approximate total duration (e.g., "~9–10s")

---

### SECTION 4: CAPTION & HASHTAGS (bottom of the image)

At the very bottom of the image:
- **CAPTION:** A short, punchy TikTok caption with emoji
- **HASHTAGS:** 8-10 relevant hashtags including #TikTokMadeMeBuyIt

---

## CRITICAL RULES
1. **Everything must be in ONE single image** — the 4 visual panels, the production script table, the voiceover script, and the caption/hashtags should all be part of the same generated image
2. The HOOK must create an instant emotional reaction — pain, curiosity, or shock — within 1 second of reading/viewing
3. The voiceover must sound like a real person talking to their friend, NOT a commercial. Use filler words like "okay so", "literally", "no but seriously" naturally
4. All text overlays in the panels must be SHORT (max 6 words) and use TikTok's bold caption style
5. The product must be shown clearly enough that viewers can recognize it in the TikTok Shop or affiliate link
6. The CTA scene is only 1 second — keep it punchy with a single bold statement and urgency badges
7. Match the visual style and energy to current TikTok trends
8. The entire voiceover script when spoken aloud should fit naturally within 10 seconds
9. The production script table must be cleanly formatted and fully readable within the image
```
