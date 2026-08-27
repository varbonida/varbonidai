---
type: project
tags: [kelly, schengen-calculator, travel, research]
created: 2026-08-20
updated: 2026-08-27
status: paused
aliases: [Schengen Calculator, Schengen 90/180 calculator]
---

# Schengen Calculator

Canonical page for Kelly's Schengen 90/180 calculator. Client: [[clients/kelly/overview|Kelly]].

**Paused since 2026-08-20**, when Kelly narrowed scope to the
[[clients/kelly/dictation-app/overview|Avelisse Dictation App]] only. Research is
complete; nothing has been built. Personally relevant to her: she was under real
Schengen-exit deadline pressure on 2026-08-26.

## 📊 Status

- **Current Phase:** Research → Scoping
- **Research:** ✅ Complete
- **Platform Decision:** ⏳ Not yet decided (web / native mobile / both)
- **Next Action:** Define MVP feature scope and pick tech stack

---

## 🔍 Research — ✅ Done

### 📜 The Rule (core logic)

- **90 days max within any rolling 180-day period**, for non-EU/EEA short-stay travelers.
- Window is calculated by counting back 180 days **from each day of the stay** — not a fixed calendar block.
- Both entry day and exit day count as full days in Schengen.
- Leaving Schengen briefly does **not** reset the count — days only fall off as the 180-day window rolls forward.
- People holding an **EU residence permit or long-stay visa** are NOT subject to this rule — decide whether to exclude or flag this group.
- **Official reference tool:** [EU Short-Stay Calculator](https://home-affairs.ec.europa.eu/policies/schengen/border-crossing/short-stay-calculator_en) — ground truth to validate our math against.

### 🗺️ Schengen Membership (29 countries, as of 2026)

- 25 EU member states + 4 non-EU (Iceland, Norway, Switzerland, Liechtenstein).
- **Bulgaria & Romania** — full members since 1 Jan 2025 (air/sea since 31 Mar 2024). Older sources often have this wrong.
- **Cyprus** — EU member, NOT Schengen (accession pending, no firm date).
- **Ireland** — EU member, permanent Schengen opt-out.
- ⚠️ Don't hardcode the list — build as an editable config; membership will keep changing (Cyprus, future candidates).

### 🛂 Entry/Exit System (EES) — context that changes the pitch

- Fully operational at all external borders as of **10 April 2026**.
- Digitally/biometrically tracks entries & exits and auto-calculates 90/180-day usage — governments now do this automatically.
- Rollout has been rocky (2–5 hr border queues at peak) → travelers are anxious right now, good timing for a clear planning tool.
- **ETIAS** (pre-travel authorization for visa-exempt travelers) launching end of 2026 — natural future feature/content extension.
- **Positioning shift:** app is less "avoid getting caught," more "plan proactively, avoid surprises before you travel."

### 🏁 Competitive Landscape

|Tool|Notable angle|
|---|---|
|EU official calculator|Accurate, but doesn't save trips between sessions|
|schengenclock.com|Privacy angle — "data never leaves your browser"|
|schengen90.app|Calendar-first visual UX|
|90 Days in Europe|PDF export, family tracking, paid tiers|
|Entorii|Free for first 3 trips, no ads, PDF border reports, future-trip simulation|

**Takeaway:** the calculator math is a commodity — everyone claims EU-calculator parity. Differentiation = UX (calendar-first vs. form-first), trust signals (privacy, cite EU source), or an underserved niche.

### 🎯 Underserved Angles / Differentiation Ideas

- [ ] Digital nomads / second-home owners with long historical trip records (competitor apps reportedly break on this)
- [ ] Post-Brexit UK travelers as an explicit niche
- [ ] Combined EES + ETIAS plain-English guidance bundled with the calculator (timely, people are confused right now)
- [ ] Border-ready PDF/export of trip history

### 💰 Monetization Patterns Observed

- Free with trip-count cap → paid unlocks unlimited trips (e.g., 3 free trips)
- Fully free, ad-supported
- Donation button (organic user requests)
- Premium bundle: unlimited trips + PDF export + multi-profile/family tracking + push notifications near limit

---

## 🧮 Core Algorithm — Requirements

- [ ] Pure function: given trip list + reference date → days used in trailing 180-day window
- [ ] Pure function: given trip list → days remaining as of today
- [ ] Pure function: given trip list → next date eligible to re-enter / regain days
- [ ] Support "planning mode" — simulate a future trip against existing history
- [ ] Handle overlapping trips (e.g., resident country + other Schengen travel same day)
- [ ] Handle long historical date ranges (multi-year lookback)
- [ ] Unit test suite: leap years, window-boundary trips, back-to-back trips, single-day trips
- [ ] Validate output against EU official calculator on real scenarios

---

## 🛠️ MVP Feature Scope

### Must-have

- [ ] Add/edit/delete trips (entry date, exit date, country optional)
- [ ] Days used in last 180 days (as of today)
- [ ] Days remaining
- [ ] Next eligible re-entry date
- [ ] Simple visual (calendar heatmap or timeline bar)
- [ ] Legal disclaimer ("not legal/immigration advice")

### Nice-to-have (post-MVP)

- [ ] Future trip planning / "what if" simulation
- [ ] Notifications before hitting the limit
- [ ] Multi-user / family profiles
- [ ] PDF export for border control
- [ ] Offline support
- [ ] EES/ETIAS explainer content

---

# 🎨 Build Workflow

## 1. Platform & Stack

- [ ] Decide platform: web-only / native mobile / both (React Native or Flutter)
- [ ] Set up project repo
- [ ] Choose hosting/deployment target (Vercel/Netlify/Cloudflare Pages for web)

## 2. Core Engine

- [ ] Build date-calculation engine (see Core Algorithm above)
- [ ] Write full unit test suite before touching UI

## 3. UI/UX

- [ ] Wireframe core flow: add trips → see result
- [ ] Build trip input UI
- [ ] Build results visualization (calendar/timeline)
- [ ] Build "days remaining" and "next eligible date" summary view

## 4. Data & Persistence

- [ ] Local/device storage for trip data
- [ ] Decide if cloud sync / accounts are in scope (adds GDPR overhead — avoid for MVP if possible)

## 5. Legal & Compliance

- [ ] Add "not legal/immigration advice" disclaimer
- [ ] Privacy policy (especially if storing personal data — trip dates = personal data under GDPR)
- [ ] Keep data on-device where possible to minimize GDPR scope
- [ ] Check app store policies if monetizing via ads/IAP in a travel-advice-adjacent app

## 6. Testing

- [ ] Unit tests on algorithm (priority over UI tests)
- [ ] Manual verification against EU official calculator
- [ ] Beta test with real frequent Schengen travelers

## 7. Distribution

- [ ] Web: deploy + domain + basic SEO ("schengen calculator" is high-intent search)
- [ ] iOS: App Store listing, screenshots, ASO keywords
- [ ] Android: Google Play listing, screenshots, ASO keywords
- [ ] Marketing: travel blogs, r/digitalnomad, r/expats, SEO content on 90/180 rule + EES/ETIAS
- [ ] Analytics setup (privacy-respecting, e.g., Plausible)

---

# ⚠️ Important Decisions

- [ ] Confirm platform (web / mobile / both)
- [ ] Confirm tech stack
- [ ] Confirm brand name, logo, visual identity
- [ ] Confirm monetization model (free / freemium / ads / donation)
- [ ] Confirm data storage approach (on-device only vs. cloud sync)
- [ ] Confirm scope: pure calculator vs. calculator + planner vs. calculator + EES/ETIAS content hub
- [ ] Confirm distribution priority (web first vs. mobile first)

---

## 📓 Early Scratch Notes

*Moved from `Dictation App/rebranding.md` on 2026-08-22, where it had been misfiled. Undated in the original — likely predates the 2026-08-20 research below.*

```
shengen calculator
may 13
28 of july

went aug 3rd
came back 10th

research shengen
how do i make it accurate
```

---

# 📝 Updates

### 2026-08-20

- Completed research: 90/180 rule mechanics, Schengen membership list, EES rollout context, competitive landscape, differentiation angles, monetization patterns.
- Identified key differentiation opportunity: UX (calendar-first) + trust signals + EES/ETIAS timing, since core math is a commodity across competitors.
- Next focus: define MVP scope and select platform/tech stack.
