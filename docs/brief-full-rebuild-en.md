# Brief: Full Store Rebuild — Navigation, Shipping & Returns, Homepage

> **Note for Claude Code**: This is the single consolidated brief, superseding all prior separate briefs and the earlier "basic shipping" (Vietnam/US/Rest-of-World placeholder) instruction discussed in chat — do not use that older plan. Execute in this order: Part 1 (Navigation) → Part 2 (Shipping & Returns) → Part 3 (Product Images) → Part 4 (Product Card Styling) → Part 5 (Homepage Rebuild, 16 sections). All work happens on the "Dev - Main" (unpublished/draft) theme. Do NOT publish to live until the user explicitly confirms.

---

## Part 1: Navigation Menu

Build the main navigation menu. Since the store is going full multi-category "supermarket" from day one (Approach A), include all 8 Tier-1 categories instead of a narrower subset:

```
Skincare | Makeup | Haircare | Body Care | Fragrance | Tools & Devices | Wellness | Men's |
Shop By Concern ▾ (dropdown: Acne & Blemishes, Anti-Aging, Dark Spots, Dryness,
                   Sensitivity, Pores & Texture, Oiliness, Dullness, Puffiness) |
Bundles | New Arrivals | Gifting
```

This supersedes any narrower nav structure discussed earlier. Requires `write_online_store_navigation` scope (already added/installed by the user).

---

## Part 2: Shipping & Returns Overhaul

Requires `write_shipping` scope (already added/installed by the user).

### 2.1 Context

- Store ships to **US customers only** — no international shipping, no domestic Vietnam zone.
- Two fulfillment flows, both ending in US-based delivery:
  1. **Private Label / FBA items** (current roller product, future in-house SKUs) — fulfilled via **Amazon MCF (Multi-Channel Fulfillment)**. FBA inventory already exists and is ready to use now.
  2. **Dropship items** (future SKUs, testing market demand) — shipped from a China-based agent to a US intermediary warehouse, then to the customer. No agent/supplier chosen yet — this flow is a future placeholder, not operational today.

### 2.2 Shipping Profiles — Build (US only)

Do NOT build Vietnam or Rest-of-World zones. Build exactly:

| Fulfillment type | Checkout display name | Est. delivery | Rate |
|---|---|---|---|
| Private Label / FBA (current roller + future in-house SKUs) | **Standard US Shipping** | 3–5 business days | Free on orders over $75; $4.99 flat under $75 |
| Dropship (future SKUs only — not active yet) | **Standard Factory Direct Shipping** | 7–12 business days | Free for all orders |

- Only **one shipping zone: United States** (all 50 states + DC).
- Order processing time: **1–3 business days** (conservative placeholder — no real order data yet; revisit once orders are flowing).
- Accept P.O. Box and APO/FPO addresses, noting these may add 3–5 extra business days in transit.

### 2.3 Amazon MCF Integration

- Roller product's FBA inventory is confirmed ready for MCF now.
- Research and set up a Shopify-Amazon MCF connector app (verify what's currently available/well-reviewed on the App Store — don't assume a specific app name is still current).
- **Cannot be fully delegated**: connecting the app to the user's Amazon Seller Central account requires the user's own login/authentication. Install and configure what you can, then stop and clearly flag this step for the user to complete themselves.
- Once connected, roller orders placed on Shopify should route to Amazon MCF for pick/pack/ship automatically, using unbranded/neutral packaging.

### 2.4 Return & Refund Policy — Rebuild

Replace the currently-published Refund Policy. Core principles: no manipulative "return-deterrence" tactics of any kind (explicitly rejected — see below), transparent and fair, consistent with the existing "Keep the Item" clause for shipping-damaged low-value orders.

**Return windows (tiered by fulfillment type — deliberately shorter for dropship than a future supplier might allow):**
- Private Label / FBA items: **30-day return window**
- Dropship items (once any go live): **14-day return window** placeholder — before adding any dropship SKU, check that supplier's own return policy and set the window at least 3–5 days shorter than what they allow, for a safe processing buffer.

**Eligibility (Private Label / FBA items, standard "changed mind" returns):**
- Item unused, unworn, unwashed, original sealed packaging with tags/seals intact
- Proof of purchase (Order ID) required
- Non-returnable: opened/used items (unless defective/damaged on arrival), Final Sale/clearance items

**Cost allocation — no restocking fee, ever (0%):**
- **Changed mind / buyer's remorse**: customer pays return shipping; once received and verified sealed/unused, shop refunds 100% of item price. No restocking fee.
- **Damaged / defective / wrong item shipped**: zero-cost resolution — shop covers everything, customer does NOT ship the item back. Photos/video proof required (unboxing video), shop issues free replacement or full refund.
- **Low-value shipping-damage cases**: existing "Keep the Item" clause stays — immediate refund/replacement without return shipment, valid unboxing video is sufficient proof.

**Return address**: existing US Virtual Mailbox (Anytime Mailbox, Claymont DE — already configured). Do not reference or set up any new 3PL/warehouse address.

**Refund method**: original payment method, within 5–7 business days after the returned item is received and inspected.

**Return process**: customer emails hello@shopmiouvalab.com with Order ID + reason (+ photos/video if damage-related); support responds within 24–48 business hours.

**Explicitly rejected — do not implement under any circumstance**: tiered "resistance" email sequences, pressuring customers into partial refunds instead of honoring valid returns, blacklisting customers who request refunds, or any tactic designed to discourage/delay legitimate return requests. These carry FTC deceptive-practices exposure and increase chargeback risk rather than reducing it.

### 2.5 Shipping Policy — Rebuild

Replace the currently-published Shipping Policy (which incorrectly describes Vietnam-origin shipping) with content reflecting 2.2 above: US-only shipping, order processing time, the two fulfillment tiers with delivery estimates/rates, P.O. Box/APO-FPO handling, and tracking-number process (email notification once shipped, 24–48 hours for tracking to activate).

### 2.6 Summary of Policy Changes

| | Currently published (outdated) | New (this brief) |
|---|---|---|
| Shipping origin | Vietnam | US warehouse (Amazon MCF) for current product |
| Shipping zones | N/A | US only |
| Return window | 7 days | 30 days (Private Label/FBA) / 14 days (future dropship) |
| Restocking fee | None mentioned | Explicitly 0% |
| Return shipping cost (damage cases) | Not fully specified | Zero-cost to customer |
| Return address | Virtual Mailbox (unchanged) | Virtual Mailbox (unchanged) |

Update both the Shipping Policy and Refund Policy pages already live in Settings > Policies to match exactly, replacing outdated content rather than appending to it.

---

## Part 3: Fix Product Images

The user corrected the files in `assets/products/under-eye-roller-serum/` locally (the very first image was accidentally wrong and has been replaced with the correct file).

**Action**: Re-sync the product's images from the current contents of that folder. Keep the current first/hero image position, but replace all other image slots (position 2 onward) with the corrected files. If file order is ambiguous, list what's found and confirm mapping with the user before uploading.

---

## Part 4: Product Card & Product Page Typography

Current state: product title is faded/low-contrast, price is small and set below the title with little visual weight. Reference: al.ive body's product cards use a clear, confident title weight and a price with equal or near-equal visual weight to the title, positioned directly under it with tight spacing.

**Action**:
- Increase product title font-weight/contrast on product cards and the product detail page.
- Increase price font size — it should read as a confident, readable price, not a caption.
- Reduce vertical gap between title and price so they read as one grouped unit.
- Apply globally via the theme's product card block settings/CSS so it applies automatically as more SKUs are added.

---

## Part 5: Homepage Rebuild (16 sections, al.ive body structure)

Context: the user is going full dropship — new SKUs will be added continuously. The homepage should be built out fully now to look like a complete multi-category beauty store, even though only 1 SKU is live today. Structure below is based on al.ive body's homepage, section by section, top to bottom.

For each section: build now if content is available; if content is genuinely missing (no reviews yet, no blog posts yet, no press mentions yet), build the section's structure/placeholder and flag it clearly rather than skipping it silently — the user decides whether to hide it until content exists or fill it with interim content.

### 5.1 Rotating announcement bar (top strip)
Two rotating messages — e.g. shipping-threshold promo ("Free US shipping over $75" — matches Part 2's real threshold) and a second placeholder brand message. **Needs user input** for the second message.

### 5.2 Utility nav row (secondary, above main nav)
Build only what applies now: About Us, Blog, Contact Us (skip Find a Stockist / Giving Back — not applicable). Flag if this requires custom Liquid beyond standard Horizon blocks.

### 5.3 Main navigation
Covered in Part 1 — already includes logo + full primary menu. Skip any "quiz"-style CTA pill unless the user confirms wanting a placeholder (e.g. "Take the Skin Quiz") for future use.

### 5.4 Hero banner with CTA
Replace the default illustration with a real lifestyle/product image once available; update CTA to point to `tools-devices` or `best-sellers` collection instead of generic "Shop all." **Needs user input**: hero image (can reuse one of the uploaded product images if no separate lifestyle image exists).

### 5.5 Promotional collection banner (e.g. "The Bundle Sale")
Not applicable yet — no bundles exist. Skip for now; leave the `bundles` collection functional for later use.

### 5.6 Product carousel/grid with pricing
Featured collection section already exists showing the live product with price; apply Part 4's typography fix here. Will grow naturally as more SKUs are added.

### 5.7 Category tiles with photos ("Objects for everyday living" equivalent)
Collection List section showing image tiles for all 8 Tier-1 categories (per Approach A — show all now, even empty ones, with a generic placeholder/brand-color tile image rather than leaving them blank or broken-looking).

### 5.8 Small category icon row
Map to the Tier-3 format collections: Bundles, Refills, Gifting, New Arrivals, Best Sellers. Build as a smaller row beneath 5.7, or merge into one section if that fits the theme's available blocks better — flag the choice made.

### 5.9 "Shop By Concern" circular showcase
Repurpose al.ive's scent-showcase pattern: circular thumbnails for the 9 concern collections (Acne & Blemishes, Anti-Aging, Dark Spots, Dryness, Sensitivity, Pores & Texture, Oiliness, Dullness, Puffiness), each linking to its collection.

### 5.10 Testimonials / reviews
No reviews exist yet (no orders placed). **Do not fabricate reviews.** Build the section structure/placeholder only, flag that it needs a reviews app (Judge.me or Loox) installed and populated once real orders/reviews exist. Leave hidden or with a "Be the first to review" placeholder.

### 5.11 "A message from our founders"
Rich text + image section. **Needs user input**: founder statement copy and a photo (or brand image if no founder photo is desired). Do not fabricate a founder quote — leave as a placeholder block with instructions until real copy is provided.

### 5.12 Newsletter signup
Use Horizon's built-in Newsletter section with MiouvaLab branding (e.g. "Get MiouvaLab updates").

### 5.13 Blog articles section
No blog posts exist yet. Build the section structure, but either hide it or populate with 1-2 real placeholder posts. **Needs user input**: write blog content now, or keep hidden until content exists?

### 5.14 Certifications / claims icon row
**Needs user input — do not assume any claims**: which of these actually apply to MiouvaLab (cruelty-free? vegan? made in Vietnam or elsewhere? any giving-back program?). Only build claims the user confirms are true — unverified claims here are a compliance risk, same as the ad-copy rules already established for product descriptions.

### 5.15 "As seen & featured in" press logos
No press mentions exist yet. **Skip entirely for now** — do not fabricate press logos or media mentions.

### 5.16 Rich footer
- Logo + short brand blurb (2-3 sentences, dermatologist-professional tone, consistent with existing product copy)
- Quick links: Contact Us, Shipping Policy, Terms of Service, Privacy Policy, Refund Policy (all 4 already published), Help Centre (can link to Contact for now)
- Skip links to features that don't exist: Gift Cards, Wholesale Login, Corporate Portal, Become a Stockist, Find a Stockist
- Contact info: hello@shopmiouvalab.com, and confirm with the user whether the business address (5900 Balcones Drive STE 100, Austin, TX 78731) should display publicly here, or email-only
- Social media icons: **needs user input** — does MiouvaLab have live Instagram/TikTok/Facebook accounts to link? Do not link to placeholder or non-existent profiles.
- Copyright line: "© 2026, MiouvaLab."

---

---

## Critical Technical Addendum (apply throughout Part 4 and Part 5)

### A. Color Schemes — Root Cause of the "colored in editor, white on live" issue

Horizon (like Dawn) uses a **Color Scheme system**: background colors aren't set once globally — each individual section must have a Color Scheme explicitly assigned to it (Scheme 1, Scheme 2, etc. under Theme Settings > Colors). A section left on "Default" will render white/blank regardless of what looks correct in a color picker elsewhere.

**Action**:
- No brand color palette has been finalized yet for MiouvaLab. Do NOT hardcode arbitrary hex values. Instead, propose 2-3 color schemes (e.g. a light neutral/cream background scheme and a darker accent scheme) that complement the existing black-and-white script logo, and present them to the user for approval before applying broadly.
- Once approved, explicitly assign a Color Scheme to every one of the 16 homepage sections in Part 5 — none should be left on an unset/default white scheme.
- **Persistence method**: continue using the same reliable CLI-based approach already established for this project (editing `config/settings_data.json` and section JSON directly, then `shopify theme push`) rather than relying on clicking "Save" in the browser theme editor — that UI was already found to be unreliable earlier in this project (unsaved-state bugs, iframe issues). Verify persistence via re-pull, as done previously.

### B. Product Card Typography — specific values

Refine Part 4 with concrete targets:
- Product title: font-weight 600–700, high contrast (dark, near-black on light backgrounds).
- Price: font size equal to or larger than the title, not a small caption.
- Title-to-price vertical gap: 4px or less, so they read as one tight grouped unit.
- Apply via global theme/CSS settings, not per-product overrides, so every future SKU (including dropship additions) automatically inherits this styling with zero manual per-product styling work.

### C. Dropship Scaling Readiness

Confirm the "Standard Factory Direct Shipping" rate (Part 2.2) is configured as a reusable global rule on the US shipping zone — not a one-off — so it's ready to attach to new dropship products as they're added, without reconfiguring shipping each time.

### D. Preview Before Publish

Before asking the user to review progress, save/push all changes and share the Dev-Main theme preview link so the user can verify actual rendered colors/typography — not just a description of what was configured.

---

## Summary of All Items Needing User Input Before Full Completion

1. Second announcement bar message
2. Hero banner image
3. Placeholder tile images for empty Tier-1 categories (or confirm generic brand-color tiles are fine)
4. Founder statement copy + photo/image
5. Blog: write real content now, or hide section until later?
6. Which product claims are actually true (cruelty-free, vegan, origin, etc.)
7. Business address: OK to display in footer, or email-only?
8. Live social media accounts to link (if any)
9. Optional: "Skin Quiz" CTA pill in nav — build now or skip?

Do not guess on any of the 9 items above — ask the user directly for each before building that specific piece, but proceed with everything else that doesn't depend on these answers.
