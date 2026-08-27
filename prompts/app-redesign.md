---
kind: prompt
category: design
tags: [design, mobile, ui, redesign]
created: 2026-08-22
updated: 2026-08-27
---

# App Redesign

Redesigns an existing mobile app UI from screenshots of the current app plus a
colour palette image as the exact colour source. Produces high-fidelity screens
that hold together as one design system rather than isolated mockups.

Attach the screenshots and the palette image when using it.

```Redesign my existing mobile app using the attached screenshots as the current
reference and the attached color palette image as the exact color source.

APP CONTEXT
App name: [your app name]
App category: [e.g. fitness tracker, food delivery, finance, social]
Primary user goal: [e.g. log a workout, track expenses, order food]
Screens attached: [list the screens, e.g. Home, Profile, Onboarding, Checkout]

OBJECTIVE
Redesign each attached screen with a modern, cohesive visual language while
preserving the existing information architecture, navigation structure, and
core user flows. Do not remove or reorder functional elements — elevate the
visual execution, hierarchy, and polish.

COLOR SYSTEM: "Mediterranean Coastal Serenity"
Use the attached color palette as the exact source of truth for hex values.
The palette should read as calm, sun-washed, and coastal — think whitewashed
walls, sea-glass blues/teals, warm terracotta or sand accents, and a muted
olive or sage green, all sitting on soft neutral off-white backgrounds.

Apply the palette using this structure:
- Base color: the primary Mediterranean Coastal Serenity tone from the
  attached palette — use for primary buttons, active states, key icons,
  and selected navigation items.
- Tint (lighter derivative, ~20–30% white mixed in): use for hover/pressed
  backgrounds, secondary buttons, card backgrounds, subtle highlights, and
  disabled-state fills.
- Shade (darker derivative, ~20–30% black mixed in): use for pressed/active
  button states, text on light backgrounds where contrast is needed, borders,
  and depth cues like shadows on colored surfaces.
- Maintain WCAG AA contrast (4.5:1 minimum) for all text against its
  background, adjusting tint/shade usage as needed without deviating from
  the base hues.
- Neutrals: pair the palette with warm off-white/sand neutrals for
  backgrounds, and a soft charcoal (not pure black) for body text.

DESIGN REQUIREMENTS
- Typography: establish a clear type scale (display, heading, body, caption)
  with consistent weight and line-height across all screens.
- Spacing: use a consistent 8px-based spacing system for padding, margins,
  and component gaps.
- Components: restyle buttons, cards, input fields, nav bars, and icons to
  match the coastal palette while keeping touch targets accessible (min 44px).
- Iconography: use simple, rounded, line-based icons that feel airy and
  match the coastal mood — avoid heavy or sharp shapes.
- Imagery/illustration accents (if any): favor soft gradients or light
  textures evoking water, sand, or linen rather than saturated blocks of color.
- States: show clear default, hover/pressed, active, and disabled states for
  interactive elements using the base/tint/shade system above.

OUTPUT
Generate high-fidelity redesigns for each attached screen, keeping them
visually consistent as a single design system rather than isolated screens.
```