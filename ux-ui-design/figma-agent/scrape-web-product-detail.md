---
name: scrape-web-products-detail
description: Scrape product data (name, image, price, discount, unit) from a any e-commerce website and populate it into selected Figma product list rows
---

# Scrape Web Products into Figma

Scrape product information from a given e-commerce URL and fill it into a selected product list component in Figma.

## When to use

The user selects a frame containing repeated product row instances (e.g. a cart list, product table, or order summary) and provides a URL to an e-commerce product listing or search results page. The user wants real product data (names, images, prices, units) pulled from the website and populated into the selected rows.

## Inputs

1. **A URL** to a product listing or search results page (e.g. `https://nhathuoclongchau.com.vn/tim-kiem?s=...`).
2. **A selected frame** in Figma containing product row instances with text and image placeholders.

## Step 1 — Inspect the selected frame

Use `evaluate_script` to build a layer tree of the selected frame. Identify:

- The repeated product row instances (typically INSTANCE nodes with a consistent component name).
- Inside each row, locate the node IDs for:
  - **Product name** (TEXT node)
  - **Sale price** (TEXT node)
  - **Strikethrough / original price** (TEXT node, may need to be hidden when no discount)
  - **Unit or specification label** (TEXT node, e.g. inside a chip or tag)
  - **Product image** (RECTANGLE or FRAME node with an image fill)

Log all relevant node IDs per row for use in later steps.

## Step 2 — Fetch product data from the website

Use `curl` via Bash to download the HTML of the given URL.

Many e-commerce sites are server-side rendered with Next.js. Look for product data in this priority order:

1. **`__NEXT_DATA__`** — parse the JSON inside `<script id="__NEXT_DATA__">`. Product arrays are typically at `props.pageProps.initProducts.products` or similar.
2. **JSON-LD** — look for `<script type="application/ld+json">` blocks with `@type: Product`.
3. **API endpoints** — inspect the HTML for fetch URLs or `_next/data` paths. Call them directly with `curl`.
4. **HTML scraping** — as a last resort, extract data from the DOM using regex or a parser.

For each product, extract:
- `name` — the display/web name
- `image` — the full image URL
- `final_price` — the current selling price, formatted (e.g. `"395.000đ"`)
- `strikethrough_price` — the original price before discount (empty string if no discount)
- `discount_pct` — percentage discount label (e.g. `"-20%"`, empty if none)
- `unit` — the measure unit (e.g. `"Hộp"`, `"Tuýp"`, `"Viên"`)
- `spec` — the specification string (e.g. `"Hộp x 100ml"`)

Filter out products with a price of 0 or missing data. Match the number of extracted products to the number of available rows in the Figma frame.

## Step 3 — Update text content

Use `evaluate_script` to update text nodes in each product row:

- Load all fonts on each text node before modifying (`getStyledTextSegments(['fontName'])` then `loadFontAsync`).
- Set the product name text.
- Set the sale price text.
- If there is a discount: set the strikethrough price and make it visible. If no discount: hide the strikethrough price node (`visible = false`).
- Set the unit/specification label text.
- If the data curated did not get any value, hide the corresponding layer in figma

## Step 4 — Upload and apply product images

1. Call `upload_assets` to get upload URLs (one per product).
2. Use `curl` via Bash to download each product image from the source URL to a temp file, then POST each image to its upload URL. Run downloads and uploads in parallel for speed.
3. Use `evaluate_script` to:
   - Set each product row's image rectangle fill to `{ type: 'IMAGE', scaleMode: 'FIT', imageHash: '<hash>' }` using the `imageHash` from the upload response.
   - Remove any auto-placed image nodes created by `upload_assets` (the `placedOnNodeId` from each upload response).

## Step 5 — Verify

Use `evaluate_script` to take a screenshot of the updated frame (`await node.screenshot()`) and visually confirm:
- All product names are readable and not truncated.
- Prices display correctly.
- Images are visible and properly fitted.
- Units/specs match each product.

## Notes

- Always format Vietnamese prices with dot separators (e.g. `395.000đ`).
- If the website blocks direct requests, try adding browser-like `User-Agent` and `Accept` headers to `curl`.
- If the page is fully client-side rendered and no `__NEXT_DATA__` exists, look for XHR/API endpoints in the page source.
- The number of products populated should match the number of row instances available in the selected frame. Do not create or remove rows.
