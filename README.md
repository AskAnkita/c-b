# Chain & Bracelet — homepage prototype

Static front-end prototype for ChainAndBracelet.com, built to the reference comp
(centred wordmark nav, split hero, three-column editorial grid, quick-shop
carousel, brown footer).

## Run

XAMPP is already serving it:

    http://localhost/c&b-prototype/

No build step, no dependencies — plain HTML, CSS and vanilla JS. Opening
`index.html` from the filesystem works too.

## Pages

| File           | What it is                                                       |
| -------------- | ---------------------------------------------------------------- |
| `index.html`   | Homepage — hero, signature grid, editorial split, carousel, gifting |
| `shop.html`    | Listing (PLP) — banner, filters, sort, grid, paging               |
| `product.html` | Detail (PDP) — gallery, buy column, tabs, add-ons, related        |

`shop.html` reads `?c=` (`chains`, `bracelets`, `earrings`, `rings`, `addons`)
and `product.html` reads `?id=` (any catalogue id), so every link deep-links.

## Files

    assets/css/style.css    tokens, layout, components, responsive rules
    assets/css/fonts.css    @font-face for the two self-hosted families
    assets/fonts/           Cormorant Garamond + Montserrat (woff2, latin sets)
    assets/js/catalog.js    the 17-piece product catalogue + helpers
    assets/js/main.js       shared shell — cart drawer, wishlist, search, carousel
    assets/js/shop.js       listing page — filter, sort, show more
    assets/js/pdp.js        detail page — gallery, sizes, tabs, add-ons, related
    assets/img/editorial/   full-bleed lifestyle photography
    assets/img/products/    cut-out product shots (transparent PNG)

The header, footer and overlays are duplicated in each HTML file rather than
included, since there is no build step. Edit one, edit all three.

## Information architecture

The client's framing — *"domain is chainandbracelet.com but we keep earrings and
rings as well for customers to add on to their purchase"* — is built into the
structure rather than just the copy:

- **Chains** and **Bracelets** are the two primary nav items, left of the wordmark.
- **Earrings & Rings** is one nav item on the right, pointing at `shop.html?c=addons`.
- In the catalogue every product carries an `addon` flag (true for earrings and
  rings), which drives the **Add-Ons** filter chip and the PDP module.
- On a chain or bracelet PDP, that module is **"Add to Your Order"** and offers
  earrings and rings with a one-tap Add. On an earring or ring PDP it flips to
  **"Wear It With"** and offers chains and bracelets. That is the add-on sell,
  in the place where it converts.

## Design tokens

Defined once at the top of `style.css` as custom properties:

| Token          | Value     | Used for                          |
| -------------- | --------- | --------------------------------- |
| `--cream`      | `#efe9e0` | page background                   |
| `--cream-soft` | `#f5f1ea` | section panels                    |
| `--brown`      | `#8a7866` | accent panels, footer, quick-shop |
| `--ink`        | `#1c1a17` | headings and body text            |
| `--muted`      | `#6b6058` | secondary copy                    |
| `--line-soft`  | `#e8e1d6` | hairline borders                  |

Display type is Cormorant Garamond, uppercase with wide tracking; UI and body
copy are Montserrat at 300–400.

## Interactions

- **Quick shop** — hovering a homepage carousel card reveals the brown plate with
  a variant selector and *Shop Now*; on touch devices tapping the card opens it.
- **Quick add** — hovering a listing card slides up an *Add — 18 in* bar that
  drops the default variant straight into the bag.
- **Bag** — items push into the drawer with variant and price, update the badge
  and subtotal, and can be removed.
- **Wishlist** — the heart on any card toggles and drives the header count.
- **Filter and sort** — category chips rewrite the URL as you click, so the state
  is shareable. Sort covers featured, price both ways and rating.
- **Gallery** — thumbnails swap the stage image; cut-outs are letterboxed and
  on-model shots fill the frame.
- **Carousel** — Prev/Next page by whole cards; also draggable, snaps to the
  nearest card, disables the arrows at each end.
- **Search** — the magnifier opens a full-screen overlay; Esc closes any overlay.

State is in-memory only — a reload empties the bag. Nothing is persisted and
there is no backend.

## Known scope limits

- Product data lives in `assets/js/catalog.js`, which is where a real catalogue
  feed or CMS would plug in. Seventeen pieces, enough to fill the grid twice.
- Photography is placeholder, borrowed from the neighbouring prototype in
  `htdocs/`. **The chain and bracelet shots are the thin part** — there is one
  true cut-out each, so some cards fall back to on-model photography. Real
  product shots are the first thing to commission.
- The white backgrounds on the ring cut-outs were knocked out to transparency so
  they sit on the grey tiles. Redo that properly on the real assets.
- Search returns a toast, not results. Checkout is a dead link. Reviews are a
  number, not a system.
