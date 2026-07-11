# Source Of Truth

Reference spreadsheet:

- [Custom Dynamic Type Token for Designer.xlsm](https://docs.google.com/spreadsheets/d/1Ecpf_CZClh7xqB8H5NAFegselvUb4nBs/edit?usp=sharing&ouid=108675797915406885699&rtpof=true&sd=true)

For this workflow, only the tabs with `figma` in the name are in scope:

- `figma_dynamic_text_token`
- `figma_dynamic_spacing_token`

## Mode Rule

Use the mode names exactly as they appear in the active sheet.

Do not hard-code a fixed set like `Smallest`, `Default`, or `lg` into the skill itself.

## Canonical Collection Mapping

- `00 Base Type`
  - `font-family/*`
  - `font-weight/*`
  - single value only
  - no theme modes

- `00 Density`
  - `font-size/*`
  - `font-line-height/*`
  - `letter-spacing/*`
  - `space/*`
  - `size/*`

## Collection Naming Rule

Use ASCII-only collection names:

- `00 Base Type`
- `00 Density`

Do not use the dotted variant with `·`.

## Canonical Text-Style Structure

Use this exact hierarchy:

```text
[token-name]/[default-size]px/[weight]
```

Examples:

- `display-lg/44px/bold`
- `display-md/40px/regular`
- `heading-md/24px/semibold`
- `body-md/14px/regular`

Notes:

- `default-size` means the `Default` mode value from `font-size/*`
- the style's line height must come from the matching `font-line-height/*` token in `Default`
- the text style should bind `fontFamily`, `fontWeight`, `fontSize`, `lineHeight`, and `letterSpacing` to the matching variables when available
- by default, create these weights only:
  - `bold`
  - `semibold`
  - `medium`
  - `regular`

## Validation Samples

These values are useful as quick sanity checks:

- `font-size/display-lg` = `39 / 41 / 44 / 50 / 55`
- `font-line-height/display-lg` = `49 / 52 / 56 / 63 / 69`
- `font-size/body-md` = `12 / 13 / 14 / 16 / 18`
- `font-line-height/body-md` = `18 / 20 / 21 / 24 / 27`
