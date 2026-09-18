# Brief: Full Shopify Store Setup — MiouvaLab

> **Note for Claude Code**: Execution brief for the current dev store (`cxkf3z-je.myshopify.com`, Horizon theme). This is a full multi-category beauty store (Approach A: build the complete framework upfront, including empty categories to be filled as new SKUs launch). Execute sections 3→7 in order. Anywhere marked `[NEEDS CONFIRMATION]` must be checked with the user before execution.

---

## 1. Context

- Store is a **full multi-category beauty "supermarket"** (Sephora/Ulta/Cult Beauty model), not a single-product or single-niche store.
- Strategy confirmed: **Approach A** — build the entire category/collection framework now, even though most categories are currently empty. Only "Tools & Devices" has a real product today. Other categories will be populated as new SKUs (via in-house production or dropshipping) launch.
- First live product: **MiouvaLab Under Eye Roller Serum** — medical-grade steel roller head (refrigeratable) combined with active serum formulation. Lives under `Tools & Devices`.
- Content tone: **Dermatologist / professional** — clinical, trustworthy language, avoid overly emotional Gen-Z style copy.
- Ad platforms: Meta (Facebook/Instagram) + TikTok → content must follow compliance rules (see Section 6).
- Brand name: **CONFIRMED as "MiouvaLab"**. Domain: user plans to register something like `miouvalab[XXXX].com` (exact string TBD, not yet purchased).

---

## 2. Full Collection & Navigation Architecture

### Tier 1 — Main Categories (top nav, product-type based)

| Handle | Display Name | Status | Notes |
|---|---|---|---|
| `skincare` | Skincare | Empty for now | Cleanser, Toner, Serum, Moisturizer, Mask, SPF — sub-collections to add per future SKU |
| `makeup` | Makeup | Empty for now | Face, Eyes, Lips, Brushes & Tools |
| `haircare` | Haircare | Empty for now | Shampoo, Conditioner, Treatment, Styling Tools |
| `body-care` | Body Care | Empty for now | Body Wash, Lotion, Scrub, Body Tools |
| `fragrance` | Fragrance | Empty for now | Perfume, Body Mist |
| `tools-devices` | Tools & Devices | **LIVE** | Roller, LED devices, Gua sha, cleansing brushes — home of the current product |
| `wellness` | Wellness | Empty for now | Ingestible beauty, supplements |
| `mens` | Men's | Empty for now | Men's grooming line |

### Tier 2 — Shop By Concern (cross-cutting, needs-based — the primary ad-landing layer)

| Handle | Display Name | Status |
|---|---|---|
| `concern-acne-blemishes` | Acne & Blemishes | Empty for now |
| `concern-anti-aging` | Anti-Aging & Fine Lines | **LIVE** — current product assigned here (USP3) |
| `concern-dark-spots` | Dark Spots & Uneven Tone | **LIVE** — current product assigned here (USP1) |
| `concern-dryness` | Dryness & Dehydration | **LIVE** — current product assigned here (USP4) |
| `concern-sensitivity` | Sensitivity & Redness | **LIVE** — current product assigned here (USP5) |
| `concern-pores-texture` | Pores & Texture | Empty for now |
| `concern-oiliness` | Oiliness & Shine Control | Empty for now |
| `concern-dullness` | Dullness & Brightening | Empty for now |
| `concern-puffiness` | Puffiness & Under-Eye | **LIVE** — current product assigned here (USP2) |

> Rationale: each future ad creative (organized by USP/concern) should deep-link directly to its matching concern collection instead of the homepage, to maximize ad-to-landing-page relevance and conversion rate.

### Tier 3 — Commercial Format Collections

| Handle | Display Name | Status |
|---|---|---|
| `bundles` | Bundles | Empty — activate once ≥2 SKUs exist |
| `refills` | Refills | Empty — activate once refillable SKUs exist |
| `gifting` | Gifting | Empty for now, structure ready (Gifts Under $30/$50/$100, By Occasion) |
| `new-arrivals` | New Arrivals | Manual, update per new SKU launch |
| `best-sellers` | Best Sellers | Auto-collection by sales |

### Current Product Assignment
`MiouvaLab Under Eye Roller Serum` → `tools-devices` + `concern-anti-aging` + `concern-dark-spots` + `concern-dryness` + `concern-sensitivity` + `concern-puffiness` + `best-sellers`

### Navigation Menu Structure (top nav)
`Skincare | Makeup | Haircare | Body Care | Tools & Devices | Shop By Concern (dropdown, 9 items) | Bundles | New Arrivals | Gifting`

Menu visibility: **confirmed — show all categories now**, including empty ones, per Approach A "supermarket" positioning.

---

## 3. Store Rename & Basic Branding

- Settings > General > Store name: change "My Store" → **MiouvaLab** (confirmed, execute now)
- Store contact email: **hello@shopmiouvalab.com** (confirmed)
- Business address: **[NEEDS CONFIRMATION]** — not yet provided
- Logo + favicon: ready on user's side, to be provided directly to Claude Code (file paths/upload)

---

## 4. First Product: Under Eye Roller Serum

**Delete the "Test Serum" placeholder product before adding the real one.**

### Product Title
`MiouvaLab Under Eye Roller Serum`

### Short Description (product card)
An under-eye care device combining a refrigeratable, medical-grade stainless steel roller head with a concentrated active serum, designed to help address visible signs of eye-area fatigue.

### Full Description (product page — dermatologist tone)

> MiouvaLab Under Eye Roller Serum pairs a medical-grade stainless steel roller head with a multi-active serum formulation, designed to help address multiple signs of eye-area fatigue and aging at once — from dark circles and puffiness to fine lines and dryness.
>
> The roller head can be chilled before use, supporting an instant cooling sensation and helping skin appear more toned. The accompanying serum contains actives studied for their effects on skin, paired with gentle massage motion to support absorption.
>
> **Note**: This product is designed to help improve the visible appearance of skin and is not a substitute for medical treatment. Patch-test recommended before full-face use if you have sensitive skin.

### 5 USP Blocks (bullet points on product page — map directly to concern collections above)

1. **Dark circle reduction** (→ `concern-dark-spots`) — Niacinamide + Tranexamic Acid: helps improve the appearance of pigmentation under the eyes, supporting a brighter, more even-toned look.
2. **Puffiness reduction & instant cooling** (→ `concern-puffiness`) — Caffeine + chilled steel roller: helps reduce the appearance of swelling, delivering an instant tightening sensation.
3. **Anti-aging support** (→ `concern-anti-aging`) — Palmitoyl Tripeptide-1, Palmitoyl Tetrapeptide-7, Adenosine: helps support skin elasticity and reduce the visible appearance of fine lines.
4. **Deep hydration** (→ `concern-dryness`) — Dual-molecular-weight Hyaluronic Acid + Betaine + Panthenol: helps deliver multi-layer hydration for softer, smoother-feeling skin.
5. **Gentle & safe for sensitive skin** (→ `concern-sensitivity`) — Allantoin, Camellia Sinensis (Green Tea) Extract, Panthenol, Tocopherol: helps soothe skin and reduce the appearance of irritation.

⚠️ **Mandatory compliance** (Meta/TikTok ads): NEVER use "cures," "eliminates completely," "treats" in a medical-device sense, or "lifts" as a medical claim. Only use "helps improve," "visible reduction," "skin feels firmer/softer."

### Price
**$39.99 USD** (confirmed)

### Product Images
User has real product photos + logo/favicon ready — **to be provided directly to Claude Code separately** (not attached in this brief). Claude Code should prompt for file paths/uploads when executing this step.

---

## 5. Technical Setup Checklist (execute via Shopify Admin/API)

- [ ] Rename store to "MiouvaLab"
- [ ] Delete "Test Serum" product
- [ ] Create all Tier 1 category collections (8 total, most empty)
- [ ] Create all Tier 2 concern collections (9 total)
- [ ] Create all Tier 3 format collections (5 total, most empty)
- [ ] Build navigation menu per Section 2 structure
- [ ] Create Under Eye Roller Serum product, assign to `tools-devices` + 5 relevant concern collections + `best-sellers` (blocked on price + images)
- [ ] Configure Settings > Shipping: domestic (Vietnam) + basic international shipping zones, placeholder fee
- [ ] Configure Settings > Payments: **CANNOT be automated** — user must personally register Stripe/PayPal
- [ ] Create legal pages (Section 6)

---

## 6. Legal Pages (Settings > Policies)

1. **Privacy Policy**
2. **Terms of Service**
3. **Refund Policy** (confirmed, full text below)
4. **Shipping Policy** — estimated delivery time, fees; ships from Vietnam (see Section 8 for fulfillment/returns operations)

### Full Refund Policy Text (confirmed)

**1. Return Window**
- Customers may request a return or exchange within **7 days** from the date the order status is updated to "Delivered" by the shipping carrier.
- Requests submitted after this window will not be accepted.

**2. Product Condition Requirements**
For Cosmetics & Skincare items, returned products must meet all of the following:
- **Unopened condition**: original shrink wrap, security seal, labels, and packaging fully intact. No sign of opening or trial use of any kind.
- **Proof of purchase**: valid e-receipt or Order ID on the Shopify system.
- **Unboxing video**: customer must provide a clear video of the full unboxing process showing the shipping label and the condition of the item inside, to ensure transparency.

**3. Cases Eligible for Return (100% free return shipping)**
- Product physically damaged during shipping (broken, leaked, cracked, pump/nozzle broken).
- Wrong item, wrong color, wrong volume, or missing quantity vs. the original order.
- Manufacturer defect (e.g. missing label, non-functioning pump/nozzle even with seal intact).

**4. Cases NOT Eligible for Return**
- Product has been unsealed, opened, scratched, or trial-used in any way (including sample testing of texture/scent).
- Change of mind (dislike scent, dislike color) after correct and complete delivery.
- Damage caused by improper storage by the customer (e.g. exposure to high heat causing melting/degradation).
- Fixed non-returnable items: minisize/sample products, free gifts, clearance/Final Sale items.

**5. Resolution Methods & Costs**
- **Exchange**: shop resends the correct item at no cost if the fault is shop/carrier's; if exchanging by customer preference (product still sealed), customer covers round-trip shipping.
- **Refund**: returned to original payment method within 5-7 business days after the shop receives and inspects the returned item.
- **Store credit**: a discount code equal to the returned product's value, for use on a future order.

**6. 3-Step Return Request Process**
- Step 1: Email **hello@shopmiouvalab.com** or message via the website support page with: Order ID + reason for return + supporting video/photos.
- Step 2: Customer support reviews and responds with a resolution within 24-48 business hours.
- Step 3: Once approved, customer carefully packages the item to avoid damage and ships it to the shop's return address as instructed.

**Additional clause — "Keep the Item" (confirmed):** For low-value orders damaged in transit, the shop may issue an immediate refund or replacement without requiring the customer to ship the damaged item back — a valid unboxing video is sufficient proof. This reduces return shipping/handling costs and improves customer goodwill for minor-value shipping damage cases.

---

## 7. Fulfillment & Returns Operations (confirmed)

- **Outbound shipping**: no US warehouse at this stage. All new orders (cosmetics/roller) ship directly from Vietnam to US customers via international shipping routes.
- **Return address**: **CONFIRMED.**
  ```
  2803 Philadelphia Pike, Suite B #1838
  Claymont, DE 19703
  United States
  ```
  A US Virtual Mailbox (Anytime Mailbox, Claymont, DE location) will be used as the single Return Address for three purposes: (1) printed on the Shipping/Return Policy page, (2) entered as the Return Address in Pirate Ship, (3) entered as the Ship From/Return Address in USPS label configuration. **This replaces the LLC registered agent address (5900 Balcones Drive) for return/shipping purposes** — the LLC address remains valid only for Terms of Service / legal registration purposes (Section 3).
  - ⚠️ **Go-live gate**: USPS Form 1583 has been submitted but not yet approved by USPS as of this brief. The address exists and can be published now, but the mailbox **cannot actually receive mail/packages until Form 1583 is approved** (typically a few hours to 1-2 business days). Claude Code should publish this address in the Shipping/Return Policy now, but the user must confirm 1583 approval before accepting live orders/returns.
- **Return handling process** (manual, current stage):
  1. Customer requests return within the 7-day window, provides Order ID + reason + unboxing video via email to hello@shopmiouvalab.com.
  2. If approved, shop manually purchases a USPS label via Pirate Ship (customer's address → Virtual Mailbox address) and emails the PDF label to the customer.
  3. Customer ships the item to the Virtual Mailbox address.
  4. Virtual Mailbox service photographs the received package and notifies the shop.
     - **Damaged/defective items**: instruct Discard on the spot.
     - **Intact items** (change-of-mind, still sealed): held at the Virtual Mailbox, batched and either shipped back to Vietnam once enough volume accumulates, or forwarded to a new US customer if a matching SKU order comes in.
- **Automation threshold**: this manual Pirate Ship process is used for the current stage. Once monthly order volume exceeds **~20 orders/month**, revisit installing a returns automation app (AfterShip Returns / Richpanel) — note these apps only automate label generation and approval workflow; they do **not** provide their own warehouse network. The Virtual Mailbox address continues to serve as the warehouse location entered into the app.

---

## 8. Cannot Be Delegated to Claude Code (user must do personally)

- Register payment gateway (Stripe/PayPal)
- Purchase custom domain
- Upgrade to paid Shopify plan
- Confirm USPS Form 1583 approval before accepting live orders (currently pending)
- Hand off product photos/logo/favicon files directly (paths or uploads)

---

## Status: Brief Complete

All decision items are now confirmed. Remaining open action (not a Claude Code task): user to confirm USPS Form 1583 approval status before the store goes fully live for order fulfillment. Everything else in this brief — brand name, collection architecture, product content, pricing, refund policy, and return address — is finalized and ready for execution.
