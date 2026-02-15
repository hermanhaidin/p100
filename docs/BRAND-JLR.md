# Jaguar Land Rover brand overrides

Brand-specific token values for Jaguar Land Rover (JLR) — colors and typography. Spacing, radius, stroke, blur, shadows, and breakpoints remain canonical.

For canonical values, see [P100-GUIDELINES.md](P100-GUIDELINES.md). For resolver architecture and file layout, see [P100-TOKEN-SCHEMA.md — Whitelabeling](P100-TOKEN-SCHEMA.md#whitelabeling--brand-overrides).

JLR gets its own complete `colors.resolver.json` and `typography.resolver.json` — same structure as canonical, different values. Tables below show full JLR values across all modes. The generator diffs these against canonical to populate the resolver's base set and theme/mode contexts.

## Color tokens

### Content colors

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/content/primary` | #0C121C | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/content/secondary` | #4A4F54 | #AEB0B3 | #AEB0B3 | #AEB0B3 | #AEB0B3 | #AEB0B3 |
| `colors/content/tertiary` | #AEB0B3 | #4A4F54 | #4A4F54 | #4A4F54 | #4A4F54 | #4A4F54 |

---

### On content colors

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/onContent/onPrimary` | #FFFFFF | #0C121C | #0C121C | #0C121C | #0C121C | #0C121C |
| `colors/onContent/onSecondary` | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/onContent/onTertiary` | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |

---

### Extended content colors

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/contentExtended/softBrand` | #E9ECEC | #0D2642 | #0D2642 | #0D2642 | #0D2642 | #0D2642 |
| `colors/contentExtended/brand` | #0C121C | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/contentExtended/strongBrand` | #0C121C | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/contentExtended/softInfo` | #EEF6FF | #0D2642 | #0D2642 | #0D2642 | #0D2642 | #0D2642 |
| `colors/contentExtended/info` | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 |
| `colors/contentExtended/strongInfo` | #1D5490 | #88B8F6 | #88B8F6 | #88B8F6 | #88B8F6 | #88B8F6 |
| `colors/contentExtended/softAccent` | #EEF6FF | #0D2642 | #0D2642 | #0D2642 | #0D2642 | #0D2642 |
| `colors/contentExtended/accent` | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 |
| `colors/contentExtended/strongAccent` | #1D5490 | #88B8F6 | #88B8F6 | #88B8F6 | #88B8F6 | #88B8F6 |
| `colors/contentExtended/softSuccess` | #E9F7EF | #022A14 | #022A14 | #022A14 | #022A14 | #022A14 |
| `colors/contentExtended/success` | #0F8A47 | #0F8A47 | #0F8A47 | #0F8A47 | #0F8A47 | #0F8A47 |
| `colors/contentExtended/strongSuccess` | #015A2B | #2FAB64 | #2FAB64 | #2FAB64 | #2FAB64 | #2FAB64 |
| `colors/contentExtended/softWarning` | #FFF4E5 | #402200 | #402200 | #402200 | #402200 | #402200 |
| `colors/contentExtended/warning` | #FF7F00 | #FF7F00 | #FF7F00 | #FF7F00 | #FF7F00 | #FF7F00 |
| `colors/contentExtended/strongWarning` | #995000 | #FFA347 | #FFA347 | #FFA347 | #FFA347 | #FFA347 |
| `colors/contentExtended/softError` | #FFF1F2 | #3A0003 | #3A0003 | #3A0003 | #3A0003 | #3A0003 |
| `colors/contentExtended/error` | #D2000A | #F94D55 | #F94D55 | #F94D55 | #F94D55 | #F94D55 |
| `colors/contentExtended/strongError` | #A80008 | #FF8A8E | #FF8A8E | #FF8A8E | #FF8A8E | #FF8A8E |

---

### On extended content colors

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/onContentExtended/onBrand` | #FFFFFF | #0C121C | #0C121C | #0C121C | #0C121C | #0C121C |
| `colors/onContentExtended/onInfo` | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/onContentExtended/onAccent` | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/onContentExtended/onSuccess` | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/onContentExtended/onWarning` | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/onContentExtended/onError` | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |

---

### Surface colors

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/surface/canvas` | #FFFFFF | #0C121C | #0C121C | #0C121C | #0C121C | #0C121C |
| `colors/surface/secondaryCanvas` | #F8F9F9 | #171D26 | #171D26 | #1E232D | #171D26 | #1E232D |
| `colors/surface/container` | #FFFFFF | #1E232D | #1E232D | #242831 | #1E232D | #242831 |
| `colors/surface/secondaryContainer` | #E9ECEC | #242831 | #242831 | #292E37 | #242831 | #292E37 |

---

### Glass material

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/glass/clear` | #FFFFFF at 1% opacity | #000000 at 1% opacity | #000000 at 1% opacity | #000000 at 1% opacity | #000000 at 1% opacity | #000000 at 1% opacity |
| `colors/glass/ultraThin` | #FFFFFF at 13% opacity | #000000 at 13% opacity | #000000 at 13% opacity | #000000 at 13% opacity | #000000 at 13% opacity | #000000 at 13% opacity |
| `colors/glass/thin` | #FFFFFF at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity |
| `colors/glass/regular` | #FFFFFF at 55% opacity | #000000 at 55% opacity | #000000 at 55% opacity | #000000 at 55% opacity | #000000 at 55% opacity | #000000 at 55% opacity |
| `colors/glass/thick` | #FFFFFF at 78% opacity | #000000 at 78% opacity | #000000 at 78% opacity | #000000 at 78% opacity | #000000 at 78% opacity | #000000 at 78% opacity |

---

### Overlays

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/overlay/hover` | #000000 at 5% opacity | #FFFFFF at 5% opacity | #FFFFFF at 5% opacity | #FFFFFF at 5% opacity | #FFFFFF at 5% opacity | #FFFFFF at 5% opacity |
| `colors/overlay/pressed` | #000000 at 8% opacity | #000000 at 8% opacity | #000000 at 8% opacity | #000000 at 8% opacity | #000000 at 8% opacity | #000000 at 8% opacity |
| `colors/overlay/disabled` | #FFFFFF at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity | #000000 at 34% opacity |
| `colors/overlay/focus` | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 | #4A90E2 |
| `colors/overlay/shimmer` | #E9ECEC | #292E37 | #292E37 | #323843 | #292E37 | #323843 |
| `colors/overlay/secondaryShimmer` | #DBDDDE | #323843 | #323843 | #3A4048 | #323843 | #3A4048 |
| `colors/overlay/dimming` | #000000 at 21% opacity | #000000 at 34% opacity | #000000 at 21% opacity | #000000 at 34% opacity | #000000 at 21% opacity | #000000 at 34% opacity |

---

### Headline accent colors

> Canonical SIXT: used for "SIXT share" and "SIXT subscribe". For brand overrides (JLR, BMW, Arval), these fall back to `content/primary`.

| Token | Prime Light | Prime Dark | Option Light | Option Dark | Accent Light | Accent Dark |
|-------|-------------|------------|--------------|-------------|--------------|-------------|
| `colors/headline/lilac` | #0C121C | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/headline/blue` | #0C121C | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/headline/green` | #0C121C | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |
| `colors/headline/yellow` | #0C121C | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF | #FFFFFF |

Loyalty program colors and global colors are not overridden by JLR.


## Gradient tokens

Gradient tokens reference semantic color tokens for their stops. With JLR color overrides applied, gradients adapt automatically — no gradient-specific overrides needed.


## Typography tokens

JLR uses different font families and weights. Font sizes, line heights, letter spacing, and text transforms remain canonical.

### Display text

| Token | Family | Weight |
|-------|--------|--------|
| `display/large/heavy` | Land Rover Web | Bold (700) |
| `display/large/heavyCaps` | Land Rover Web | Bold (700) |
| `display/large/regular` | Land Rover Web | Light (300) |
| `display/large/regularCaps` | Land Rover Web | Light (300) |
| `display/medium/heavy` | Land Rover Web | Bold (700) |
| `display/medium/heavyCaps` | Land Rover Web | Bold (700) |
| `display/medium/regular` | Land Rover Web | Light (300) |
| `display/medium/regularCaps` | Land Rover Web | Light (300) |
| `display/small/heavy` | Land Rover Web | Bold (700) |
| `display/small/heavyCaps` | Land Rover Web | Bold (700) |
| `display/small/regular` | Land Rover Web | Light (300) |
| `display/small/regularCaps` | Land Rover Web | Light (300) |

---

### Title text

| Token | Family | Weight |
|-------|--------|--------|
| `title/large/heavy` | Land Rover Web | Bold (700) |
| `title/large/heavyCaps` | Land Rover Web | Bold (700) |
| `title/large/regular` | Land Rover Web | Light (300) |
| `title/large/regularCaps` | Land Rover Web | Light (300) |
| `title/medium/heavy` | Land Rover Web | Bold (700) |
| `title/medium/heavyCaps` | Land Rover Web | Bold (700) |
| `title/medium/regular` | Land Rover Web | Light (300) |
| `title/medium/regularCaps` | Land Rover Web | Light (300) |
| `title/small/heavy` | Land Rover Web | Bold (700) |
| `title/small/heavyCaps` | Land Rover Web | Bold (700) |
| `title/small/regular` | Land Rover Web | Light (300) |
| `title/small/regularCaps` | Land Rover Web | Light (300) |

---

### Copy text

| Token | Family | Weight |
|-------|--------|--------|
| `copy/xLarge/heavy` | Avenir Next | Demi Bold (600) |
| `copy/xLarge/heavyCaps` | Avenir Next | Demi Bold (600) |
| `copy/xLarge/heavyTight` | Avenir Next | Demi Bold (600) |
| `copy/xLarge/regular` | Avenir Next | Regular (400) |
| `copy/xLarge/regularCaps` | Avenir Next | Regular (400) |
| `copy/xLarge/regularTight` | Avenir Next | Regular (400) |
| `copy/large/heavy` | Avenir Next | Demi Bold (600) |
| `copy/large/heavyCaps` | Avenir Next | Demi Bold (600) |
| `copy/large/heavyTight` | Avenir Next | Demi Bold (600) |
| `copy/large/regular` | Avenir Next | Regular (400) |
| `copy/large/regularCaps` | Avenir Next | Regular (400) |
| `copy/large/regularTight` | Avenir Next | Regular (400) |
| `copy/medium/heavy` | Avenir Next | Demi Bold (600) |
| `copy/medium/heavyCaps` | Avenir Next | Demi Bold (600) |
| `copy/medium/heavyTight` | Avenir Next | Demi Bold (600) |
| `copy/medium/regular` | Avenir Next | Regular (400) |
| `copy/medium/regularCaps` | Avenir Next | Regular (400) |
| `copy/medium/regularTight` | Avenir Next | Regular (400) |
| `copy/small/heavy` | Avenir Next | Demi Bold (600) |
| `copy/small/heavyCaps` | Avenir Next | Demi Bold (600) |
| `copy/small/heavyTight` | Avenir Next | Demi Bold (600) |
| `copy/small/regular` | Avenir Next | Regular (400) |
| `copy/small/regularCaps` | Avenir Next | Regular (400) |
| `copy/small/regularTight` | Avenir Next | Regular (400) |

---

### Email

Email design for JLR is not in scope. All email-mode typography remains canonical.