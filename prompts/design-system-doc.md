---
kind: prompt
category: design
tags: [design, design-system, tokens, documentation]
created: 2026-08-26
updated: 2026-08-27
---

# Design System Doc

Generates a docs-only `design.md` at a project root: colour tokens, light and
dark theming via `[data-theme]`, and typography. Documentation only, it is told
explicitly not to scaffold or modify any other file.

Pairs with [[prompts/portfolio-site-build|Portfolio Site Build]], which treats
the resulting `design.md` as its binding style source.

```Create a new file `design.md` at the project root documenting this project's design system as a reference doc for future UI work. Do not touch, scaffold, or modify any other file.

<context>
This is a solo portfolio project. The repo is currently empty — no code, no framework, no existing CSS setup. design.md does not exist yet and there is no prior design token file to reconcile against — write these values as the source of truth. This is documentation-only: no CSS file, no framework config, no implementation code. Keep everything framework-agnostic (raw CSS custom properties) since the eventual build stack (plain CSS, Tailwind, etc.) is not yet decided.
</context>

<task>
Write design.md with these exact sections, in this order:

1. **Overview** — 1-2 sentences: this file is the single source of truth for color tokens and typography, implemented as CSS custom properties switched via a `[data-theme]` attribute on a root element (e.g. `<html data-theme="dark">` / `<html data-theme="light">`).

2. **Color Tokens** — a fenced `css` code block defining both themes exactly as given, no substitutions, no added/removed tokens:

```css
[data-theme="dark"] {
  --background: #0F172A; /* Dark Navy */
  --primary:    #22D3EE; /* Neon Cyan */
  --secondary:  #64748B; /* Cool Gray */
  --accent:     #F4F4F4; /* Light Gray */
}

[data-theme="light"] {
  --background: #F8FAFC; /* Off-White */
  --primary:    #0891B2; /* Deep Cyan */
  --secondary:  #475569; /* Slate Gray */
  --accent:     #0F172A; /* Dark Navy */
}
```

3. **Accent Role Flip** — immediately after the color block, a small 2-row table making this unmissable:

| Theme | `--accent` resolves to |
|---|---|
| Dark  | `#F4F4F4` (Light Gray) |
| Light | `#0F172A` (Dark Navy) |

Follow the table with one sentence: `--accent` is not a fixed color — components must reference the custom property, never hardcode either hex value assuming one direction.

4. **Usage Guidance** — a short table or bullet list mapping each token to where it belongs: `--background` (page/surface background), `--primary` (CTAs, links, active/interactive states, focus rings), `--secondary` (muted text, borders, disabled states, secondary UI chrome), `--accent` (see table above — text on inverse surfaces / high-contrast highlights). Include one line flagging: verify contrast before using `--primary` (`#22D3EE` on `#0F172A`, `#0891B2` on `#F8FAFC`) for small text or icons — do not use it for body copy.

5. **Typography** — Google Fonts imports for Inter (body/UI text, weights 400/500/600) and Montserrat (headers only, weights 700/800 — bold only, do not use Montserrat below weight 700). Include the `@import` or `<link>` snippet for both families and a font-family custom property pair: `--font-body: 'Inter', sans-serif;` and `--font-heading: 'Montserrat', sans-serif;`.

6. **Type Scale** — a minimal table for headers (h1–h4) and body text: sizes, line-heights, and which font-weight from Montserrat's bold range each heading level uses. One table, no more than 6 rows.

7. **Theme Switching Note** — one paragraph explaining that theme switching is done by toggling the `data-theme` attribute value on the root element, not by media query, and that components must reference the CSS custom properties only, never hardcode a hex value.
</task>

<constraints>
- Use the hex values and comments exactly as given above — do not alter, "improve," or re-balance any color.
- Do not invent additional tokens (no `--danger`, `--success`, `--border`, etc.) — only the four tokens per theme given.
- Do not create, edit, or scaffold any other file (no actual CSS file, no HTML demo, no package.json changes, no framework config) — design.md is a documentation-only deliverable.
- Do not add a full accessibility audit or color-theory rationale section — the contrast flag in section 4 is a single line, not a separate section.
- Keep the whole file under ~130 lines.
</constraints>

<forbidden_actions>
- Do not install any dependency or run any package manager command.
- Do not modify any existing file in the repo.
- Do not commit or push anything.
</forbidden_actions>

Stop and ask before creating design.md in any location other than the project root, and before adding any section not listed above.

<output_format>
After writing the file, output:
✅ Created design.md at [path]
Then show the final file's section headers only (not the full content) as a checklist confirming all 7 sections are present.
</output_format>
```
