---
kind: prompt
category: video-production
tags: [faceless-video, ai-drama, reverse-engineering, gemini, claude-code, workflow]
created: 2026-09-06
updated: 2026-09-06
---

# Reverse-Engineering AI Drama Videos

Canonical 13-step workflow for taking an existing short AI drama video (the
kind of animal/human melodrama short common on Shorts/Reels), extracting how
it's built, and using that structure to produce an original video. See
[[projects/faceless-video-content/overview|Faceless Video Content]] for the
project this serves.

Each step's copy-paste prompt lives in its own file: `step-01.md` through
`step-13.md` (zero-padded so the files sort correctly in a file browser,
unlike the plain `step-1`/`step-2` numbering the steps are discussed with).

## Tool division

- **Gemini - video analysis (Steps 1-6).** Gemini can natively ingest video,
  audio, and timestamps and reference specific moments directly - the actual
  strength this workflow depends on for the reverse-engineering half.
- **Claude Code - automation and implementation (Steps 7-13 onward).**
  Turning the analysis into scripts, organized project files, a prompt
  system, and a repeatable pipeline. Claude Code does not have native video
  analysis (a 2026 feature request for it was closed as not planned), so it
  is not used for Steps 1-6.
- **GPT-5.6 Luna - methodology design.** Designed and iterated this workflow
  itself; not part of the per-video pipeline.

## The two phases

**Phase A - reverse-engineer a reference (Steps 1-6).** Run once per
reference video whose construction you want to study. Output is that video's
reusable "blueprint" - the storytelling mechanics, not the specific story.

**Phase B - create an original video (Steps 7-13).** Run once per new video
you produce. Does **not** repeat Steps 1-6 - it starts from an existing
blueprint (see below) and produces a new, original story built on the same
mechanics.

## Running Steps 1-6 against Gemini

- Upload the reference video once, then run the six step prompts
  **sequentially in the same conversation**, not as one combined prompt -
  one prompt covering all six produces shallower, blended analysis.
- For Steps 2-6, keep the earlier steps' results in context (either the same
  conversation, or pasted in) so each step builds cumulatively on the last,
  rather than analyzing the video cold each time.
- Tell Gemini explicitly: *"Return the analysis in clean Markdown format. Do
  not wrap the entire response in a code block. Use clear Markdown headings,
  tables where useful, bullet lists, and timestamps."* Don't just ask it to
  "print as MD" and trust the formatting.
- Save each step's result as its own file, per reference video:

```
Reference_001/
├── reference-video.mp4
├── 01-story-structure.md
├── 02-scene-construction.md
├── 03-visual-filmmaking.md
├── 04-editing-strategy.md
├── 05-dialogue.md
└── 06-story-blueprint.md
```

`06-story-blueprint.md` is the file that matters most afterward - it's what
Phase B actually consumes. The other five are the supporting evidence,
useful when you need to reproduce the reference's visual language, pacing,
or dialogue mechanics specifically.

## The Story Blueprint Library

Steps 1-6 are a research asset; Steps 7-13 are a production asset. Do
Steps 1-6 once per reference and keep the resulting blueprint - don't redo
them for every new video made from it. Over time this becomes a library:

```
Story Blueprint Library/
├── Emotional Rescue.md
├── Betrayal to Revenge.md
├── Poor to Rich Transformation.md
├── Bully to Consequence.md
├── Mystery to Revelation.md
├── Underdog to Victory.md
└── Family to Emotional Reunion.md
```

Each new video picks a blueprint from the library, then runs Step 7 onward
with a genuinely different story on top of it. A useful reference-image
counterpart to this is a **master character library** - a locked, reusable
character description (e.g. "23-year-old woman, long black hair, red
jacket") that later stories can reference directly in Step 9 rather than
re-inventing a character sheet each time.

## Where the story actually changes

If your original video is a 20-year-old boy and your version needs a
23-year-old girl instead, that swap belongs in **Step 7 (Original Story
Adaptation)**, not earlier:

- Steps 1-5 stay an unmodified record of what's actually in the source video
  (so Step 1 still correctly says "protagonist: 20-year-old boy" - it's
  documenting the reference, not your story).
- Step 6 extracts the story-agnostic structure only (hook formula, conflict
  formula, escalation pattern, etc.) - never a copy of the specific
  characters, dialogue, or events, and never a rewritten "original example"
  either; that was tried and dropped as unnecessary since Step 7 already
  does exactly that job.
- Step 7 is where you deliberately swap in new characters, setting,
  conflict, events, dialogue, and ending, while keeping the underlying
  mechanics from Step 6's blueprint.
- The original character/story never needs to appear anywhere in the
  production assets (Steps 8-13) - only your new one does.

## Steps

1. [[projects/faceless-video-content/reverse-engineering-videos/step-01|Story Structure Analysis]] - Phase A
2. [[projects/faceless-video-content/reverse-engineering-videos/step-02|Scene Construction Analysis]] - Phase A
3. [[projects/faceless-video-content/reverse-engineering-videos/step-03|Visual Filmmaking Analysis]] - Phase A
4. [[projects/faceless-video-content/reverse-engineering-videos/step-04|Editing Strategy Analysis]] - Phase A
5. [[projects/faceless-video-content/reverse-engineering-videos/step-05|Dialogue Analysis]] - Phase A
6. [[projects/faceless-video-content/reverse-engineering-videos/step-06|Reusable Story Blueprint]] - Phase A, ends the reverse-engineering half
7. [[projects/faceless-video-content/reverse-engineering-videos/step-07|Original Story Adaptation]] - Phase B, where the new story is deliberately created
8. [[projects/faceless-video-content/reverse-engineering-videos/step-08|Production-Ready Recreation Plan]] - Phase B
9. [[projects/faceless-video-content/reverse-engineering-videos/step-09|Character Bible]] - Phase B
10. [[projects/faceless-video-content/reverse-engineering-videos/step-10|Environment / Location Bible]] - Phase B
11. [[projects/faceless-video-content/reverse-engineering-videos/step-11|Shot-by-Shot Image Prompts]] - Phase B
12. [[projects/faceless-video-content/reverse-engineering-videos/step-12|Shot-by-Shot Video Prompts]] - Phase B
13. [[projects/faceless-video-content/reverse-engineering-videos/step-13|Generate, Edit, Compare, Iterate]] - Phase B, ends the production half
