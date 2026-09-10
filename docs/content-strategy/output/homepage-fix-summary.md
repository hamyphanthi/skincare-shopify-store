# Homepage fix — 1-SKU catalog

**Date:** 2026-09-10
**Scope:** remove placeholder-driven homepage sections and replace them with content that fits a single-product catalog.
**Files changed:** `templates/index.json`, `sections/collection-list.liquid`
**Design tokens:** untouched. No new colour or font values were introduced.

---

## 1. What was rendering the placeholders

Everything on the homepage is configured in `templates/index.json` — there are no bespoke
homepage section files. The three problem areas mapped to:

| Problem area | Section key in `templates/index.json` | Rendered by |
|---|---|---|
| Shop by Category (8 tiles) | `cl_categories` | `sections/collection-list.liquid` |
| Shop by Concern (9 circles) | `cl_concerns` | `sections/collection-list.liquid` |
| News / blog (dummy posts) | `blog` | `sections/featured-blog-posts.liquid` |
| Bestsellers grid (1 card in a 4-col grid) | `product_list_fa6P9H` | `sections/product-list.liquid` |

## 2. Collection data (verified against the live storefront, not assumed)

`GET /collections.json` on `cxkf3z-je.myshopify.com`:

- **Categories — 1 of 8 has a product.** `tools-devices` = 1. `skincare`, `makeup`,
  `haircare`, `body-care`, `fragrance`, `wellness`, `mens` = 0.
- **Concerns — 5 of 9 have a product.** `concern-anti-aging`, `concern-dark-spots`,
  `concern-dryness`, `concern-puffiness`, `concern-sensitivity` = 1 each.
  `concern-acne-blemishes`, `concern-dullness`, `concern-oiliness`,
  `concern-pores-texture` = 0.
- Also empty: `bundles`, `gifting`, `new-arrivals`, `refills`, `frontpage`.

So filtering by product count would have collapsed the category grid to a **single tile**,
which reads worse than removing it. That is why the categories grid was removed rather than
filtered.

## 3. Research

### Structural patterns in premium DTC beauty with a tiny catalogue

- **[Vintner's Daughter](https://www.vintnersdaughter.com/)** — ran a single SKU for five
  years ([Beauty Independent](https://www.beautyindependent.com/vintners-daughter-active-botanical-serum/),
  [Glossy](https://www.glossy.co/podcasts/vintners-daughter-founder-april-gargiulo-skincare/)).
  Its homepage today: hero → product showcase → performance/benefits → founder philosophy →
  proprietary-process deep-dive → press → values badges → newsletter.
  **No "shop by category" grid, no "shop by concern" grid, no blog feed.**
- **[Dieux](https://dieuxskin.com/)** — products → bundles → community favourites →
  before/after UGC → five brand principles → press → Instagram → email. Category and
  concern navigation lives in the **nav menu**, not as a homepage grid. No blog feed on the
  homepage.
- **[Shopify's single-product roundup](https://www.shopify.com/blog/single-product-website)** —
  the recurring sections across single-product sites are: hero, benefits, video/photo
  demonstration of use, before/after, comparison, FAQ, brand story, subscription.

The consistent pattern: a small catalogue does not pad the homepage with navigation, it
replaces navigation with **substance about the one product** — how it is made, how it is
used, what is in it, who made it.

### Does under-eye care skew gift or routine? (US)

**Routine/replenishment, with gifting as a seasonal secondary.**

- [ShelfTrend's under-eye category analysis](https://www.shelftrend.com/health-beauty/under-eye-care-market-analysis-seller-profit-guide)
  states routine replenishment drives primary demand, on a ~90-day repurchase cycle driven
  by product depletion, and puts November–December at 22% of annual volume as gifting and
  self-purchase rise together. It also lists a puffiness-focused buyer persona at a
  $22–$48 price band — the roller serum sits in that band at $39.99.
- **Caveat, stated explicitly:** I could not find category-specific gift-share data for
  eye care from a primary or independently audited source. The
  [Retention Side beauty report](https://retentionside.com/industry-reports/beauty-and-skincare-retention-report-2026-benchmarks-buying-cycles-and-customer-trends)
  gives skincare repeat-purchase benchmarks (25–40% average, 40–55%+ for strong brands) but
  contains **no eye-care data and no gifting data at all**. ShelfTrend is a seller-tools
  content site, not an audited research house — treat its 22% figure as directional.

**Applied to the homepage:** the framing is routine/self-care ("How to use it — three steps,
morning and night"), not gift-ready. A gift/bundle angle is a Q4 seasonal addition, not the
base frame.

## 4. What changed

### Removed
- `cl_categories` — the 8-tile category grid. 7 of 8 tiles were empty.
- `cl_concerns` — the 9-circle concern grid.
- `blog` — the News feed. It was rendering Shopify's onboarding placeholders ("Title",
  "An excerpt of your blog post's content"). Neither reference brand carries a homepage blog
  feed; the blog itself is untouched and still linked from the header and footer.
- `product_list_fa6P9H` — the "Bestsellers" 4-column grid holding one card.

### Added
- **`spotlight`** — single-product spotlight. Product image left, accent heading
  "One product. Used every day.", two paragraphs stating the catalogue is deliberately one
  product, the price, and a primary CTA to the PDP. Structure mirrors the existing `founder`
  section.

  The price is a `custom-liquid` block reading the live product object:
  `all_products['miouvalab-under-eye-roller-serum'].price | money`. It is never hardcoded, so
  a price change in Admin flows straight through. It is emitted with the theme's own
  `text-block h4` classes, so it inherits the locked typography tokens — no new CSS, no
  inline styles.
- **`howto`** — "How to use it": three numbered steps (chill / roll outward / let it settle).
  This is the routine framing the category data supports, and the "photo guide to using it"
  pattern from the Shopify roundup.
- **`targets`** — "What it targets": the five concerns the product genuinely addresses, each
  with its actives and benefit. This replaces the concern grid with the same information in
  a form that does not dead-end into five collections that all contain the same one product.
  Claim wording is lifted from the live product description, which is already written to the
  Meta/TikTok compliance rules in `docs/brief-shopify-store-setup-en.md`.

### New homepage order
`hero` → `spotlight` → `howto` → `targets` → `testi_head` → `testi_marquee` → `founder` → `newsletter`

### `sections/collection-list.liquid` — empty-collection guard
Yes, hiding zero-product collections is possible from Liquid, and it is now implemented:
the item loop skips any collection where `all_products_count == 0`, the carousel slide count
follows the number of cards that actually rendered, and the list is not rendered at all if
nothing survives. The guard only applies when collections were picked in the theme editor,
so Horizon's onboarding placeholder path is unaffected. This makes any future category or
concern grid self-hiding as the catalogue fills in.

## 5. Verification

- `shopify theme check` — 330 files, 0 offenses.
- Pushed to the unpublished **Dev - Main** theme (`#144351199298`) and rendered at 1440px
  and at a narrow viewport. All three new sections render, stack correctly on mobile, and no
  placeholder text remains on the homepage.
- One defect was caught and fixed during verification: the first spotlight build used
  Horizon's `featured-product` section, whose media block requires a merchant-picked image
  and was falling back to Shopify's placeholder t-shirt illustration. It was rebuilt as an
  image + copy + CTA section using the real product photo.

## 6. Your tasks in Shopify Admin

1. **Header menu still lists the empty categories.** The nav shows Skincare, Makeup,
   Haircare, Body Care, Fragrance, Wellness, Men's, Bundles, New Arrivals, Gifting — all
   with zero products. Removing the grid from the homepage does not touch the menu.
   Trim it under *Online Store → Navigation* to what actually has stock.
2. **The product is not in the `skincare` collection.** It sits in `tools-devices` only.
   You are holding this one until the nav trim is done — left as-is, nothing changed.
3. **The founder portrait is a blank placeholder.** `miouvalab-founder2.png` in *Content →
   Files* is an empty porcelain rectangle with a hairline border, so the founder section
   renders an empty box. Upload the real photo **under the same filename** and no code
   change is needed.
4. **The product shows "Sold out" on the live theme.** Check inventory / "continue selling
   when out of stock" under the product's variant settings.
5. **Local asset folders break `theme push`.** `assets/products/` and `assets/branding/` are
   rejected by Shopify (subfolders are not allowed in `assets/`, and several filenames
   contain spaces and Vietnamese diacritics). They are untracked in git. Move them outside
   the theme directory or add them to `.gitignore` — every push currently reports errors for
   them. I did not move or delete anything.

## 7. Open items for you

- Copy in the three new sections is a first draft written from your existing brief and
  product description. Review the wording before this goes to traffic.
- Decisions you confirmed this session: no "coming soon" teaser, News section removed
  outright, no email popup (inline signup only), Bestsellers grid reframed as a spotlight,
  price shown from live product data.
- One token note, flagged rather than changed: `type_size_h5` is 14px, the same size as
  `type_size_paragraph`, so the h5 preset is indistinguishable from body copy. The price uses
  h4 (24px) as a result. Not touched — your call if you ever want h5 to sit between the two.
