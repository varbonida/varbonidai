---
kind: prompt
category: marketing
tags: [tiktok, affiliate-marketing, marketing, video, image-gen]
created: 2026-08-29
updated: 2026-08-29
---

# TikTok Affiliate Video Generation

Turns a TikTok affiliate storyboard image into an actual 10-second vertical
video: raw UGC style, natural voiceover matched to the storyboard's production
script, snappy jump cuts between scenes, TikTok-style caption overlays.

**Second stage of a two-step pipeline.** Run
[[prompts/tiktok-affiliate-storyboard|TikTok Affiliate Storyboard]] first to
produce the storyboard image and production script, then attach that image to
this prompt to generate the video itself. No other input is needed - the
storyboard image carries the product, scenes, timing, dialogue, and camera
directions this prompt reads from.

```
Generate a 10-second vertical video (9:16 aspect ratio) based on the attached TikTok affiliate storyboard image.

The attached image contains everything you need:
- Top section: A 2x2 grid showing 4 visual panels (HOOK → PRODUCT → PAYOFF → CTA) with camera directions and timing
- Bottom section: A production script table with exact scene-by-scene details including VISUAL descriptions, CAMERA directions, TEXT OVERLAY content, VOICEOVER dialogue, and AUDIO/SFX cues
- A full voiceover script for recording/TTS

Read the entire storyboard image carefully and use ALL the information to generate the video.

GLOBAL STYLE DIRECTIVE:
- Visual style: Raw UGC (user-generated content), shot on a smartphone, natural lighting, slightly handheld camera feel, authentic creator vibe — NOT polished or cinematic
- Text style: All on-screen text should appear as TikTok-style bold white captions with a black drop shadow, matching the text overlays shown in the storyboard panels
- Aspect ratio: 9:16 vertical / portrait
- The person and product in the video should match what is depicted in the storyboard panels

SCENE INSTRUCTIONS:
- Follow the exact timing shown in each panel header (SCENE 1: 0:00–0:02, SCENE 2: 0:02–0:05, SCENE 3: 0:05–0:08, SCENE 4: 0:08–0:10)
- Recreate each scene's visual composition as shown in the storyboard panels
- Apply the camera direction noted at the bottom of each panel
- Display the text overlays exactly as written in each panel
- Use the voiceover dialogue from the production script table — spoken naturally, not read robotically
- Apply the audio/SFX cues listed in the AUDIO/SFX column of the production script

VOICE DIRECTION:
- Voice should sound like a real young person talking casually to their phone camera — energetic, authentic, slightly breathy with excitement
- NOT a commercial voiceover — think a creator genuinely recommending something to a friend
- Pacing should be natural but quick enough to fit all dialogue within 10 seconds
- Match the exact words from the VOICEOVER column in the storyboard's production script

TRANSITION DIRECTION:
- Use quick, snappy cuts between scenes — no fades or dissolves
- Each cut should feel like a natural TikTok jump cut
- Maintain visual continuity of the person and setting across all 4 scenes

IMPORTANT:
- Keep the entire video exactly 10 seconds
- The product must be clearly recognizable and match the product shown in the storyboard
- Text overlays should be large, readable, and timed to appear with the voiceover
- The overall feel should be indistinguishable from organic TikTok creator content
```
