# Source Of Truth

Reference workbook:

- [Multi-brand Color Token for Designer.xlsx](https://docs.google.com/spreadsheets/d/1-IzflJv0nSI3r0U_BrJ24HIcMI_h653P/edit?usp=sharing&ouid=108675797915406885699&rtpof=true&sd=true)

For this workflow, only these tabs are in scope:

- `Base`
- `Alias`
- `Component`

Optional extension:

- a dedicated alternate-brand tab or source block for a sub-brand, mini-app, or campaign theme

## Tab Purpose

- `Base`
  - stores actual color values
  - theme columns:
    - whatever theme or brand columns exist in the workbook
- `Alias`
  - stores token-name links to Base
  - mode columns:
    - whatever alias modes exist in the workbook
- `Component`
  - stores token-name links to Alias or Base
  - mode column:
    - whatever component mode exists in the workbook

- optional alternate-brand source
  - stores raw values for a secondary branding branch
  - often used for new primary and secondary families plus matching alpha and dark families

## Canonical Collection Mapping

- `00 Base Color`
  - source tab: `Base`
  - modes:
    - read the exact theme or brand columns from the workbook
  - values:
    - actual color values only

- `01 Alias`
  - source tab: `Alias`
  - modes:
    - read the exact alias modes from the workbook
  - values:
    - token references to Base

- `02 Component`
  - source tab: `Component`
  - modes:
    - read the exact component modes from the workbook
  - values:
    - token references to Alias or Base

- `00 Another Branding Theme`
  - source:
    - only create when the workbook explicitly defines a separate alternate-brand source
  - modes:
    - read the exact alternate-theme modes from the workbook
  - values:
    - actual color values only
  - purpose:
    - provide raw primary and secondary scales for a sub-brand, mini-app, or campaign branch

## Canonical Logic

Use this exact flow:

```text
Base value -> Alias token reference -> Component token reference
```

Optional extended flow:

```text
Another Branding Theme raw value -> Base mode alias bridge -> Alias token reference -> Component token reference
```

Examples:

- `color/bg/brand-primary`
  - one visual mode -> `color/brand-primary/9`
  - another visual mode -> `color/brand-primary-dark/9`

- `color/graphic/accent/9`
  - one visual mode -> `color/accent/9`
  - another visual mode -> `color/accent-dark/9`

- `button/bg/primary`
  - component mode -> `color/bg/brand-primary`

- optional alternate-brand bridge
  - `00 Another Branding Theme`
    - `color/brand/9`
    - `color/brand-secondary/9`
    - `color/brand-alpha/9`
    - `color/brand-dark/9`
  - one mode in `00 Base Color`
    - `color/brand-primary/9` -> alias to `color/brand/9`
    - `color/brand-secondary/9` -> alias to `color/brand-secondary/9`
    - `color/brand-primary-alpha/9` -> alias to `color/brand-alpha/9`
    - `color/brand-primary-dark/9` -> alias to `color/brand-dark/9`
  - `01 Alias`
    - still points to `00 Base Color`

## Workbook Notes

- `Base` is the only place that should carry raw color values.
- `Alias` and `Component` should remain linked-token layers.
- The workbook uses simple link-style relationships. Preserve the visible token names rather than flattening them into hardcoded color values during normal Figma sync.
- If one theme or brand diverges from another, trust only the rows that explicitly show that divergence. Do not extrapolate beyond the rows present in the workbook.
- If an optional alternate-brand collection exists, it should stay as a raw-value collection while `00 Base Color` acts as the bridge layer for the affected theme mode.

## Validation Samples

Use these as quick sanity checks:

- Base token:
  - `color/brand-primary/9`
- optional bridge check:
  - one Base mode aliases `color/brand-primary/9` to a token in `00 Another Branding Theme`
- Alias tokens:
  - `color/bg/brand-primary`
  - `color/text/primary`
  - `color/graphic/primary/9`
- Component tokens:
  - `button/bg/primary`
  - `input/text/value`
  - `toast/bg/error`
