---
kind: prompt
category: video-production
tags: [faceless-video, ai-drama, reverse-engineering, phase-b, image-gen]
created: 2026-09-06
updated: 2026-09-06
---

# Step 11 - Shot-by-Shot Image Prompts

Phase B. One prompt per shot, describing only the starting frame - what the
shot looks like, not what happens in it. That distinction matters: an image
prompt and a video prompt (Step 12) do different jobs and should never be
merged into one. See
[[projects/faceless-video-content/reverse-engineering-videos/index|the workflow overview]].

```
Using the Character Bible, Environment Bible, and Production-Ready Shot Plan, create one image-generation prompt for each shot.

Each image prompt must describe the STARTING FRAME of the shot.

Include:
- Character identity and appearance
- Character clothing
- Character pose
- Facial expression
- Body language
- Character position
- Environment
- Important props
- Composition
- Shot size
- Camera angle
- Lens/look
- Depth of field
- Lighting
- Color palette
- Atmosphere
- Visual emphasis
- Cinematic realism
- Important continuity details

The generated image should function as the visual starting frame for the corresponding video prompt.

Maintain strict consistency with the Character Bible and Environment Bible.

Do not introduce new character traits, props, locations, or visual details that contradict the bibles.
```
