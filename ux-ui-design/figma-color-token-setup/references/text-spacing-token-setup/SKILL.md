---
name: figma-text-spacing-token-setup
description: Use when the task is to set up or refresh Figma text tokens, spacing tokens, and text styles from a spreadsheet source of truth. Triggers on requests like import token from sheet to Figma, setup 00 Base Type or 00 Density, sync text and spacing token, bind text-style properties to variables, or create text styles from token with hierarchy like display-lg/44px/bold.
---

# Figma Text And Spacing Token Setup

Use this skill when the user wants to:

- import text tokens from a spreadsheet into a Figma file
- import spacing tokens from a spreadsheet into a Figma file
- create or refresh `00 Base Type` and `00 Density`
- create text styles from imported text tokens
- bind text-style properties back to variables
- rebuild text-style naming so it is easy to search in Figma

## Source Of Truth

Read [references/source-of-truth.md](references/source-of-truth.md) before editing values.

Use this reference sheet when the user does not provide a different source:

- [Custom Dynamic Type Token for Designer.xlsm](https://docs.google.com/spreadsheets/d/1Ecpf_CZClh7xqB8H5NAFegselvUb4nBs/edit?usp=sharing&ouid=108675797915406885699&rtpof=true&sd=true)

## Required Workflow

1. Inspect the target Figma file first.
2. Check local variable collections, modes, variables, and text styles before writing.
3. Only use tabs whose name contains `figma`.
4. For this spreadsheet, the active tabs are:
   - `figma_dynamic_text_token`
   - `figma_dynamic_spacing_token`
5. Read displayed values from those tabs. Do not infer production values from older local copies or from formula shortcuts if the visible sheet values are available.
6. Create or update the Figma collections:
   - `00 Base Type`
   - `00 Density`
7. For density-like collections, use the mode names exactly as they appear in the sheet. Do not hard-code a mode vocabulary into the skill.
8. Exception: `00 Base Type` should not use theme or multi-mode setup. Keep it as a single-value collection only.
9. Keep collection names ASCII-friendly. Do not use `·` in collection names.
10. Update variables idempotently. Reuse existing variables by collection + name when present.
11. After token sync succeeds, create or refresh text styles from the text tokens.
12. Bind text-style properties to the matching variables whenever the corresponding variable exists.
13. Validate a few key token values and a few key text-style names before stopping.

## Variable Mapping

### `00 Base Type`

Keep only typography primitives here.

- `font-family/*`
- `font-weight/*`

Important:

- do not create theme modes here
- do not mirror `Smallest / Smaller / Default / Bigger / Biggest`
- keep only one mode or one value column for this collection
- treat this as a static primitive table for export and handoff

Use explicit scopes:

- family: `FONT_FAMILY`
- weight: `FONT_WEIGHT`

### `00 Density`

Put text sizing and spacing tokens here.

- `font-size/*`
- `font-line-height/*`
- `letter-spacing/*`
- `space/*`
- `size/*`

Use explicit scopes:

- font size: `FONT_SIZE`
- line height: `LINE_HEIGHT`
- letter spacing: `LETTER_SPACING`
- spacing gaps: `GAP`
- control or touch sizes: `WIDTH_HEIGHT`

## Naming Rule For Collections

Use plain ASCII collection names for export friendliness.

Required names:

- `00 Base Type`
- `00 Density`

Do not use:

- `00 · Typo Base`
- `00 Typo Base`
- `00 · Density`

## Text-Style Rules

Create text styles only after the text tokens are correct.

Each text style should bind back to the variables that define it whenever the Figma API supports that binding.

### Naming

The required naming hierarchy is:

```text
[token-group]/[default-font-size]px/[weight]
```

Examples:

- `display-lg/44px/bold`
- `display-md/40px/regular`
- `heading-md/24px/semibold`
- `body-md/14px/regular`

Important:

- Do not flatten as `display/44px/bold` unless the user explicitly asks for that structure.
- The middle segment must be the actual default mode font size from the token.
- The style preview should read like `bold · 44/56`, `regular · 14/21`, etc because the style itself is built from the default mode size and line height.

### Which weights to create

Default set for this workflow:

- `bold`
- `semibold`
- `medium`
- `regular`

Only create more weights if the user asks.

### Which mode drives the style

Use the `Default` mode values for text-style creation unless the user explicitly asks for style variants per mode.

That means:

- style name size comes from `Default`
- `fontSize` comes from `Default`
- `lineHeight` comes from `Default`

### Binding Requirements

When matching variables exist, bind these text-style properties:

- `fontFamily`
- `fontWeight`
- `fontSize`
- `lineHeight`
- `letterSpacing`

If the file or API requires a concrete value to exist before binding, set the concrete value from the same token first, then bind the property to the variable.

## Font Handling

Inspect available fonts in the target Figma file before creating styles.

- Use the font family defined in the sheet.
- Do not replace the source font family with workflow-specific assumptions in the skill.

Do not guess font style names. Check available styles first, then load exact names such as `Semi Bold`.

## Validation Checklist

Always verify all of the following:

1. Collections exist with the exact names above.
2. `00 Base Type` remains single-value and does not carry theme modes.
3. `00 Density` mode names match the sheet being used.
4. At least these variables match the sheet:
   - `font-size/display-lg`
   - `font-line-height/display-lg`
   - `letter-spacing/display-lg`
   - `font-size/body-md`
   - `font-line-height/body-md`
5. At least these text styles exist with correct hierarchy:
   - `display-lg/44px/bold`
   - `display-md/40px/regular`
   - `body-md/14px/regular`
6. Bound text-style properties point to the matching variables where supported, including `letterSpacing`.
7. No stale flat naming remains if the task was a rebuild.

## Recovery Notes

- If the Google connector cannot read the spreadsheet as a native Google Sheet because it is still an Office file, do not assume the data is unavailable. Fall back to the workbook content itself or another direct way to read the visible tab values.
- If prior Figma variables or text styles were created with wrong mode names or wrong naming hierarchy, correct them directly instead of layering a second parallel system on top.
- If a token family changed between attempts, trust the canonical sheet values, not earlier local approximations.
