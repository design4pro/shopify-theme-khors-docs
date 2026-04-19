# Research: Khors Premium Shopify Theme

**Branch**: `001-khors-theme` | **Date**: 2026-02-06 | **Phase**: 0 (Research)
**Status**: Complete — all decisions resolved, zero NEEDS CLARIFICATION markers

## Overview

This document captures the technology decisions and research findings for the Khors Premium Shopify Theme implementation. All items were resolved during the specification phase — no outstanding clarifications remain.

## Technology Decisions

### 1. Template System: Shopify OS 2.0 JSON Templates

**Decision**: Use JSON templates exclusively (no Liquid templates except `gift_card.liquid`).

**Rationale**: JSON templates are required for Shopify OS 2.0, enabling merchants to add/remove/reorder sections through the theme editor. This is mandatory for Theme Store acceptance. The `gift_card.liquid` exception exists because Shopify does not support JSON templates for gift card pages.

**Alternatives Rejected**:
- Liquid templates: Legacy approach, doesn't support section groups or theme editor customization.

### 2. CSS Architecture: CSS Layers + BEM + Custom Properties

**Decision**: Three CSS files using `@layer` cascade control with BEM naming convention and CSS custom properties for design tokens.

**Rationale**:
- `@layer reset, base` in `critical.css` (preloaded, render-blocking) — establishes foundation
- `@layer components` in `components.css` — shared component foundations
- `@layer utilities` in `utilities.css` — single-purpose utility classes
- CSS custom properties injected via `snippets/css-variables.liquid` for color schemes, typography, and spacing
- BEM naming (`.block__element--modifier`) for predictable specificity

**Alternatives Rejected**:
- Tailwind CSS: External dependency, violates constitution (no CSS frameworks)
- CSS Modules: Not supported in Shopify Liquid environment
- Sass: Build step required, unnecessary complexity

### 3. JavaScript Strategy: Progressive Enhancement + Vanilla JS

**Decision**: Zero JS for basic functionality. Vanilla ES6+ for interactive enhancements only. 16KB gzipped budget. `<script defer>` loading.

**Rationale**: Shopify Theme Store requires performance (Lighthouse 90+). Progressive enhancement ensures pages work without JS. Native browser features (popover, details/summary, CSS scroll-snap) replace JS where possible.

**Key JS Modules** (estimated 13KB total):
- Variant selector (~3KB): Option change, price/image/availability updates
- Cart drawer (~3KB): AJAX add-to-cart, quantity updates
- Slideshow controller (~2KB): Autoplay, navigation, a11y
- Predictive search (~2KB): Debounced fetch, result rendering
- Media controller (~2KB): 3D/AR/Video lazy loading, controls
- Utilities (~1KB): Custom events, DOM helpers

**Alternatives Rejected**:
- React/Vue/Svelte: Framework overhead exceeds 16KB budget alone
- jQuery: Deprecated, unnecessary with modern ES6+
- Module bundler (Webpack/Vite): No build step to maintain simplicity

### 4. Component Model: Sections + Blocks + Snippets

**Decision**: Follow Shopify's native component hierarchy:
- **Sections**: Full-width page modules with `{% schema %}` for settings and blocks
- **Blocks**: Nestable components within sections, also with `{% schema %}`
- **Snippets**: Reusable rendering fragments via `{% render %}` with LiquidDoc headers

**Rationale**: Shopify's component model is the only option for Theme Store themes. The key architecture decision is the delegation pattern: blocks provide theme editor configuration UI while snippets handle rendering logic (e.g., `blocks/button.liquid` configures settings, `snippets/button.liquid` renders HTML). This enables reuse — the same snippet renders in both block and direct-render contexts.

### 5. Color System: Shopify Native Color Schemes

**Decision**: Use Shopify's native `color_scheme` setting type with 3 preset schemes per industry preset (9 total). Sections can assign color schemes individually.

**Rationale**: Native color scheme support integrates with Shopify's theme editor. CSS custom properties (`--color-background`, `--color-text`, etc.) are set per-section based on the selected scheme. This satisfies FR-048 (native color schemes) and SC-007 (4.5:1 contrast ratio per scheme).

**Implementation**:
- `settings_schema.json` defines color scheme settings
- `snippets/css-variables.liquid` converts settings to CSS custom properties
- Sections include a `color_scheme` setting referencing the scheme selector

### 6. Navigation: 3-Level Mega Menu with Mobile Drawer

**Decision**: CSS-driven desktop mega menu (3 levels), JS-enhanced mobile drawer. Progressive enhancement — navigation works without JS via native `<details>` elements.

**Rationale**: FR-012 requires 3 levels, 10+ top-level items, 30-60 character titles. PRD recommends mega menu with promotional images. Mobile drawer is standard for touch devices.

**Implementation**:
- Desktop: `<details>`/`<summary>` for disclosure, CSS for positioning
- Mobile: Off-canvas drawer with focus trap (JS required for a11y)
- `snippets/header-nav.liquid` + `snippets/header-nav-dropdown.liquid` handle rendering

### 7. Rich Media: Shopify Native model-viewer + Video APIs

**Decision**: Use Shopify's native `<model-viewer>` web component for 3D/AR. Standard `<video>` element for hosted video. YouTube/Vimeo via lite embeds.

**Rationale**: Shopify provides `<model-viewer>` with AR support built in. No custom 3D code needed. For video, native `<video>` element with poster images and lazy loading minimizes JS overhead.

### 8. Search: Shopify Predictive Search API

**Decision**: Use Shopify's Predictive Search API (`/search/suggest.json`) for live suggestions. Standard search results page for full results.

**Rationale**: The Predictive Search API is the official Shopify solution, returning products, collections, pages, and articles. It satisfies FR-041 (predictive suggestions) and SC-012 (500ms response target).

**Implementation**:
- Debounced input handler (300ms)
- AbortController for request cancellation
- Result caching for repeated queries
- Keyboard navigation for accessibility

### 9. Cart: AJAX Cart Drawer

**Decision**: AJAX-powered cart drawer using Shopify Cart API (`/cart.js`, `/cart/add.js`, `/cart/change.js`). Fallback to full page cart for no-JS.

**Rationale**: AJAX cart is standard for premium themes. The Cart API is well-documented and reliable. Progressive enhancement ensures the cart page works without JS.

### 10. Presets: JSON Configuration Only

**Decision**: Three presets (Aura, Apex, Nexus) implemented entirely through `settings_data.json` presets and `listings/` directory structure. No preset-specific Liquid code.

**Rationale**: Constitution principle I mandates single codebase, multiple configurations. Presets differ only in: color schemes, typography selections, section ordering in templates, and listing metadata. The `listings/` directory provides Theme Store with preset-specific template configurations.

### 11. Structured Data: JSON-LD via Snippet

**Decision**: Server-side rendered JSON-LD via `snippets/json-ld.liquid` for Product, Offer, BreadcrumbList, and Organization entities.

**Rationale**: JSON-LD is the preferred structured data format for SEO. Server-side rendering ensures search engines can parse it without JS execution. FR-060 requires these specific entity types.

### 12. Accessibility: WCAG 2.1 Level AA

**Decision**: Full WCAG 2.1 AA compliance through semantic HTML, ARIA attributes, keyboard navigation, focus management, and 4.5:1 contrast ratios.

**Rationale**: Theme Store requires accessibility compliance. SC-006 mandates 100% keyboard operability. SC-007 mandates 4.5:1 contrast. This is non-negotiable.

**Key Implementation Areas**:
- Skip-to-content link (already in `theme.liquid`)
- Focus trap in modals/drawers
- `aria-live` regions for dynamic content (cart updates, search results)
- Visible focus indicators on all interactive elements
- Semantic landmarks (`<nav>`, `<main>`, `<article>`, `<aside>`)

## Resolved Clarifications

All specification items were resolved during the `speckit.specify` phase. The following were potential ambiguities that were pre-resolved:

| Area | Resolution |
|------|-----------|
| Quick View implementation | Modal (not drawer) — better UX for product preview |
| Pagination options | All three: numbered with truncation, "Load More" button, infinite scroll (configurable per section) |
| Slideshow max slides | 12 (exceeds typical 10, provides merchant flexibility) |
| Lighthouse target | 90+ (above minimum 60, premium positioning) |
| Filtering approach | Dual: Storefront Filtering API (modern) + tag-based (legacy fallback) |
| Video section count | 2 minimum (standard + background variant) |
| Unique sections | 5 minimum: Ingredient Spotlight, Tech Specs Comparison, Room Visualizer, Before/After Slider, Testimonials |
| Cart implementation | Drawer (AJAX) as primary, full page as fallback |
| Color swatches | Native Shopify swatches + custom color metafield support |
| Announcement bar | Part of header section group, supports text + rich text + links |
