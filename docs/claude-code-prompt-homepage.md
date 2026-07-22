# Project Context — Skincare Shopify Store

## Stack
- Shopify theme: Dawn (OS 2.0), customized via Liquid sections
- Do NOT edit Dawn's core files directly — create new files in `sections/`, `snippets/`, `blocks/`
- Version control: GitHub, this repo
- Local dev: Shopify CLI (zsh, Mac)

## Design tokens (locked — never change without explicit approval)
- Background (porcelain): `#F5F0E8`
- Card background: `#EDE7DD`
- Text: `#2B2419`
- Accent (sage green): `#7C8B6F`
- Accent (dark brown): `#3D2B1F`
- Heading font: Lora (Google Fonts, serif)
- Body font: Manrope (Google Fonts, sans-serif)
- Define as CSS variables once in `snippets/theme-variables.liquid`, import everywhere else.

## Data architecture (Formula Dossier)
- Metaobject `ingredient`: name, function, safety_rating, source_description
- Metaobject `product_ingredient_entry`: ingredient reference + per-product concentration
- Product Metafield: list-of-references to `product_ingredient_entry`
- This solves the many-to-many relationship where concentration varies per product
  but ingredient info is reused across products.

## Working agreement
- Rachel owns: Admin UI actions, Metaobject data entry, review/approval of design decisions
- Claude Code owns: writing Liquid/CSS/JSON, implementing sections
- After each section is built, STOP and wait for review before moving to the next one
- No jQuery. Vanilla JS only, following Dawn's custom-element pattern (e.g. `product-form.js`)
- Mobile-first, main breakpoint 750px (Dawn convention)
- All new sections need full `{% schema %}` so settings are editable in theme editor —
  never hardcode text/images that should be editable

## Copyright boundary
- Never reproduce pixel-exact layouts or copy from competitor/paid themes
- Describing layout structure in words for fresh implementation is fine
- Colors and Google Fonts have no copyright concern

## Build phases (in order)
1. Design System (fonts, colors, spacing — done)
2. Hero Section
3. Trust Bar
4. Metaobject data entry (Rachel, in Admin UI)
5. Formula Dossier Section
6. Bestsellers Section
7. Extended homepage sections (promo banner, cart drawer restyle, testimonials,
   category circles, founder story, newsletter, trust badges, footer)
8. Polish / responsive pass
9. Publish
