# P100 token structure in Figma

This document describes how design tokens are organized in the **P100 Design System** Figma library (used at SIXT) — collections, modes, styles, and naming.

For token values and usage guidelines, see [P100-GUIDELINES.md](P100-GUIDELINES.md).


## Mental model

Tokens are expressed in Figma via two primitives:

- **Figma variables**: typed values (color, number, string) grouped into variable collections with modes
- **Figma styles**: higher-level artifacts that can reference variables (text styles, effect styles, color styles for gradients, layout guide styles)


## Mode reference

Exact mode IDs for the Figma API:

| Collection | Mode IDs |
|------------|----------|
| Colors | `Prime Light`, `Prime Dark`, `Option Light`, `Option Dark`, `Accent Light`, `Accent Dark` |
| Typography | `Mobile`, `Tablet`, `Desktop`, `Email` |
| Size | `Value` |

**Note**: token paths stay camelCase (e.g. `content/primary`, `fontFamily/display`, `spacing/5xs`); only the **collection** and **mode** labels are Title Case (see Mode reference above).


## Figma variables

### `Colors` collection

- **What it is**: flat (non-gradient) semantic colors
- **Modes**: `Prime Light`, `Prime Dark`, `Option Light`, `Option Dark`, `Accent Light`, `Accent Dark`

| Group | Tokens |
|-------|--------|
| `content/*` | `primary`, `secondary`, `tertiary` |
| `onContent/*` | `onPrimary`, `onSecondary`, `onTertiary` |
| `contentExtended/*` | `softBrand`, `brand`, `strongBrand`, `softInfo`, `info`, `strongInfo`, `softAccent`, `accent`, `strongAccent`, `softSuccess`, `success`, `strongSuccess`, `softWarning`, `warning`, `strongWarning`, `softError`, `error`, `strongError` |
| `onContentExtended/*` | `onBrand`, `onInfo`, `onAccent`, `onSuccess`, `onWarning`, `onError` |
| `surface/*` | `canvas`, `secondaryCanvas`, `container`, `secondaryContainer` |
| `glass/*` | `clear`, `ultraThin`, `thin`, `regular`, `thick` |
| `overlay/*` | `hover`, `pressed`, `disabled`, `focus`, `shimmer`, `secondaryShimmer`, `dimming` |
| `loyalty/*` | `silver`, `gold`, `platinum`, `diamond` |
| `headline/*` | `lilac`, `blue`, `green`, `yellow` |
| `global/*` | `black`, `sixtAnthracite`, `white`, `sixtOrange` |

**Example with values - `content/*`**

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `content/primary` | #1A1A1A | #FFFFFF | #FFFFFF | #FFFFFF | #1A1A1A | #1A1A1A |
| `content/secondary` | #656A6F | #8D9299 | #8D9299 | #8D9299 | #1A1A1A | #1A1A1A |
| `content/tertiary` | #D7DADC | #313234 | #313234 | #363739 | #1A1A1A | #1A1A1A |

---

### `Typography` collection

- **What it is**: typographic primitives used to wire text styles: `fontFamily/*`, `fontSize/*`, `fontWeight/*`, `lineHeight/*`, `letterSpacing/*`
- **Modes**: `Mobile`, `Tablet`, `Desktop`, `Email`
- **Responsiveness**: values like `fontSize/*` and `lineHeight/*` typically vary by mode; others (e.g. `fontWeight/*`) are often constant

| Group | Tokens |
|-------|--------|
| `fontFamily/*` | `display`, `title`, `copy` |
| `fontWeight/*` | `display`, `heavyDisplay`, `title`, `heavyTitle`, `copy`, `heavyCopy` |
| `fontSize/*` | `largeDisplay`, `mediumDisplay`, `smallDisplay`, `largeTitle`, `mediumTitle`, `smallTitle`, `xLargeCopy`, `largeCopy`, `mediumCopy`, `smallCopy` |
| `lineHeight/*` | `largeDisplay`, `mediumDisplay`, `smallDisplay`, `largeTitle`, `mediumTitle`, `smallTitle`, `xLargeCopy`, `xLargeTightCopy`, `largeCopy`, `largeTightCopy`, `mediumCopy`, `mediumTightCopy`, `smallCopy`, `smallTightCopy` |
| `letterSpacing/*` | `display`, `largeTitle`, `smallTitle`, `copy` |

**Example with values - `fontFamily/*`**

| Token | Mobile | Tablet | Desktop | Email |
|-------|--------|--------|---------|-------|
| `fontFamily/display` | Helvetica Now Display | Helvetica Now Display | Helvetica Now Display | Helvetica |
| `fontFamily/title` | Helvetica Now Text | Helvetica Now Text | Helvetica Now Text | Helvetica |
| `fontFamily/copy` | Helvetica Now Text | Helvetica Now Text | Helvetica Now Text | Helvetica |

---

### `Size` collection

- **What it is**: size primitives used across layout and effects
- **Modes**: `Value`

| Group | Tokens |
|-------|--------|
| `spacing/*` | `5xs`, `4xs`, `3xs`, `2xs`, `xs`, `sm`, `md`, `lg`, `xl`, `2xl`, `3xl`, `4xl`, `5xl`, `6xl` |
| `radius/*` | `xs`, `sm`, `md`, `lg`, `xl`, `pill` |
| `stroke/*` | `sm`, `md`, `lg`, `xl` |
| `blur/*` | `glass` |

**Example with values - `blur/*`**

| Token | Value |
|-------|-------|
| `blur/glass` | 30 |

---

### Variable scopes

We use variable scopes to prevent unrelated tokens from showing up in the wrong picker contexts (e.g. radius tokens appearing in auto-layout gap pickers).

- **String scope**
  - `fontFamily/*`: font family
  - `fontWeight/*`: font weight or style
- **Typography scope**
  - `fontSize/*`: font size
  - `lineHeight/*`: line height
  - `letterSpacing/*`: letter spacing
- **Number scope**
  - `spacing/*`: auto layout gap / spacing values
  - `radius/*`: corner radius
  - `stroke/*`: stroke width
  - `blur/*`: effects

**Exception**: for convenience, all color variables are allowed in all scopes in Figma.


## Figma styles

### Color styles (gradients)

Gradients are **color styles** in Figma because variables cannot contain gradients. All current gradients are **radial gradients with two stops**.

**Figma implementation**: both stops use variable colors from the `Colors` collection. Fill opacity (30%) is applied at the *color style* level, not per stop — Figma does not support stop-level opacity when using variable colors.

| Group | Tokens |
|-------|--------|
| `radialGradient/*` | `brandTopLeading`, `brandTopTrailing`, `infoTopLeading`, `infoTopTrailing`, `accentTopLeading`, `accentTopTrailing`, `successTopLeading`, `successTopTrailing`, `silverTopLeading`, `silverTopTrailing`, `goldTopLeading`, `goldTopTrailing`, `platinumTopLeading`, `platinumTopTrailing`, `diamondTopLeading`, `diamondTopTrailing` |

**Example with values - `radialGradient/brandTopLeading`**

| Token | Fill | Type | Stop 1 | Stop 2 |
|-------|------|------|--------|--------|
| `radialGradient/brandTopLeading` | Gradient at 30% opacity | Radial | 10% `contentExtended/brand` | 100% `glass/clear` |

---

### Effect styles (blur + elevation)

**Blur**: background blur references `blur/glass` variable in `Size` collection; combine with `colors/glass/*` for frosted glass look.

| Group | Tokens |
|-------|--------|
| `blur/*` | `glass` |

**Elevation**: each style uses two drop shadow layers.

| Group | Tokens |
|-------|--------|
| `elevation/*` | `small`, `medium`, `large` |

---

### Text styles (typography)

Typography is applied primarily through **text styles**, not by directly using typography variables in designs.

Each text style wires multiple typography variables into its properties:

- `fontFamily/*`
- `fontSize/*`
- `fontWeight/*`
- `lineHeight/*`
- `letterSpacing/*`

**Constraint**: Figma does not support variables for `textTransform`, so some styles hardcode `text-transform: uppercase`. When present, this is reflected in the style name (e.g. `display/large/heavyCaps`).

Text styles are organized as `role/size/presentation` (e.g. `display/large/heavy`, `copy/medium/regularTight`).

**Text style → Typography variable mapping** — each text style wires these variables (paths are relative to `Typography` collection):

| Text Style | fontFamily | fontSize | fontWeight | lineHeight | letterSpacing |
|------------|------------|----------|------------|------------|---------------|
| `display/large/heavy` | display | largeDisplay | heavyDisplay | largeDisplay | display |
| `display/large/heavyCaps` | display | largeDisplay | heavyDisplay | largeDisplay | display |
| `display/large/regular` | title | largeDisplay | display | largeDisplay | display |
| `display/large/regularCaps` | title | largeDisplay | display | largeDisplay | display |
| `display/medium/heavy` | display | mediumDisplay | heavyDisplay | mediumDisplay | display |
| `display/medium/heavyCaps` | display | mediumDisplay | heavyDisplay | mediumDisplay | display |
| `display/medium/regular` | title | mediumDisplay | display | mediumDisplay | display |
| `display/medium/regularCaps` | title | mediumDisplay | display | mediumDisplay | display |
| `display/small/heavy` | display | smallDisplay | heavyDisplay | smallDisplay | display |
| `display/small/heavyCaps` | display | smallDisplay | heavyDisplay | smallDisplay | display |
| `display/small/regular` | title | smallDisplay | display | smallDisplay | display |
| `display/small/regularCaps` | title | smallDisplay | display | smallDisplay | display |
| `title/large/heavy` | display | largeTitle | heavyTitle | largeTitle | largeTitle |
| `title/large/heavyCaps` | display | largeTitle | heavyTitle | largeTitle | largeTitle |
| `title/large/regular` | title | largeTitle | title | largeTitle | largeTitle |
| `title/large/regularCaps` | title | largeTitle | title | largeTitle | largeTitle |
| `title/medium/heavy` | display | mediumTitle | heavyTitle | mediumTitle | largeTitle |
| `title/medium/heavyCaps` | display | mediumTitle | heavyTitle | mediumTitle | largeTitle |
| `title/medium/regular` | title | mediumTitle | title | mediumTitle | largeTitle |
| `title/medium/regularCaps` | title | mediumTitle | title | mediumTitle | largeTitle |
| `title/small/heavy` | title | smallTitle | heavyTitle | smallTitle | smallTitle |
| `title/small/heavyCaps` | title | smallTitle | heavyTitle | smallTitle | smallTitle |
| `title/small/regular` | title | smallTitle | title | smallTitle | smallTitle |
| `title/small/regularCaps` | title | smallTitle | title | smallTitle | smallTitle |
| `copy/xLarge/heavy` | copy | xLargeCopy | heavyCopy | xLargeCopy | copy |
| `copy/xLarge/heavyCaps` | copy | xLargeCopy | heavyCopy | xLargeCopy | copy |
| `copy/xLarge/heavyTight` | copy | xLargeCopy | heavyCopy | xLargeTightCopy | copy |
| `copy/xLarge/regular` | copy | xLargeCopy | copy | xLargeCopy | copy |
| `copy/xLarge/regularCaps` | copy | xLargeCopy | copy | xLargeCopy | copy |
| `copy/xLarge/regularTight` | copy | xLargeCopy | copy | xLargeTightCopy | copy |
| `copy/large/heavy` | copy | largeCopy | heavyCopy | largeCopy | copy |
| `copy/large/heavyCaps` | copy | largeCopy | heavyCopy | largeCopy | copy |
| `copy/large/heavyTight` | copy | largeCopy | heavyCopy | largeTightCopy | copy |
| `copy/large/regular` | copy | largeCopy | copy | largeCopy | copy |
| `copy/large/regularCaps` | copy | largeCopy | copy | largeCopy | copy |
| `copy/large/regularTight` | copy | largeCopy | copy | largeTightCopy | copy |
| `copy/medium/heavy` | copy | mediumCopy | heavyCopy | mediumCopy | copy |
| `copy/medium/heavyCaps` | copy | mediumCopy | heavyCopy | mediumCopy | copy |
| `copy/medium/heavyTight` | copy | mediumCopy | heavyCopy | mediumTightCopy | copy |
| `copy/medium/regular` | copy | mediumCopy | copy | mediumCopy | copy |
| `copy/medium/regularCaps` | copy | mediumCopy | copy | mediumCopy | copy |
| `copy/medium/regularTight` | copy | mediumCopy | copy | mediumTightCopy | copy |
| `copy/small/heavy` | copy | smallCopy | heavyCopy | smallCopy | copy |
| `copy/small/heavyCaps` | copy | smallCopy | heavyCopy | smallCopy | copy |
| `copy/small/heavyTight` | copy | smallCopy | heavyCopy | smallTightCopy | copy |
| `copy/small/regular` | copy | smallCopy | copy | smallCopy | copy |
| `copy/small/regularCaps` | copy | smallCopy | copy | smallCopy | copy |
| `copy/small/regularTight` | copy | smallCopy | copy | smallTightCopy | copy |

**Note**: Within a role, fontFamily can differ by style — e.g. display/heavy uses Helvetica Now Display, display/regular uses Helvetica Now Text. The wiring table above captures these overrides.

---

### Layout guide styles

Layout guide styles help align UI elements across common screen sizes. Style names include the range for less cognitive load (e.g. `xs (320...649px)`).

| Group | Tokens |
|-------|--------|
| `web` | `xs (320...649px)`, `sm (650...899px)`, `md (900...1199px)`, `lg (1200...1599px)`, `xl (1600...2560px)` |
| `email` | `xs (320...649px)`, `sm (650...2560px)` |


## Publishing rules

- Typography variables are not published from the `typography` variable collection.
- Designers consume typography via **text styles**, which already carry the correct variable wiring.