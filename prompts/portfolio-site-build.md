---
kind: prompt
category: coding
tags: [nextjs, tailwind, portfolio, frontend]
created: 2026-08-26
updated: 2026-08-27
---

# Portfolio Site Build

Scaffolds a Next.js + Tailwind portfolio site with Automations and Projects
sections plus detail pages, Framer Motion, and an Impeccable design-approval
checkpoint. Requires a `design.md` at the project root, which it treats as the
binding source of truth for every visual decision.

Run [[prompts/design-system-doc|Design System Doc]] first if `design.md` does
not exist yet.

```Build my personal portfolio website in this repo. `design.md` at the project root already defines the design system (dark/light theme via `[data-theme]`, color tokens, Inter for body, Montserrat bold for headers, type scale) — treat it as the binding style source of truth for every visual decision.

<context>
Project root: `C:\Users\Vergel\Documents\development\portfolio\varbonida`. Currently empty except `design.md`. No Next.js project has been scaffolded yet. No pnpm/yarn installed — use npm.
</context>

<content>
No real copy/project data exists yet. Use clearly-labeled placeholder content everywhere (bios, descriptions, images as labeled placeholder blocks) — structure it so swapping in real content later is a data-only change, not a component rewrite. Generate 6 placeholder items each for Projects and Automations.
</content>

<structure>
Single scrolling home page, section order: Hero, Automations (top 3 preview), Projects (top 3 preview), Stack, Experience, Contact. Resume download button (Hero or Contact).

Additional routes:
- `/automations` — full list of all automation items (same card as home preview)
- `/automations/[slug]` — detail page per automation
- `/projects` — full list of all project items (same card as home preview)
- `/projects/[slug]` — detail page per project

Home's "Automations" and "Projects" sections each have a "View all" link to their respective listing route.
</structure>

<data_shape>
Shared summary card (used on home preview + listing pages): title, short description, tags, thumbnail, external link (live/repo).

Automation detail page: Problem, Solution, Workflow Architecture (supports both an image AND an embedded/self-hosted video — build the media slot to accept either), Results/what it solves.

Project detail page: extended description, single hero image that expands to the full screenshot in a lightbox/modal on click (build the modal with Framer Motion — do not add a lightbox library).

Define all placeholder data in one local data file per type (e.g. `lib/data/projects.ts`, `lib/data/automations.ts`) that home, listing, and detail pages all read from — do not duplicate content inline per page. Use `generateStaticParams` for the `[slug]` routes.
</data_shape>

<resume>
Wire the resume download button to `/resume.pdf` in the `public/` folder. Do not generate a placeholder PDF — the user will drop their real file in at that path themselves after this build.
</resume>

<task>
1. Invoke the `impeccable:impeccable` skill first to make the visual/UX design decisions (layout, hierarchy, spacing, motion direction) for the home page and the listing/detail page templates. Present the resulting design direction and stop — wait for explicit approval before writing any component code.
2. Once approved, scaffold a Next.js (App Router, latest stable) + Tailwind CSS (latest stable) project via npm.
3. Wire `design.md`'s tokens into Tailwind: define the CSS custom properties from `design.md` in `globals.css` under `[data-theme="dark"]` / `[data-theme="light"]`, and reference them from Tailwind's theme config rather than hardcoding hex values anywhere in components.
4. Load Inter and Montserrat via `next/font/google` per `design.md`'s Typography section (Inter for body, Montserrat 700/800 for headers only).
5. Build all sections/routes above as components, with Framer Motion entrance/scroll animations — subtle and purposeful, not decorative for its own sake.
6. Use `react-icons` for the Stack section's technology logos — this is the one approved exception to the dependency list below.
7. Implement a dark/light theme toggle that switches the `data-theme` attribute on `<html>`, persists the choice (localStorage), and defaults to the user's OS preference on first load.
8. Ensure responsive layout at minimum for mobile (375px) and desktop (1440px) widths.
</task>

<constraints>
- Every color used in any component MUST resolve to a `design.md` custom property — no new hex values, including hover/focus/disabled states.
- Do not use any font other than Inter and Montserrat.
- Do not add authentication, a CMS, a database, analytics, or contact-form backend — the contact section is static (links/mailto only).
- Dependencies limited to: Next.js, Tailwind CSS, Framer Motion, react-icons, and their direct peers. No other UI kit (no shadcn/MUI/Chakra), no lightbox/carousel/video-player library — build the image lightbox and video slot yourself with Framer Motion and native HTML.
- Do not deviate from the section/route structure above without flagging it first.
</constraints>

<forbidden_actions>
- Do not deploy or configure any hosting/CI.
- Do not commit or push.
- Do not delete or overwrite `design.md`.
- Do not generate or fetch a placeholder resume PDF.
</forbidden_actions>

Stop and ask before: adding any dependency not listed above, changing the section/route structure, or introducing any color/font outside `design.md`'s tokens.

<output_format>
Step 1 output: the impeccable design direction, then wait for approval.
After implementation, output:
✅ Project scaffolded — [list of files/components/routes created]
Then run the build check (`npm run build`) and report pass/fail with the actual output, not an assumption.
</output_format>
```
