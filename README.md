# SnagWise theme

Shopify theme for **SnagWise** (snagwise.myshopify.com): brand-new, sealed, name-brand products under retail, with free pickup in Hamilton and Waterloo and flat-fee delivery across the GTHA and Waterloo Region.

Fork of Shopify Dawn 16.0.0 with the shared conversion layer used across the Bello-online stores (`trust-bar`, `testimonials`, `comparison-table`, `stats-strip` sections, `sticky-atc` and `free-shipping-bar` snippets, `assets/cro.css`), plus the SnagWise layer described below.

## Two themes, two branches

| Branch | Theme in the store | Palette |
| --- | --- | --- |
| `main` | SnagWise Soot | #0F0F0F ground, #1A1A1A surface, #DAFA9C lime, white paper |
| `pine` | SnagWise Pine | #0B2E24 ground, #124034 surface, #DAFA9C lime, #EEF3EF paper |

The only difference between the branches is `config/settings_data.json` (the five colour schemes). Build features on `main`, then `git checkout pine && git rebase main` to carry them across.

Through Shopify's GitHub integration each branch connects to its own theme in the store's theme library (Online Store > Themes > Add theme > Connect from GitHub). Pushes sync to the theme; edits made in the theme editor come back as "Update from Shopify" commits, so always `git fetch` and rebase before pushing.

## The SnagWise layer

Direction: "the object, large". One product cut-out breaks the right edge of a flat dark field, the copy sits small on the left, and two corner cards point at Almost gone and Just landed. Archivo only (400 for headlines, 600 for buttons and prices), square corners, no shadows or gradients, lime reserved for savings and the one action.

Sections (all in `sections/snag-*.liquid`, styles in `assets/snag.css` and `assets/section-snag-hero.css`):

- **snag-hero**: pick a hero deal product; its image is the object, its price feeds the fact line (price, retail, units left). Object size and tilt are settings. Two corner cards take a collection each.
- **snag-drop**: collection grid of `card-snag` cards: cut-out on white, price with retail struck through, "You save $X" in lime, stock count, "Just landed" on products tagged `new` or created within N days.
- **snag-almost-gone**: lime band of rows from a collection, filtered to items at or below a stock threshold.
- **snag-categories**: collection tiles with item counts.
- **snag-how**: three tiles that grow on hover.
- **snag-social**: six image blocks plus Instagram and TikTok links.
- Dawn's `newsletter` section carries the "Get first dibs on new drops" signup; `trust-bar` carries the four trust items.

Product page blocks in `sections/main-product.liquid` (rendered by `snippets/snag-product-blocks.liquid`):

- **SnagWise deal line**: "You save $X", condition line, "Only N left · Limited quantity".
- **SnagWise pickup & delivery**: Hamilton / Waterloo / Delivery picker that shows the fee and timing for each. Works without JavaScript (first option shown).
- **SnagWise ask button**: opens WhatsApp (with a prefilled message) or an Instagram DM. Set the number or handle in the block settings.

Dawn's own product card (`snippets/card-product.liquid`, used on collection and search pages) gets the same savings and stock lines through `snippets/snag-card-meta.liquid`.

Stock counts come from `variant.inventory_quantity`, so inventory tracking must be on for every product. The deal line and stock count render for the selected variant on page load; the sample products have a single variant each.

## Product photos

Product images are transparent PNG cut-outs (1200 x 1200) so the same image works on the dark hero field and on the white cards. Working files for the sample products live in `../media/snagwise/` (originals, `cutout.py`, `out/`). The nine sample products are placeholders: replace them with the real items before launch.

## Content the theme expects

Collections: `this-weeks-drop`, `last-chance`, `home-kitchen`, `vacuums-cleaning`, `audio-tech`, `toys-collectibles`, `baby-kids`, `tools-auto`, `under-50`. Pages: `about`, `how-it-works`, `faq`, `pickup-delivery`, `returns-policy`, `contact` (contact template). Menus: `main-menu`, `footer`.

Brand names appear only on product listings, never in the theme's copy or design.

## Working locally

```bash
shopify theme dev --store snagwise
shopify theme check
```
