# Bayong Gracia — Online Shop (Design Handoff)

E-commerce site for **Bayong Gracia**, a handicraft bag business in Paniqui, Tarlac, Philippines.
- Founded in 2018 by Honey Tess B. Alcantara.
- Sells hand-woven, hand-painted bags made with local weavers and artists.
- Site copy is in **Filipino (Tagalog)**.

## About these files
`Bayong Gracia Site.dc.html` is a **high-fidelity, fully clickable HTML prototype**. It is the design reference, not production code.

**Task:** rebuild it as a real site, following the visuals, copy and behavior exactly. Recommended stack: **Next.js (App Router) + Tailwind**, with product data in a local JSON/TS file first and a commerce backend later.

How the prototype file is put together:
- It uses a small runtime (`support.js`).
- Markup uses `{{ }}` holes, `<sc-for>` loops and `<sc-if>` conditionals.
- All logic and data live in the `<script data-dc-script>` block at the bottom: `PRODUCTS`, `HELP`, `DETAILS`, `FILTERS` and the state handlers.

To preview it locally, run any static server in this folder (e.g. `npx serve`) and open the `.dc.html` file.

## Pages / routes
| Route | Content |
|---|---|
| `/` | Hero (photo with swaying brand tag), 3 pillars, "Mga paborito" grid (4), founder story band, custom CTA |
| `/koleksyon` | Title + count, filter chips (Lahat, Rosas, Abo, Itim, Kayumanggi, Berde, Puti, Lila, Bago), sort (Itinatampok, Pinakabago, Presyo ↑/↓), product grid |
| `/koleksyon?f=bago` | The same page with the "Bago" filter; this is the "Bago" link in the header |
| `/bayong/[slug]` | Breadcrumb, gallery, product info, founder quote band, "Baka magustuhan mo rin" (4 items, same color first) |
| `/kuwento` | Founder story, milestones (2018, bazaars, social media, DTI Negosyo Center), 4 values, CTAs |
| `/custom` | 3 steps, gallery, custom request form (name, contact, base color, idea), success state |
| `/tulong` | FAQ accordion: Shipping, Bayad, Returns, Pag-aalaga, Custom |
| `/account` | Login form; when logged in, shows greeting and order list |
| `/checkout` | Shipping form + payment (GCash / Maya / COD) + sticky order summary |
| `/salamat` | Order confirmation: number, total, payment method |

**Product page details**
- The gallery has 4 views (Buong bag, Detalye ng pinta, Hawakan, Habi). Each view is a crop of the same photo, made with object-position plus scale.
- Info column, in order: tag, label, name, price, description, design swatches, size (LAKI), quantity, "Idagdag sa bayong" button, and an accordion.

**Global UI**
- Announcement marquee at the very top.
- Sticky header:
  - Nav on the left: Koleksyon, Bago, Custom na pinta, Kuwento.
  - Logo in the center.
  - On the right: Hanapin, Account, and **Bayong (n)** in bold maroon.
- Banig strip under the header.
- Cart drawer slides in from the right. It has items, quantity steppers, a free-shipping notice, a "banig na kahon" gift box option (+₱150) and the totals.
- Search overlay drops from the top and shows results live as you type.
- "Added to cart" toast at the bottom center.
- Footer: logo, SHOP / TULONG / SUNDAN columns, and the credit line "Sa tulong ng DTI Negosyo Center Paniqui".

## Business rules (placeholders — confirm with client)
- Size adjustment on the product's base price:
  - Maliit (28×22 cm): −₱250
  - Katamtaman (36×30 cm): base price
  - Malaki (44×36 cm): +₱300
- Shipping is free at ₱2,000 or more; otherwise ₱120.
- The gift box adds ₱150.
- Custom orders require a 50% downpayment.
- Returns are accepted within 7 days; custom orders can't be returned.

## Design tokens
**Colors** (brand guide — only these five):
- Narra Maroon `#6B1A24`: logo, buttons, headings, story band, BAGO tag
- Buri Cream `#F3EBDD`: page background
- Abaca Beige `#D8C7A8`: borders, banig pattern, notices
- Uling `#1D1A17`: text, footer, PABORITO tag
- Rattan Gold `#B8925A`: hairlines, foil mark, ISA NA LANG tag background

**Helper colors:**
- `#561420`: maroon hover
- `#E6DAC4`: image backing
- `#FBF7F0`: inputs and cards

**Color rules:**
- Never use gold text on cream.
- Never put the banig pattern behind text.

**Type:** Averia Serif Libre only (Google Fonts), weights 300 / 400 / 700 and italic 400.
- Display: 700, clamp(46px, 6.2vw, 80px), line-height 1
- Heading: 400, 28–40px, line-height 1.2
- Body: 300, 16–19px, line-height 1.6
- Label: 400, 11–13px, uppercase, letter-spacing 0.2em
- Price format: `₱1,950`

**Banig pattern:**
`conic-gradient(from 45deg, #6B1A24 25%, #D8C7A8 0 50%, #6B1A24 0 75%, #D8C7A8 0) 0 0/10px 10px`

**Layout:**
- Max width 1280px; gutter clamp(18px, 4vw, 56px).
- Grids use `repeat(auto-fill, minmax(min(100%, 240px), 1fr))`.
- Button and input radius 2px; filter chips are pills.

**Product tags:**
| Tag | Background | Text |
|---|---|---|
| BAGO | `#6B1A24` | `#F3EBDD` |
| PABORITO | `#1D1A17` | `#F3EBDD` |
| ISA NA LANG | `#B8925A` | `#1D1A17` |

On cards, the tag hangs at the top-left with a 6px cream hole dot and sways.

## Motion
- **Easing** for all entrances: `cubic-bezier(.2,.7,.2,1)`.
- **Entrance (bgUp):** fade in from translateY(24px), 0.7–0.9s.
  - Hero elements stagger from 0s to 0.6s.
  - Product cards stagger at 0.05s plus 0.07s per index.
- **Hero photo zoom:** scale 1 → 1.08, 16s, alternate.
- **Tag sway:** rotate −5° → 4°, about 3s, alternate.
- **Gold mark:** floats 4px up and down.
- **Banig strips:** scroll 140px every 8s.
- **Marquee:** 32s linear.
- **Hover:**
  - Cards lift 6px.
  - Primary buttons change to `#561420`.
  - Outline buttons fill maroon.
- **Active:** buttons scale to 0.97.
- **Cart drawer:** slides in over 0.35s.
- **Search panel:** drops in over 0.3s.
- **Reduced motion:** honor `prefers-reduced-motion` by disabling all of the above.

## Products (15) — names and prices are placeholders
Product data is in the `PRODUCTS` array: name, number, image, price, category, material label, description and tag.

| Bag | Image | Price | Category | Tag |
|---|---|---|---|---|
| Paru-paro | paru-paro.jpg | ₱2,100 | Abo | PABORITO |
| Sakura sa Gabi | sakura-sa-gabi.jpg | ₱1,850 | Itim | ISA NA LANG |
| Rosas Mayumi | rosas-mayumi.jpg | ₱1,950 | Rosas | — |
| Rosas Ube | rosas-ube.jpg | ₱1,950 | Rosas | BAGO |
| Liwayway | liwayway.jpg | ₱2,100 | Abo | BAGO |
| Alon | alon.jpg | ₱2,100 | Berde | BAGO |
| Tagsibol | tagsibol.jpg | ₱1,850 | Rosas | — |
| Diwata | diwata.jpg | ₱2,450 | Kayumanggi | ISA NA LANG |
| Rosas Kape | rosas-kape.jpg | ₱1,950 | Kayumanggi | — |
| Dalaga | dalaga.jpg | ₱2,450 | Itim | PABORITO |
| Boss Lady | boss-lady.jpg | ₱2,450 | Puti | BAGO |
| Hardin | hardin.jpg | ₱1,950 | Rosas | — |
| Liryo | liryo.jpg | ₱2,450 | Itim | — |
| Payak Lila | payak-lila.jpg | ₱1,250 | Lila | — |
| Sinag | sinag.jpg | ₱2,650 | Puti | BAGO |

## Assets (`assets/`)
- `logo.png`, `mark.png`: black on transparent. Apply them as CSS masks so they can be tinted maroon, cream or gold.
- `icon-habi.png`: weave icon from the brand guide.
- `home-hero.jpg`: home hero photo and Kuwento page image.
- `honey-tess.png`: founder at the Likha ng Central Luzon trade fair. Used in the home story band, the Kuwento portrait and the round portrait on the product page.
- 15 product photos, listed in the table above.

## State to implement
- **Persisted** (localStorage, or a backend later):
  - cart: `{id, pid, name, variant, price, qty}`
  - gift box option
  - orders
  - user
- **UI state:**
  - product page: selected product, gallery view, size, quantity, open accordion item
  - collection: filter and sort
  - search query
  - cart drawer and search overlay open or closed
- **Form validation:**
  - Checkout requires name, mobile number and address.
  - Login requires email and password.
  - Custom request requires name, contact and idea.

## Not yet done
- Real authentication, payments and inventory.
- An actual contact form endpoint for custom requests.
- Final copy for the founder quote.
- Social media URLs.
