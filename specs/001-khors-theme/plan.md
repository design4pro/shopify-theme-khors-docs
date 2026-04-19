# Implementation Plan: Khors Premium Shopify Theme

**Branch**: `001-khors-theme` | **Date**: 2026-02-06 | **Spec**: [specs/001-khors-theme/spec.md](./spec.md)
**Input**: Feature specification from `/specs/001-khors-theme/spec.md`

## Summary

Khors is a premium Shopify theme targeting Theme Store submission with three industry presets (Aura/Beauty, Apex/Electronics, Nexus/Home & Garden). The theme requires 25+ homepage sections, 7 product configurations, 3-level navigation, rich media support (3D/AR/Video), selling plans, local pickup, and unit pricing — all built on Shopify OS 2.0 with JSON templates, CSS BEM/Layers architecture, and vanilla JavaScript within a 16KB budget.

The implementation follows a 12-phase roadmap spanning Foundation → Design System → Header/Footer → Homepage Sections → Product Page → Collection Page → Cart/Checkout → Blog/Content → Advanced Features → Presets → Performance/A11y → Testing/Submission. Phases 01-02 are complete (Foundation + Design System), Phase 03 is ~14% complete (Header/Footer), and Phases 04-12 remain pending.

The technical approach uses Shopify's native Liquid templating with progressive enhancement: server-rendered HTML with CSS-only interactions where possible, vanilla JS only when native features are insufficient. The CSS Layers architecture (`@layer reset, base, components, utilities`) is established. All section schemas use `t:` translation keys, all snippets require LiquidDoc headers, and all blocks follow the BEM naming convention.

## Technical Context

**Language/Version**: Liquid (Shopify OS 2.0), CSS3 (Layers + Custom Properties), Vanilla JavaScript (ES6+)
**Primary Dependencies**: Shopify CLI 3.0, Shopify Liquid, Shopify Storefront Filtering API, Shopify Predictive Search API, Shopify model-viewer (3D/AR)
**Storage**: Shopify-managed (product/collection/content data via Liquid objects, settings via JSON)
**Testing**: `shopify theme check` (linting), Lighthouse CI (performance/a11y/SEO), manual testing matrix (7 breakpoints × 7 product configs = 49 combinations)
**Target Platform**: Shopify Theme Store (all modern browsers, 320px–2560px responsive)
**Project Type**: Web (Shopify theme — single codebase, no build step)
**Performance Goals**: Lighthouse 90+ all categories, LCP < 2.5s, CLS < 0.1, JS ≤ 16KB gzipped
**Constraints**: Zero `shopify theme check` errors/warnings, WCAG 2.1 AA, no external JS dependencies, no CSS frameworks, single `<h1>` per page, 131 Theme Store checklist items
**Scale/Scope**: 30+ sections, 20+ blocks, 25+ snippets, 3 presets, 11+ JSON templates, 25 homepage sections minimum

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Evidence |
|-----------|--------|----------|
| **I. One Codebase, Multiple Configurations** | COMPLIANT | Single theme codebase with 3 presets via `settings_data.json`. CSS variables for single-property, CSS classes for multi-property settings. No preset-specific code files. |
| **II. Shopify OS 2.0 Standards** | COMPLIANT | All templates are JSON (11 .json files). Sections use `{% schema %}`. Snippets have `{% doc %}` headers. `{% stylesheet %}` and `{% javascript %}` used for component styles/scripts. |
| **III. Coding Standards** | COMPLIANT | CSS uses BEM naming, mobile-first `min-width` queries, max 1-level nesting, no `!important`, no ID selectors, no `&` operator. JS is vanilla only, native features preferred. Liquid uses `{% liquid %}` for multiline. |
| **IV. Theme Check Compliance** | COMPLIANT | Zero-tolerance policy enforced. `shopify theme check` must pass before every commit. All existing files pass theme check. |
| **V. Git Workflow** | COMPLIANT | Feature branches from `develop`, PRs to `develop` only. `main` branch is protected. Conventional commits format used. Branch pattern: `task/X.X-feature-name`. |
| **VI. Quality Gates** | COMPLIANT | Theme Check: zero offenses. Responsive: 320px–2560px (7 breakpoints). Accessibility: WCAG 2.1 AA. Performance: Lighthouse 90+. |

## Project Structure

### Documentation (this feature)

```text
specs/001-khors-theme/
├── plan.md              # This file (/speckit.plan command output)
├── spec.md              # Feature specification (10 stories, 60 FR, 14 SC)
├── research.md          # Phase 0 output (technology decisions)
├── data-model.md        # Phase 1 output (7 entity mappings)
├── quickstart.md        # Phase 1 output (dev setup guide)
├── contracts/           # Phase 1 output (interface contracts)
│   ├── sections.md      # Section schema contracts
│   ├── snippets.md      # Snippet parameter contracts (LiquidDoc)
│   ├── javascript.md    # JS API contracts (events, classes)
│   └── translations.md  # Translation key structure
├── checklists/
│   └── requirements.md  # 45/45 items passing
└── tasks.md             # Phase 2 output (/speckit.tasks - NOT created by /speckit.plan)
```

### Source Code (repository root)

```text
khors-theme/
├── assets/                    # Static files (CSS, JS, SVG icons)
│   ├── critical.css           # @layer reset, base — render-blocking critical styles
│   ├── components.css         # @layer components — shared component foundations
│   ├── utilities.css          # @layer utilities — single-purpose utility classes
│   ├── icon-account.svg       # Account icon
│   ├── icon-cart.svg          # Cart icon
│   └── shoppy-x-ray.svg      # Placeholder illustration
│
├── blocks/                    # Nestable UI components with {% schema %}
│   ├── _accordion-item.liquid # Private accordion item block
│   ├── _tab-item.liquid       # Private tab item block
│   ├── accordion.liquid       # Accordion container block
│   ├── badge.liquid           # Badge display block
│   ├── button.liquid          # Button block (delegates to snippets/button.liquid)
│   ├── group.liquid           # Block grouping container
│   ├── heading.liquid         # Heading text block
│   ├── icon.liquid            # Icon display block
│   ├── image-block.liquid     # Image display block
│   ├── rating.liquid          # Star rating block
│   ├── tabs.liquid            # Tabs container block
│   └── text.liquid            # Rich text block
│
├── config/                    # Theme configuration
│   ├── settings_schema.json   # Global theme settings (typography, colors, layout)
│   └── settings_data.json     # Current setting values (preset data)
│
├── layout/                    # Page wrappers
│   ├── theme.liquid           # Main layout (head, body, sections groups)
│   └── password.liquid        # Password page layout
│
├── locales/                   # Translations
│   ├── en.default.json        # English translations (storefront)
│   └── en.default.schema.json # English translations (theme editor)
│
├── sections/                  # Full-width page modules
│   ├── 404.liquid             # 404 error page section
│   ├── article.liquid         # Blog article section
│   ├── blog.liquid            # Blog listing section
│   ├── cart.liquid             # Cart page section
│   ├── collection.liquid      # Collection page section
│   ├── collections.liquid     # Collection list section
│   ├── custom-section.liquid  # Custom/generic section
│   ├── design-system-showcase.liquid # Design system demo (dev only)
│   ├── footer.liquid          # Footer section
│   ├── header.liquid          # Header with nav, logo, cart, account
│   ├── hello-world.liquid     # Placeholder (to be replaced)
│   ├── page.liquid            # Generic page section
│   ├── password.liquid        # Password page section
│   ├── product.liquid         # Product page section
│   └── search.liquid          # Search results section
│   # Planned: 15+ additional sections for homepage (slideshows, featured products,
│   # featured collections, image-with-text, newsletter, rich-text, blog-posts,
│   # video, unique industry sections, announcement-bar)
│
├── snippets/                  # Reusable fragments via {% render %}
│   ├── badge.liquid           # Badge rendering snippet
│   ├── breadcrumb.liquid      # Breadcrumb navigation
│   ├── button.liquid          # Button rendering (4 variants, 3 sizes)
│   ├── css-variables.liquid   # Design tokens + color schemes injection
│   ├── form-field.liquid      # Form field rendering
│   ├── header-logo.liquid     # Logo rendering (7 aspect ratios)
│   ├── header-nav.liquid      # Navigation rendering (3 levels)
│   ├── header-nav-dropdown.liquid # Dropdown submenu rendering
│   ├── icon.liquid            # SVG icon rendering
│   ├── image.liquid           # Responsive image rendering
│   ├── meta-tags.liquid       # SEO meta tags (OG, Twitter)
│   ├── pagination.liquid      # Pagination rendering
│   ├── placeholder.liquid     # Placeholder/empty state rendering
│   ├── price.liquid           # Price display (regular, compare-at, unit)
│   ├── rating.liquid          # Star rating display
│   ├── skeleton-loader.liquid # Loading skeleton animation
│   └── social-links.liquid    # Social media links (8 platforms)
│   # Planned: 8+ additional snippets (product-card, variant-selector,
│   # cart-item, search-result, video-player, model-viewer, json-ld, share-links)
│
├── templates/                 # JSON page templates
│   ├── 404.json
│   ├── article.json
│   ├── blog.json
│   ├── cart.json
│   ├── collection.json
│   ├── index.json             # Homepage (currently 1 section, needs 25+)
│   ├── list-collections.json
│   ├── page.json
│   ├── password.json
│   ├── product.json
│   └── search.json
│   # Planned: page.contact.json, gift_card.liquid
│
├── sections/                  # Section groups (OS 2.0)
│   ├── header-group.json      # Header section group
│   └── footer-group.json      # Footer section group
│
└── listings/                  # Preset configurations (planned)
    ├── aura/
    │   ├── listing.json
    │   └── templates/
    ├── apex/
    │   ├── listing.json
    │   └── templates/
    └── nexus/
        ├── listing.json
        └── templates/
```

**Structure Decision**: Shopify theme — flat directory structure mandated by Shopify OS 2.0. No build step. Sections, blocks, and snippets are the primary component model. CSS uses Layers architecture across 3 files. JavaScript will be added as `assets/*.js` files loaded via `<script defer>`.

## Data Model

Seven entities from the specification mapped to Shopify's Liquid object model. See [data-model.md](./data-model.md) for full entity details.

| Entity | Shopify Mapping | Access Pattern |
|--------|----------------|----------------|
| **Preset** | `settings_data.json` presets + `listings/` directory | `settings.*` in Liquid, `listing.json` for Theme Store |
| **Section** | `sections/*.liquid` with `{% schema %}` | `section.settings.*`, `section.blocks` |
| **Block** | `blocks/*.liquid` with `{% schema %}` | `block.settings.*`, `block.shopify_attributes` |
| **Product Configuration** | `product` Liquid object | `product.variants`, `product.options`, `product.media` |
| **Color Scheme** | `settings_schema.json` color_scheme type | `settings.color_schemes`, section-level `color_scheme` setting |
| **Variant** | `product.variants` collection | `variant.price`, `variant.available`, `variant.sku` |
| **Selling Plan** | `product.selling_plan_groups` | `selling_plan_group.selling_plans`, `selling_plan.price_adjustments` |

## Contracts

Interface contracts define the API surface between components. See [contracts/](./contracts/) for full details.

### Section Schemas (see [contracts/sections.md](./contracts/sections.md))

Every section MUST define:
- `name` using `t:` translation key
- `settings` array with typed settings
- `blocks` array (usually `[{ "type": "@theme" }]` for theme blocks)
- `presets` array with at least one default preset

### Snippet Parameters (see [contracts/snippets.md](./contracts/snippets.md))

Every snippet MUST have:
- `{% doc %}` header with description, `@param` types, and `@example`
- Parameters passed via `{% render 'name', param: value %}`
- No global variable access (Liquid render scope isolation)

### JavaScript APIs (see [contracts/javascript.md](./contracts/javascript.md))

JS modules communicate via:
- Custom events on `document` (`khors:cart:updated`, `khors:variant:changed`, etc.)
- Web Components with `#private` methods
- `<script defer>` loading, no module bundling

### Translation Keys (see [contracts/translations.md](./contracts/translations.md))

Two locale files:
- `en.default.json` — storefront-facing text (`{{ 'key' | t }}`)
- `en.default.schema.json` — theme editor labels (`"label": "t:key"`)

## Quickstart

See [quickstart.md](./quickstart.md) for full development environment setup.

```bash
# Prerequisites: Node.js 18+, Shopify CLI 3.0, Ruby 3.0+

# Clone and setup
git clone <repo-url> && cd khors-theme
git checkout develop

# Connect to development store
shopify theme dev --store khors-theme-design4pro.myshopify.com

# Lint theme
shopify theme check

# Push changes
shopify theme push --store khors-theme-design4pro.myshopify.com
```

## Complexity Tracking

No constitution violations exist. All principles are COMPLIANT.

### Hotspots

| Area | Complexity | Mitigation |
|------|-----------|------------|
| Variant selector (100 variants) | High — combinatorial option states | Pre-compute availability matrix in Liquid, event-driven JS updates |
| 3D/AR media | Medium — Shopify model-viewer dependency | Use Shopify's native `<model-viewer>` web component, lazy load |
| Selling plans + compare-at pricing | Medium — dual pricing display | Dedicated `price.liquid` snippet handles all price states |
| 25 homepage sections | High — volume | Modular section pattern with shared block types (`@theme`) |
| 3 preset configurations | Medium — testing surface | Single codebase, presets are JSON-only configuration swaps |
| Predictive search (500ms target) | Medium — performance | Debounced fetch, abort controller, result caching |

### JavaScript Budget Allocation

| Module | Estimated Size | Purpose |
|--------|---------------|---------|
| Variant selector | ~3 KB | Option change → price/image/availability updates |
| Cart drawer (AJAX) | ~3 KB | Add to cart, quantity update, remove |
| Slideshow controller | ~2 KB | Autoplay, navigation, accessibility |
| Predictive search | ~2 KB | Debounced fetch, result rendering |
| Media (3D/AR/Video) | ~2 KB | Lazy load, play/pause controls |
| Utilities (events, DOM) | ~1 KB | Shared helpers, custom events |
| **Total** | **~13 KB** | **Within 16 KB budget** |
