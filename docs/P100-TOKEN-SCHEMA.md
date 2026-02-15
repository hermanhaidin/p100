# P100 token schema

This document is the source of truth for how P100 design tokens are expressed as DTCG JSON files — file layout, resolver architecture, types, and override patterns. Always generate from docs, not the other way around.

For token values and usage guidelines, see [P100-GUIDELINES.md](P100-GUIDELINES.md). For Figma-specific structure (variable scopes, text style wiring, publishing rules), see [P100-FIGMA-TOKENS.md](P100-FIGMA-TOKENS.md).


## File layout

All token files live under `tokens/` folder. The canonical brand is `sixt/`; brand variants go in `brands/<brand>/`.

| File | Format | DTCG Type | Description |
|------|--------|-----------|-------------|
| `sixt/colors.resolver.json` | Resolver | `color` | Semantic colors across 6 theme modes |
| `sixt/typography.resolver.json` | Resolver | `string`, `dimension` | Typography primitives + text style overrides across 4 responsive modes |
| `sixt/size.json` | Plain DTCG | `dimension` | Spacing, radius, stroke, blur |
| `sixt/breakpoints.json` | Plain DTCG | `dimension` | Viewport range min/max per breakpoint |
| `sixt/gradients.json` | Plain DTCG | `gradient` | Radial gradients referencing color token paths |
| `sixt/shadows.json` | Plain DTCG | `shadow` | Multi-layer drop shadows for elevation |
| `brands/<brand>/colors.resolver.json` | Resolver | `color` | Brand-specific colors (same structure as canonical) |
| `brands/<brand>/typography.resolver.json` | Resolver | `string`, `dimension` | Brand-specific typography (same structure as canonical) |
| `manifest.json` | — | — | File index for the Figma plugin |

**Resolver vs plain DTCG**: collections with multiple modes (Colors, Typography) use the DTCG resolver format — a base set plus sparse modifier contexts. Single-mode collections (Size, Breakpoints) and non-variable tokens (Gradients, Shadows) use plain DTCG.

Brand resolvers share the same structure as canonical — only values differ. Files that don't change across brands (size, breakpoints, gradients, shadows) are shared from `sixt/`.


## Mode ID mapping

Figma uses Title Case for collection and mode labels. DTCG resolver contexts use camelCase.

| Figma Collection | Figma Mode | Resolver Context | Modifier |
|------------------|------------|------------------|----------|
| Colors | `Prime Light` | `primeLight` | `theme` |
| Colors | `Prime Dark` | `primeDark` | `theme` |
| Colors | `Option Light` | `optionLight` | `theme` |
| Colors | `Option Dark` | `optionDark` | `theme` |
| Colors | `Accent Light` | `accentLight` | `theme` |
| Colors | `Accent Dark` | `accentDark` | `theme` |
| Typography | `Mobile` | `mobile` | `mode` |
| Typography | `Tablet` | `tablet` | `mode` |
| Typography | `Desktop` | `desktop` | `mode` |
| Typography | `Email` | `email` | `mode` |
| Size | `Value` | — | No resolver (plain DTCG) |


## Colors resolver

### Architecture

The colors resolver contains all semantic color tokens.

- **Base set**: all semantic tokens at their `primeLight` values. No primitive tonal palettes — semantic tokens only.
- **`theme` modifier**: 6 contexts, one per Figma mode. `primeLight` is empty (base already has those values). The other 5 contexts contain sparse overrides — only tokens whose value differs from the base.
- **`contrast` modifier**: reserved for future accessibility use. Single `default` context (empty).

Brand variants get their own complete colors resolver with the same structure but different values.

---

### Resolution order

```
base → theme → contrast
```

---

### Example structure

```json
{
  "sets": {
    "base": {
      "sources": [{
        "colors": {
          "content": {
            "primary": { "$type": "color", "$value": "#1A1A1A" }
          },
          "surface": {
            "canvas": { "$type": "color", "$value": "#FFFFFF" }
          }
        }
      }]
    }
  },
  "modifiers": {
    "theme": {
      "contexts": {
        "primeLight": [],
        "primeDark": [{
          "colors": {
            "content": {
              "primary": { "$type": "color", "$value": "#FFFFFF" }
            },
            "surface": {
              "canvas": { "$type": "color", "$value": "#1A1A1A" }
            }
          }
        }]
      },
      "default": "primeLight"
    },
    "contrast": {
      "contexts": { "default": [] },
      "default": "default"
    }
  },
  "resolutionOrder": [
    { "$ref": "#/sets/base" },
    { "$ref": "#/modifiers/theme" },
    { "$ref": "#/modifiers/contrast" }
  ]
}
```

The example above is abbreviated — the full base set contains all semantic tokens, and each non-default theme context contains only tokens that differ from `primeLight`.

Tokens are nested by group under a `colors` root (e.g. `colors/content/primary`). Color values use hex (`#RRGGBB`) or hex with alpha (`#RRGGBBAA`).


## Typography resolver

### Architecture

The typography resolver has two top-level sections in its base set:

1. `typography` — primitive variables (fontFamily, fontWeight, fontSize, lineHeight, letterSpacing) at their mobile/default values.
2. `textStyles` — sparse per-style property overrides for text styles that differ from what their role primitives would give them.

`textStyles` concept: most text styles inherit all properties from their role primitives (e.g. `display/large/heavy` uses the `display` fontFamily). But some styles override a specific property — for example, `display/large/regular` uses `Helvetica Now Text` instead of the display role's `Helvetica Now Display`. These exceptions are captured in `textStyles` as sparse overrides.

`mode` modifier: 4 contexts, one per Figma mode. `mobile` is empty (base is mobile). `tablet` and `desktop` override `fontSize` and `lineHeight` only. `email` overrides all groups: `fontFamily`, `fontWeight`, `fontSize`, `lineHeight`, `letterSpacing`.

Brand variants get their own complete typography resolver with the same structure but different values.

---

### Resolution order

```
base → mode
```

---

### Example structure

```json
{
  "sets": {
    "base": {
      "sources": [{
        "typography": {
          "fontFamily": {
            "display": { "$type": "string", "$value": "Helvetica Now Display" }
          },
          "fontWeight": {
            "display": { "$type": "string", "$value": "Regular" }
          },
          "fontSize": {
            "largeDisplay": { "$type": "dimension", "$value": { "value": 60, "unit": "px" } }
          }
        },
        "textStyles": {
          "display": {
            "large": {
              "regular": {
                "fontFamily": { "$type": "string", "$value": "Helvetica Now Text" }
              }
            }
          }
        }
      }]
    }
  },
  "modifiers": {
    "mode": {
      "contexts": {
        "mobile": [],
        "tablet": [{
          "typography": {
            "fontSize": {
              "largeDisplay": { "$type": "dimension", "$value": { "value": 68, "unit": "px" } }
            },
            "lineHeight": {
              "largeDisplay": { "$type": "dimension", "$value": { "value": 68, "unit": "px" } }
            }
          }
        }],
        "desktop": [{ }],
        "email": [{ }]
      },
      "default": "mobile"
    }
  },
  "resolutionOrder": [
    { "$ref": "#/sets/base" },
    { "$ref": "#/modifiers/mode" }
  ]
}
```

---

### DTCG types

| Group | DTCG Type |
|-------|-----------|
| `fontFamily` | `string` (e.g. `Helvetica Now Display`) |
| `fontWeight` | `string` (e.g. `Regular`, `Bold`, `Cn Blk`) |
| `fontSize` | `dimension` (px) |
| `lineHeight` | `dimension` (px) |
| `letterSpacing` | `dimension` (px) |


## Size and breakpoints

Both are plain DTCG — single mode, no resolver.

### Size

Tokens are grouped under `spacing`, `radius`, `stroke`, `blur`. All values are `$type: dimension` with `unit: px`.

```json
{
  "spacing": {
    "5xs": { "$type": "dimension", "$value": { "value": 2, "unit": "px" } }
  },
  "radius": {
    "xs": { "$type": "dimension", "$value": { "value": 4, "unit": "px" } }
  }
}
```

---

### Breakpoints

Each breakpoint has `min` and `max` values in px. All values are `$type: dimension` with `unit: px`. Tokens are grouped under `web` and `email` to match layout guide usage.

```json
{
  "web": {
    "xs": {
      "min": { "$type": "dimension", "$value": { "value": 320, "unit": "px" } },
      "max": { "$type": "dimension", "$value": { "value": 649, "unit": "px" } }
    }
  },
  "email": {
    "xs": {
      "min": { "$type": "dimension", "$value": { "value": 320, "unit": "px" } },
      "max": { "$type": "dimension", "$value": { "value": 649, "unit": "px" } }
    }
  }
}
```


## Gradients

Plain DTCG, no modes.

Each token is a two-stop radial gradient. Gradient tokens reference semantic color token paths — they adapt to theme automatically through the color resolver.

### Structure per token

- **Type**: `gradient`
- **Two stops**: inner at 10% (base color at 30% opacity), outer at 100% (transparent via `colors/glass/clear`)
- **Position**: `0% 0%` (topLeading) or `100% 0%` (topTrailing)

```json
{
  "radialGradient": {
    "brandTopLeading": {
      "$type": "gradient",
      "$value": {
        "position": "0% 0%",
        "size": "100% 100%",
        "stops": [
          { "position": "10%", "color": "{colors.contentExtended.brand}", "opacity": 0.3 },
          { "position": "100%", "color": "{colors.glass.clear}" }
        ]
      }
    }
  }
}
```


## Shadows

Plain DTCG, no modes.

Each elevation token is two drop shadow layers.

### Structure per token

- **Type**: `shadow`, `$value`: array of two layer objects
- **Dimensions**: use `{ value, unit }` per DTCG spec
- **Colors**: use hex with alpha (`#RRGGBBAA`) — same format as color tokens

```json
{
  "elevation": {
    "small": {
      "$type": "shadow",
      "$value": [
        {
          "offsetX": { "value": 0, "unit": "px" },
          "offsetY": { "value": 2, "unit": "px" },
          "blur": { "value": 6, "unit": "px" },
          "spread": { "value": 0, "unit": "px" },
          "color": "#0000001A"
        },
        {
          "offsetX": { "value": 0, "unit": "px" },
          "offsetY": { "value": 1, "unit": "px" },
          "blur": { "value": 4, "unit": "px" },
          "spread": { "value": 0, "unit": "px" },
          "color": "#00000014"
        }
      ]
    }
  }
}
```


## Whitelabeling

P100 supports brand variants (whitelabeling). Brands change **values**, not structure — same token keys, same collections, same modes.

Each brand gets its own **complete resolver files** for colors and typography. These are generated from a brand override doc (e.g. [BRAND-JLR.md](BRAND-JLR.md)) by diffing brand values against canonical and placing them in the correct base set and modifier contexts.

Files that don't change across brands (size, breakpoints, gradients, shadows) are shared from the canonical `sixt/` folder.

### Rules

- Brand resolvers must have the **same structure** as canonical: same token keys, same modifier contexts, same resolution order
- Brand resolvers must not introduce new token keys, modes, or modifiers
- Brand override docs specify full values across all modes; the generator diffs against canonical to produce resolvers
- Gradients adapt automatically — they reference color token paths, so brand color values propagate without gradient-specific changes
- Keep brand changes in brand-isolated PRs for clean diffs and review

---

### File layout per brand

```
tokens/
  sixt/                               ← canonical (SIXT)
    colors.resolver.json
    typography.resolver.json
    size.json                         ← shared across brands
    breakpoints.json                  ← shared across brands
    gradients.json                    ← shared across brands
    shadows.json                      ← shared across brands
  brands/
    jaguar-landrover/                 ← per-brand resolvers only
      colors.resolver.json
      typography.resolver.json
  manifest.json
```

---

### Figma library model

Each brand is a separate Figma library file (e.g. "P100 Foundations" for SIXT, "JLR Foundations" for Jaguar Land Rover). Both libraries have identical variable names, collection names, and mode names. A shared "P100 Components" library references the canonical foundation; designers swap foundation libraries to get brand-specific values.


## DTCG 2025.10 compliance

This project targets the [DTCG 2025.10 stable spec](https://www.designtokens.org/TR/2025.10/) (Format + Resolver modules). Known deviations:

| Area | DTCG 2025.10 | P100 | Reason |
|------|--------------|------|--------|
| Color `$value` | Object: `{ colorSpace, components, hex }` | Plain hex string (`"#1A1A1A"` / `"#RRGGBBAA"`) | Figma API returns hex; simpler for tooling; applies to color tokens and shadow color fields |
| Gradient schema | `gradient` composite | Custom `{ position, size, stops }` | DTCG gradient type is underspecified; it's a known gap they acknowledge |
| Font weight `$type` | `number` (100–900) | `string` (e.g. `"Cn Blk"`, `"Demi Bold"`) | Some weights carry information numeric values can't express (e.g. `Cn Blk` encodes condensed width + black weight); Figma font styles require string names |


## Generating from docs

JSON files are derived from these docs, not vice versa. To regenerate all JSON files from scratch:

1. Read **this doc** for the resolver structure, file layout, and DTCG types
2. Read [P100-GUIDELINES.md](P100-GUIDELINES.md) for all token values across modes
3. Read [P100-FIGMA-TOKENS.md](P100-FIGMA-TOKENS.md) for the Figma structure and text style to typography variable wiring table (needed to derive the `textStyles` overrides in the typography resolver)
4. Read the brand override docs (e.g. [BRAND-JLR.md](BRAND-JLR.md)) for brand-specific values