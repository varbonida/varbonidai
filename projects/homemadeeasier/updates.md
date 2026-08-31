---
kind: changelog
project: homemadeeasier
tags: [homemadeeasier, astro, changelog]
created: 2026-08-28
updated: 2026-08-28
---

# Home Made Easier - Updates

Progress log for `development/portfolio/homemadeeasier`. See
[[projects/homemadeeasier/overview|Home Made Easier]] for stack, monetisation,
and open items.

---

## 📝 Updates

### 2026-08-28

- Added to the vault. Repo already had Astro 7 + Tailwind v4 scaffolded, one
  live post (kitchen shears, kettle, thermometer), and an affiliate disclosure
  component in place.
- Resolved a GitLab merge conflict in `README.md` and pushed; repo is back in
  sync with the GitLab remote.
- Ran a full design pass: chose "The Exposed Binding" (coptic bookbinding /
  chain-stitch) as the visual direction, and built the whole site around it -
  sidebar nav, post cards, a key-rail of facts, a verdict stamp, the affiliate
  disclosure. `PRODUCT.md` and `DESIGN.md` now document the product and the
  shipped system. This supersedes the "sage/warm-neutral palette" direction
  named in the original planning conversation - that one was never built.
- Caught and fixed a real layout bug after that pass looked finished: the
  sidebar was pinned to the true viewport edge, so on an actual desktop
  monitor the content floated in a huge dead void - it had only been tested at
  1440px and on mobile before. Worth remembering for future screenshot checks
  on this project.
- Next focus: set the real domain in `astro.config.mjs`, confirm Amazon
  Associates status, replace the placeholder hero image, write the 9 remaining
  posts needed for Amazon approval.
