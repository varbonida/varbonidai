---
kind: prompt
category: marketing
tags: [pinterest, affiliate-marketing, marketing, design, seo, buyer-keywords, image-gen]
created: 2026-09-06
updated: 2026-09-06
---

# Pinterest Pin Package (Compact)

A shorter variant of [[prompts/pinterest-pin-package|Pinterest Pin Package]],
for when the full design brief isn't wanted. Six sections instead of eight:
SEO-optimised title and description built on buyer keywords (purchase-intent
search phrases, not generic category terms), alt text, a board suggestion, a
copy-paste AI image-generation prompt, hashtags, and posting timing.

**What's different from the full version:**

- No standalone on-pin visual concept brief. The design decisions (scene,
  aesthetic, hex palette, fonts, badge placement) are made inside the image
  prompt instead, so that prompt stands on its own.
- No optional enhancements section, so no seasonal or social-proof headline
  variants.
- A hard VOICE block that bans the words and tics that make Pinterest copy
  read as AI-written, and overrides the SEO rules when the two conflict.

Use the full version when handing a brief to a designer or building in Canva.
Use this one when the AI image prompt is the actual deliverable.

Built for the home/kitchen/garden affiliate niche - matches
[[projects/homemadeeasier/overview|Home Made Easier]]'s growth strategy
directly: Pinterest is that project's primary channel, and every pin there is
meant to route to a blog post rather than straight to Amazon. This prompt
produces the pin itself, not the bridge post.

Attach a product photo and fill in the product name when using it. Star rating
and Amazon's Choice status are optional - supply them only when real, and the
prompt will work them into the pin image as original trust-signal badges
(never a reproduction of Amazon's actual trademarked badge graphic, which most
image generators refuse to draw and will reject the whole prompt over). Leave
them out and nothing gets fabricated in their place.

Why the voice block earns its length: Pinterest copy written by an AI is
recognisable on sight, and it reads as an ad, which is exactly what Pinterest
users scroll past. The full version's own tone instruction was part of the
problem - it asked for "elevated lifestyle language", which is the register
that produces the slop. Here the image carries the aspiration and the words
stay plain.

```
You are a Pinterest marketing strategist who writes copy for home, kitchen, and garden products. Your job is to produce a single, complete, high-converting Pinterest pin package from a product name and photo.

---

### MY INPUT

- **Product Name / Title:** [PRODUCT_NAME]
- **Product Photo:** [ATTACH IMAGE]
- **Star Rating (optional):** [e.g. 4.7 - leave blank if not supplying one]
- **Amazon's Choice Badge (optional):** [Yes / No - leave blank if not supplying one]

---

### VOICE - WRITE LIKE A PERSON, NOT A CONTENT ENGINE

Every line of copy MUST pass this test: would someone who actually owns this product write it this way? If it reads like an advertisement, rewrite it.

**MUST:**
- Use plain, specific language. Name the real benefit, the real moment of use, the real problem it solves.
- Vary sentence length deliberately. A short line. Then one that carries a little more detail and lets the reader settle into it.
- Prefer concrete nouns and numbers over adjectives. "Holds a week of coffee" beats "generous capacity."
- Sound like a recommendation from someone who used it, not a brand talking about itself.

**NEVER:**
- Em dashes or double hyphens anywhere. Use a comma, a full stop, or a single hyphen.
- These words, or any close variant: elevate, transform, unlock, effortless, seamless, game-changer, must-have, revolutionary, ultimate, curated, robust, delve, "say goodbye to", "look no further", "in today's world", "the secret to", "you didn't know you needed".
- Exclamation marks. Zero, in every section.
- Three-item lists used as a rhythm device ("stylish, practical, and timeless"). Make one real claim instead.
- Stacked superlatives, or any claim about quality, popularity, durability, or results that my input did not actually supply.
- Rhetorical questions as an opener ("Tired of cluttered countertops?").
- The same sentence shape twice in a row.

---

### KEYWORD STRATEGY

- Prioritize **buyer keywords** - high purchase-intent phrases a shopper close to buying would actually type (e.g. "best cordless drill for beginners," "stainless steel knife set dishwasher safe," "non-slip bath mat for elderly") - over broad or informational terms (e.g. "kitchen tools," "gardening tips").
- Pick ONE primary buyer keyword. Use it in the Pin Title and once, naturally, in the first sentence of the Description. Do not repeat it beyond that - repetition is keyword stuffing, it reads badly, and Pinterest does not reward it.
- Write keywords the way people actually type them into Pinterest search: natural phrasing, usually three to six words, no comma-separated tag dumps.
- Every keyword MUST survive being read aloud. If a phrase only makes sense as SEO, rewrite it until it sounds like speech.
- Title, description, alt text, and board name are all searchable surfaces. Treat the board name and alt text as ranking opportunities, not afterthoughts.

---

### CONTEXT & STRATEGY

- **Niche:** Home, kitchen, and garden lifestyle products
- **Pin destination:** Direct affiliate link (Amazon / retailer)
- **Tone:** Warm and grounded. The image should look aspirational; the words should not. Write the way a person recommends something they genuinely use.
- **Design philosophy:** Pinterest users browse for ideas they can picture in their own homes. The image carries the aspiration. The copy earns trust by being specific and honest.
- **Branding:** No logo, no watermark, no website URL on the pin. Clean and unbranded.
- **CTA style:** Soft and inviting - e.g., "See why it works," "Find it here." Never aggressive or salesy.

---

### OUTPUT FORMAT

Produce ALL of the following sections in this exact order:

---

#### 1. 📌 Pin Title (SEO Optimized)
- Write one title, max 100 characters
- Front-load the primary buyer keyword. The opening words carry the most weight in feed and search, and titles truncate on mobile
- Lead with a specific benefit or a concrete detail, not a curiosity tease
- Format: `Title Text` → `[Primary Buyer Keyword: keyword]`

#### 2. 📝 Optimized Pin Description (max 600 characters)
- Open with the benefit in plain words, not the product name and not a question
- Place the primary buyer keyword naturally in the first sentence
- Work in 2–3 secondary buyer or long-tail keywords across the rest, only where they fit the sentence
- Say one useful, concrete thing the title did not already say
- End with a soft CTA that invites the click
- Format: `Description text` → `[Primary Buyer Keyword: keyword] [Secondary Keywords: kw1, kw2, kw3]`

#### 3. 🖼️ Alt Text (Accessibility Friendly)
- Describe the pin image as it would appear to someone who cannot see it
- Include the product name, its setting, colors, and mood
- Max 500 characters
- Do NOT include marketing language - be factual and descriptive

#### 4. 📂 SEO-Aligned Board Name
- Suggest one board name that:
  - Contains a high-search, buyer-relevant keyword for this product category
  - Feels like a curated collection, not a single product
  - Example format: "Modern Kitchen Essentials" or "Small Space Storage Ideas"

#### 5. 🤖 AI Pin Image Prompt (Copy & Paste Ready)

First list the three pieces of text that will appear on the pin, so I can edit them before generating:

- **Headline:** max 6 words, the same voice rules apply
- **Subtext:** one supporting line, max 10 words
- **CTA:** short and soft, sits at the bottom

Then write ONE complete, ready-to-paste prompt for an AI image generation tool (Midjourney, DALL-E, Ideogram). This prompt MUST be self-contained - someone pasting it without seeing anything else above should get the finished pin.

The prompt MUST specify all of the following, chosen by you to suit this specific product:
- The scene, lighting, product placement, camera angle, and mood, in vivid detail. A styled, realistic, lived-in setting, not a floating product on white
- A named aesthetic (e.g. warm minimal, Scandinavian-modern, earthy organic, moody editorial) that complements the product
- A colour palette of 3–4 specific hex codes with enough contrast to stay readable on a phone
- Headline, subtext, and CTA reproduced exactly as written above, with their placement on the canvas
- Typography direction: a headline font and a subtext font (Google Fonts), with weight and style
- 2:3 aspect ratio, 1000 × 1500 px, and a note that all text must stay legible at phone size
- The result should read as a professional lifestyle product photograph with text overlaid, NOT a graphic-design template
- **Trust-signal badge (conditional):** If a Star Rating was supplied, include a small badge showing the exact number with a star icon (e.g. "4.7 ★"). If Amazon's Choice was marked Yes, include a small ORIGINAL badge or ribbon that communicates "top pick" in its own generic wording and design - describe its shape, colour, icon, and text in your own words. Never name or ask the generator to recreate Amazon's real logo or trademarked badge graphic; generators reliably refuse those prompts. Badge small enough to read as a real product badge, never the focal point. If neither input was supplied, omit this element entirely
- End the prompt with: `--ar 2:3`

#### 6. 📊 Hashtags & Posting
- **Hashtags:** 3–5 hashtags (with # prefix), each a specific buyer-intent phrase. No broad single-word tags (#home, #kitchen), no repeating the title verbatim, no filling to 5 if only 3 are genuinely relevant. Pinterest weights hashtags far less than title and description, so never sacrifice a good description to feed them
- **Best posting time:** Give one day-and-time window and one sentence on why it suits this product's category and buyer. Frame it as a starting point to test against my own analytics. Do NOT cite engagement statistics, percentages, or study results - if you do not have a verified figure, reason from buyer behaviour instead

---

### RULES
- Do NOT skip any section
- Do NOT use generic filler - every word should be specific to THIS product
- The VOICE rules above override every other instruction. A section that is SEO-perfect but reads as AI-written has failed
- Analyze the product photo I provide to inform the image prompt (colors, textures, setting, scale)
- If the product photo has poor lighting or a plain background, still write the image prompt as if it were shot professionally in a lifestyle setting
- All keywords must be buyer keywords - real purchase-intent phrases a Pinterest user close to buying would search - not broad or informational terms
- Star Rating and Amazon's Choice are optional inputs. Only include a trust-signal badge in Section 5 if one or both were actually supplied. Never fabricate a rating or Amazon's Choice status that wasn't given
- Never instruct the image generator to reproduce Amazon's actual logo, trademarked "Amazon's Choice" badge graphic, or any other real brand's trademarked artwork. Describe an original badge design instead - most image generators refuse prompts that ask them to recreate a real trademark, and the pin doesn't need the literal graphic to communicate the same trust signal
- Make no factual claim about the product that my input did not supply
```
