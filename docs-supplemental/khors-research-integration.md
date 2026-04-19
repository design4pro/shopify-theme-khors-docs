# Khors Design System — Research Integration

> Extracted design tokens from analyzed Shopify themes, mapped to Khors CSS variables.

---

## 📊 Current Khors Design Tokens

### Colors (from `snippets/css-variables.liquid`)

| Token | Default | Usage |
|-------|---------|-------|
| `--color-background` | `#FFFFFF` | Page background |
| `--color-foreground` | `#121212` | Primary text |
| `--color-secondary-background` | `#F3F3F3` | Cards, sections |
| `--color-border` | `#E5E5E5` | Borders, dividers |
| `--color-accent` | `#0066CC` | Links, CTAs |
| `--color-accent-hover` | `#004C99` | Accent hover |

### Typography

| Token | Default | Source |
|-------|---------|--------|
| `--font-primary` | `work_sans_n4` | Body text |
| `--font-heading` | `work_sans_n4` | Headings |

### Spacing (CSS custom properties)

| Token | Default |
|-------|---------|
| `--space-1` | `0.25rem` |
| `--space-2` | `0.5rem` |
| `--space-3` | `0.75rem` |
| `--space-4` | `1rem` |
| `--space-6` | `1.5rem` |
| `--space-8` | `2rem` |
| `--space-12` | `3rem` |
| `--space-16` | `4rem` |

---

## 🎨 Elegance Theme Analysis

### Color Palette (Art/Gallery Industry)

| Color | Hex | Usage |
|-------|-----|-------|
| Primary | `#1A1A1A` | Text, strong contrast |
| Secondary | `#666666` | Muted text |
| Accent | `#C9A962` | Gold accent (Art/Gallery vibe) |
| Background | `#FFFFFF` | Clean gallery feel |
| Surface | `#F8F7F5` | Warm off-white (canvas feel) |

### Typography Observations

- **Headings:** Elegant serif or refined sans-serif
- **Body:** Clean, highly readable
- **Accent text:** Subtle uppercase with letter-spacing

### Layout Patterns

1. **Hero:** Full-width imagery with minimal text overlay
2. **Product grid:** Generous whitespace, 3-column on desktop
3. **Product detail:** Large imagery, sticky sidebar on desktop
4. **Navigation:** Mega menu with imagery support

---

## 🔄 Research → Khors Mapping

### Feature Implementation Priority

| Feature (Elegance) | Khors Section/Snippet | Status |
|--------------------|----------------------|--------|
| Mega Menu | `snippets/header-nav-dropdown.liquid` | 🔴 TO DO |
| Image Zoom (hover) | `snippets/product-gallery.liquid` | ⚠️ Basic, needs enhancement |
| Quick View | `snippets/quick-view.liquid` | ✅ Exists |
| Color Swatches | `snippets/color-swatch.liquid` | ✅ Exists |
| Sticky Header | `sections/header.liquid` | ✅ Exists |
| Trust Badges | — | 🔴 TO DO |
| Countdown Timer | — | 🔴 TO DO |
| Stock Counter | — | 🔴 TO DO |
| Image Rollover | `snippets/collection-card.liquid` | ⚠️ Partial |
| Slideshow | `sections/slideshow.liquid` | ✅ Exists (3 variants) |
| Product Filtering | `sections/collection.liquid` | ✅ Exists |
| Recently Viewed | — | 🔴 TO DO |

---

## 🎯 Design Direction per Industry

### Fashion (Primary)

**Vibe:** Editorial, clean, image-forward

**Colors:**
- Background: `#FFFFFF`
- Text: `#1A1A1A`
- Accent: `#000000` (black) or `#DC2626` (sale red)
- Muted: `#6B7280`

**Typography:**
- Headings: Bold, tight letter-spacing
- Body: Regular weight, generous line-height

**Layout:**
- Large hero imagery
- 4-column product grid on desktop
- Minimal whitespace between grid items

### Beauty (Secondary)

**Vibe:** Soft, luxurious, visual-first

**Colors:**
- Background: `#FDFCFA` (warm white)
- Text: `#1A1A1A`
- Accent: `#B8860B` (golden) or `#8B5A8B` (soft purple)
- Surface: `#F5F0EB` (cream)

**Typography:**
- Headings: Elegant, slightly wider letter-spacing
- Body: Light weight, airy

**Layout:**
- Generous padding
- Rounded corners (8px+)
- Soft shadows

### Electro (Tertiary)

**Vibe:** Technical, data-rich, efficient

**Colors:**
- Background: `#FFFFFF`
- Text: `#1A1A1A`
- Accent: `#0066CC` (electric blue)
- Secondary: `#F3F4F6` (light gray surfaces)
- Success: `#059669`

**Typography:**
- Headings: Medium weight, clear hierarchy
- Body: Technical, precise

**Layout:**
- Dense information display
- Comparison tables
- Filter-heavy collections

---

## 📋 Next Steps

1. [ ] **Mega Menu** — Create `header-mega-menu.liquid` snippet
2. [ ] **Trust Badges** — Create `trust-badges.liquid` section
3. [ ] **Countdown Timer** — Create countdown block/section
4. [ ] **Image Zoom Enhancement** — Improve `product-gallery.liquid` zoom
5. [ ] **Stock Counter** — Add to product page
6. [ ] **Recently Viewed** — Create section for homepage

---

## 🔗 Related Files

- Theme: `~/dev/projects/design4.pro/shopify/khors-theme/`
- Research: `~/dev/shopify/research/`
- Screenshot tool: `npx playwright screenshot --browser chromium --full-page {URL} {output}.png`

---

*Auto-generated from market research*