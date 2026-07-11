---
name: figma-color-token-setup
description: Use when the task is to set up or refresh Figma color tokens from a spreadsheet or workbook source of truth, import Base Alias Component color variables into a Figma file, sync multi-theme or multi-brand color modes, rebuild alias-to-base and component-to-alias token links, or fix color-variable collections such as 00 Base Color, 01 Alias, and 02 Component.
---

# Figma Color Token Setup

Use this skill when the user wants to:

- import color tokens from a spreadsheet into a Figma file
- sync multi-brand color variables from workbook to Figma
- create or refresh `00 Base Color`, `01 Alias`, and `02 Component`
- rebuild token relationships from `Base -> Alias -> Component`
- correct color token links so alias points to base and component points to alias
- preserve theme and mode logic defined by the source workbook

## Source Of Truth

Read [references/source-of-truth.md](references/source-of-truth.md) before editing values.

Use this reference sheet when the user does not provide a different source:

- [Multi-brand Color Token for Designer.xlsx](https://docs.google.com/spreadsheets/d/1-IzflJv0nSI3r0U_BrJ24HIcMI_h653P/edit?usp=sharing&ouid=108675797915406885699&rtpof=true&sd=true)

## Required Workflow

1. Inspect the target Figma file first.
2. Check local variable collections, modes, and variables before writing.
3. Read the workbook source of truth before changing any color token.
4. For this workbook, only these tabs are in scope:
   - `Base`
   - `Alias`
   - `Component`
5. Read displayed token names and displayed color values from the workbook source. Do not infer missing rows from earlier exports if the current workbook content is available.
6. If the Drive connector cannot read the file as a native Google Sheet because it is still an Office workbook, fall back to reading the workbook content directly. Do not assume the source is unavailable.
7. Create or update the Figma collections:
   - `00 Base Color`
   - `01 Alias`
   - `02 Component`
8. Optional extension: if the workbook or target Figma architecture includes a separate sub-brand or mini-app theme layer, also create `00 Another Branding Theme`.
9. Use the mode structure exactly as defined by the workbook.
10. Keep `00 Base Color` as the main bridge collection unless the workbook explicitly defines a different architecture. Do not mirror Base themes into Alias or Component unless the workbook explicitly requires that.
11. In `00 Base Color`, store actual color values only, except when the workbook explicitly uses one Base mode as a bridge layer that aliases to `00 Another Branding Theme`.
12. In `01 Alias`, store token references to Base tokens. Do not flatten Alias into hardcoded hex values unless the user explicitly asks for a destructive export.
13. In `02 Component`, store token references to Alias tokens, or to Base only when the workbook explicitly does so.
14. Update variables idempotently. Reuse existing variables by collection + name whenever they already exist.
15. Preserve workbook row order and numeric token order. Do not auto-sort token scales alphabetically.
16. Validate a few key base values, alias links, and component links before stopping.

## Radix Scale Rule

When the user asks for a Radix-style palette generated from one anchor color, treat the palette as a **12-step Radix scale** and keep the numeric naming exactly as:

- `1`
- `2`
- `3`
- `4`
- `5`
- `6`
- `7`
- `8`
- `9`
- `10`
- `11`
- `12`

Do not rename these steps to `25/50/100/.../950` inside this skill unless the user explicitly asks for a downstream export mapping. In the Figma/base-token system governed by this skill, Radix steps should stay `1..12`.

### How to interpret the anchor color

For Radix-style generation, the provided main color is the anchor for **step `9`**.

That means:

- step `9` = the main solid brand color
- step `10` = hover state for the solid color
- steps `11` and `12` = accessible text / high-contrast text derived from the same hue family
- steps `1` through `8` = progressively lighter background, surface, and border steps derived from the same hue family

### How to generate the scale

When generating a custom Radix-style palette:

1. Start from an official Radix light scale whose hue family is closest to the requested brand hue.
2. Treat that official Radix scale as the reference shape across steps `1..12`.
3. Replace the reference scale's step `9` with the user's provided main color.
4. Rebuild the remaining steps so they preserve the same role progression as Radix:
   - `1..2`: app/background steps
   - `3..5`: subtle UI backgrounds
   - `6..8`: borders and separators
   - `9..10`: solid and hover solid
   - `11..12`: accessible text
5. Keep alpha scales aligned to the same `1..12` numbering and semantic role progression.

Important:

- do not generate the scale by simply mixing white and black in evenly spaced percentages
- do not assume `9` is the darkest step; Radix balances lightness, chroma, and usefulness per role
- if possible, use official Radix custom-palette output or official Radix palette CSS as the reference shape
- if you must approximate, explicitly preserve the Radix role of each step instead of treating the scale as a generic tint/shade ramp

## Variable Mapping

### `00 Base Color`

Keep only actual color primitives here.

- theme columns:
  - whatever theme or brand columns exist in the workbook
- values:
  - real color values
  - RGBA or hex-backed color data only

Common families include:

- `color/brand-*`
- `color/gray*`
- `color/blackA*`
- `color/whiteA*`
- `color/red*`
- `color/pink*`
- `color/purple*`
- `color/blue*`
- `color/cyan*`
- `color/green*`
- `color/orange*`
- `color/yellow*`
- `color/sky*`

Important:

- keep theme logic only in this collection
- do not mirror semantic presentation modes here unless the workbook explicitly stores them in Base
- do not convert Base rows into token-name aliases
- exception: if the workbook defines an optional alternate-brand bridge, one or more Base modes may alias selected brand families to variables from `00 Another Branding Theme`

### Optional `00 Another Branding Theme`

Use this collection only when the workbook or target Figma file clearly uses a separate raw token set for a mini-app, sub-brand, campaign, or alternate branding branch.

- collection name:
  - `00 Another Branding Theme`
- modes:
  - whatever alternate theme modes exist in the workbook
- values:
  - real color values only

Typical families in this collection:

- `color/brand/*`
- `color/brand-secondary/*`
- `color/brand-alpha/*`
- `color/brand-secondary-alpha/*`
- `color/brand-dark/*`
- `color/brand-secondary-dark/*`
- `color/brand-dark-alpha/*`
- `color/brand-secondary-dark-alpha/*`

Important:

- this collection is optional
- do not create it unless the workbook or existing Figma file clearly shows this pattern
- use it as the raw source for alternate primary and secondary branding scales
- keep `01 Alias` and `02 Component` linked to `00 Base Color`, not directly to `00 Another Branding Theme`
- let one or more modes in `00 Base Color` act as the bridge by aliasing selected brand-family variables to `00 Another Branding Theme`

### `01 Alias`

Use this collection for semantic links only.

- modes:
  - whatever alias modes exist in the workbook
- values:
  - token references to `00 Base Color`

Common groups include:

- `color/bg/*`
- `color/text/*`
- `color/border/*`
- `color/icon/*`
- `color/error/*`
- `color/warning/*`
- `color/success/*`
- `color/info/*`
- `color/skeleton/*`
- `color/graphic/*`

Important:

- keep alias values as references, not duplicated color values
- the first visual mode often points to the normal base families
- the second visual mode often points to `-dark` or `A-dark` families when defined by the workbook

### `02 Component`

Use this collection for component-level links only.

- mode:
  - whatever component mode exists in the workbook
- values:
  - token references to `01 Alias`
  - direct links to Base only when the workbook explicitly uses Base

Common groups include:

- `button/*`
- `input/*`
- `card/*`
- `badge/*`
- `nav/*`
- `modal/*`
- `toast/*`
- `skeleton/*`
- `rich-text/*`

Important:

- keep one mode only
- do not introduce `Light` and `Dark` modes here
- do not replace workbook links with copied color values

## Naming Rule For Collections

Use the collection names exactly as the workbook and target Figma workflow expect.

Required names:

- `00 Base Color`
- `01 Alias`
- `02 Component`

Optional name:

- `00 Another Branding Theme`

Do not use:

- `00 · Base Color`
- `01 · Alias`
- `02 · Component`

Use ASCII-only collection names for export friendliness and to match files where the dot separator has already been removed in Figma.

## Linking Rules

The canonical relationship is:

```text
Base value -> Alias semantic token -> Component usage token
```

Examples:

- Base stores a primitive token such as `color/brand-primary/9` as a real color value.
- Alias stores a semantic token such as `color/bg/brand-primary` as a reference to one Base token in one visual mode and to a dark or alternate Base token in another visual mode.
- Component stores a usage token such as `button/bg/primary` as a reference to the matching Alias token.

Optional alternate-branding example:

- `00 Another Branding Theme` stores raw values for `color/brand/9`, `color/brand-secondary/9`, and matching alpha or dark families.
- one mode inside `00 Base Color` aliases:
  - `color/brand-primary/9` -> `00 Another Branding Theme / color/brand/9`
  - `color/brand-secondary/9` -> `00 Another Branding Theme / color/brand-secondary/9`
  - `color/brand-primary-alpha/9` -> `00 Another Branding Theme / color/brand-alpha/9`
  - `color/brand-primary-dark/9` -> `00 Another Branding Theme / color/brand-dark/9`
- `01 Alias` still points only to `00 Base Color`, so semantic and component layers stay unchanged while one Base mode switches the brand family underneath.

Important:

- When the workbook expresses a token as a linked token name, keep it as a linked token in Figma.
- Do not collapse Alias and Component into direct raw values during normal sync.
- Do not invent new token names or family names that are not present in the workbook.

## Workbook Rules

- `Base` is the only tab that contains actual color values by theme.
- `Alias` keeps token-name links to Base.
- `Component` keeps token-name links to Alias or Base.
- This workbook uses simple spreadsheet linking patterns. Respect the visible linked token names instead of replacing them with your own mapping logic.
- If one theme or brand diverges from another, trust only the rows that explicitly show that divergence. Do not globally assume an entire family should be swapped unless the workbook rows confirm it.
- Optional architecture: if the workbook shows a dedicated alternate-brand collection, keep that collection as a raw-value source and use one Base mode as the bridge layer through variable aliases.

## Validation Checklist

Always verify all of the following:

1. Collections exist with the exact names above.
2. `00 Base Color` has exactly the theme or brand modes defined by the workbook.
3. `01 Alias` has exactly the semantic or visual modes defined by the workbook.
4. `02 Component` has exactly the component mode structure defined by the workbook.
5. If the workbook defines an alternate-brand collection, `00 Another Branding Theme` exists and contains raw values rather than aliases.
6. At least these Base tokens exist and keep real values or valid bridge aliases, depending on the workbook architecture:
   - `color/brand-primary/9`
   - one secondary or alternate family token such as `color/brand-secondary/9`
   - one neutral or utility family token such as `color/gray/9`
   - one dark or alternate token such as `color/brand-primary-dark/9`
7. At least these Alias tokens exist and link correctly:
   - `color/bg/brand-primary`
   - `color/text/primary`
   - one graphic token such as `color/graphic/primary/9`
   - one semantic feedback token such as `color/error/text`
8. At least these Component tokens exist and link correctly:
   - `button/bg/primary`
   - `input/text/value`
   - one navigation or selection token such as `nav/tab/active-icon`
   - one feedback token such as `toast/bg/error`
9. If `00 Another Branding Theme` is present, confirm that Alias still points to `00 Base Color` rather than directly to the optional branding collection.
10. Alias and Component remain linked-token systems, not flattened color copies, unless the task explicitly asked for flattening.

## Recovery Notes

- If the source workbook is still an Excel file on Drive, do not block on native Google Sheets APIs. Read the workbook content directly and continue.
- If earlier sync attempts created dotted collection names or duplicated collections, rename or consolidate them into the ASCII-only set instead of layering a second parallel system on top.
- If a token family changed between attempts, trust the current workbook source of truth, not an older local export or memory of previous values.
