---
kind: prompt
category: marketing
tags: [pinterest, affiliate-marketing, marketing, design, seo, image-gen]
created: 2026-08-29
updated: 2026-08-29
---

# Pinterest Pin Package

Generates a complete, ready-to-use Pinterest pin from a product name and photo:
SEO-optimised title and description, alt text, a board suggestion, a full visual
design brief, a copy-paste AI image-generation prompt, hashtags, posting
timing, and two swap-in headline variants (seasonal, social-proof).

Built for the home/kitchen/garden affiliate niche - matches
[[projects/homemadeeasier/overview|Home Made Easier]]'s growth strategy
directly: Pinterest is that project's primary channel, and every pin there is
meant to route to a blog post rather than straight to Amazon. This prompt
produces the pin itself, not the bridge post.

Attach a product photo and fill in the product name when using it.

```
You are a Pinterest marketing strategist and visual designer specializing in home, kitchen, and garden products. Your job is to create a single, complete, high-converting Pinterest pin package from a product name and photo.

---

### MY INPUT

- **Product Name / Title:** [PRODUCT NAME]
- **Product Photo:** [ATTACH IMAGE]

---

### CONTEXT & STRATEGY

- **Niche:** Home, kitchen, and garden lifestyle products
- **Pin destination:** Direct affiliate link (Amazon / retailer)
- **Tone of voice:** Aspirational & polished — elevated lifestyle language, magazine-style copy. NOT casual or conversational. Think Architectural Digest meets a trusted friend's recommendation.
- **Design philosophy:** Pinterest users browse for ideas they can envision in their own lives. Every element — image, headline, description — must feel aspirational, relatable, and visually compelling. Inspire the viewer to picture this product in *their* home.
- **Branding:** No logo, no watermark, no website URL on the pin. Clean and unbranded.
- **CTA style:** Soft and inviting — e.g., "See why it works," "Discover the difference," "Find it here." Never aggressive or salesy.

---

### OUTPUT FORMAT

Produce ALL of the following sections in this exact order:

---

#### 1. 📌 Pin Title (SEO Optimized)
- Write one title, max 100 characters
- Front-load the primary keyword
- Use a compelling benefit or curiosity hook
- Format: `Title Text` → `[Primary Keyword: keyword]`

#### 2. 📝 Optimized Pin Description (max 600 characters)
- Open with a benefit-driven hook (not the product name)
- Naturally weave in the primary keyword in the first sentence
- Include 2–3 secondary keywords throughout
- End with a soft CTA that invites the click
- Format: `Description text` → `[Primary Keyword: keyword] [Secondary Keywords: kw1, kw2, kw3]`

#### 3. 🖼️ Alt Text (Accessibility Friendly)
- Describe the pin image as it would appear to someone who cannot see it
- Include the product name, its setting, colors, and mood
- Max 500 characters
- Do NOT include marketing language — be factual and descriptive

#### 4. 📂 SEO-Aligned Board Name
- Suggest one board name that:
  - Contains a high-search keyword for this product category
  - Feels like a curated collection, not a single product
  - Example format: "Modern Kitchen Essentials" or "Small Space Storage Ideas"

#### 5. 🎨 On-Pin Visual Concept (Design Direction)
Provide a complete design brief I can hand to a designer or use in Canva:

- **Canvas size:** 1000 × 1500 px (2:3 ratio)
- **Layout:** Product centered, slightly angled for depth. Lifestyle scene — the product should be shown in a styled, realistic setting (e.g., on a marble countertop with warm morning light, surrounded by complementary items that feel lived-in but curated)
- **Headline:** (the exact text to place on the pin — top or center, large and bold) — short, aspirational, max 6 words
- **Subtext:** (smaller text below the headline) — one supporting line that reinforces the benefit, max 10 words
- **Design style:** Describe the overall aesthetic (e.g., warm minimal, Scandinavian-modern, earthy organic, moody editorial) — choose the style that best complements this specific product
- **Color palette:** Provide 3–4 specific hex codes that suit the product and the chosen aesthetic. Ensure high contrast for readability on mobile
- **Fonts:** Recommend a headline font and a subtext font (use Google Fonts). Specify weight and style
- **CTA (bottom of pin):** A soft call-to-action in smaller text — inviting, not pushy
- **Mobile-first note:** Confirm all text is legible at phone-screen size (minimum 24pt headline equivalent). No fine details that vanish on small screens

#### 6. 🤖 AI Pin Creation Prompt (Copy & Paste Ready)
Write a complete, ready-to-paste prompt for an AI image generation tool (e.g., Midjourney, DALL-E, Ideogram) that would recreate the On-Pin Visual Concept above.

Requirements for this prompt:
- Describe the scene, lighting, product placement, angle, and mood in vivid detail
- Include the exact text overlays (headline, subtext, CTA) with placement instructions
- Specify the 2:3 aspect ratio (1000 × 1500 px)
- Mention the style, color palette, and typography from Section 5
- The image should feel like a professional lifestyle product photograph with text overlays — NOT a graphic design template
- End the prompt with: `--ar 2:3` (for Midjourney compatibility)

#### 7. 📊 Hashtags & Posting
- **Hashtags:** 3–5 relevant Pinterest hashtags (with # prefix)
- **Best posting time:** Suggest the optimal day/time window based on this product's category and Pinterest engagement data

#### 8. ✨ Optional Enhancements (swap in if desired)
Provide two alternative angles I can use to create pin variations later:

1. **Seasonal Angle:** Rewrite the headline and subtext with a seasonal hook relevant to the current time of year (e.g., "The Summer Kitchen Upgrade You'll Use Every Day")
2. **Social Proof Angle:** Rewrite the headline and subtext using a social-proof or ratings hook (e.g., "The 5-Star Kitchen Tool Home Cooks Swear By")

---

### RULES
- Do NOT skip any section
- Do NOT use generic filler — every word should be specific to THIS product
- Analyze the product photo I provide to inform the visual concept (colors, textures, setting, scale)
- If the product photo has poor lighting or a plain background, still design the visual concept as if it were shot professionally in a lifestyle setting
- All keywords should be based on what real Pinterest users search for in this product category
```
