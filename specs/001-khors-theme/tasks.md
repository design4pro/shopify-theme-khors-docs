# Tasks: Khors Premium Shopify Theme

**Input**: Design documents from `/specs/001-khors-theme/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

> **Note**: This is the authoritative Spec Kit task list.

**Tests**: Not included — TDD was not requested for this feature.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Phase 1: Setup (COMPLETE)

**Purpose**: Foundation and Design System — Phases 01-02 fully completed

All foundation tasks (CSS Layers, design tokens, typography, color schemes, spacing) and design system components (button, badge, heading, text, icon, image, accordion, tabs, rating, form-field, pagination, skeleton-loader, placeholder, breadcrumb) are complete. No tasks remain.

**Checkpoint**: Foundation ready — implementation can proceed

---

## Phase 2: Foundational — Header & Footer (Phase 03 Remaining)

**Purpose**: Complete Header/Footer infrastructure that blocks homepage sections and product pages

**⚠️ CRITICAL**: Logo (3.2) and Navigation (3.3) are already complete. Remaining 11 task groups must finish before homepage sections can be fully tested.

- [x] T001 [US1] Rebuild header section schema with layout, sticky, transparent, background, border, padding settings in `sections/header.liquid` (FR-013)
- [x] T002 [P] [US1] Create mega menu snippet with featured image/collection/product slots, multi-column layout, and animation in `snippets/header-mega-menu.liquid` (FR-012)
- [x] T003 [P] [US1] Create mobile drawer snippet with slide-in animation, focus trap, overlay, Escape/swipe close, accordion menus, account/cart links in `snippets/header-drawer.liquid` (FR-012)
- [x] T004 [P] [US5] Create predictive search snippet with Shopify API integration, results for products/collections/pages/articles, keyboard navigation in `snippets/header-search.liquid` (FR-041)
- [x] T005 [P] [US1] Create cart icon snippet with dynamic count badge, AJAX update, add-to-cart animation in `snippets/header-cart-icon.liquid` (FR-013)
- [x] T006 [US1] Rebuild footer section with 5+ configurable columns, background, padding, border, copyright in `sections/footer.liquid` (FR-014)
- [x] T007 [P] [US1] Create footer newsletter snippet with email validation, AJAX submission, honeypot spam protection, success/error messaging in `snippets/footer-newsletter.liquid` (FR-014, FR-007)
- [x] T008 [P] [US1] Create footer social icons snippet for 8 platforms with inline SVG, accessibility labels in `snippets/footer-social.liquid` (FR-014)
- [x] T009 [P] [US1] Create footer payment icons snippet with auto-detection via `payment_type_svg_tag` filter in `snippets/footer-payment.liquid` (FR-014)
- [x] T010 [P] [US1] Create announcement bar section with rich text, link, dismissible option, color scheme in `sections/announcement-bar.liquid` (FR-015)
- [x] T011 [US1] Create header JavaScript module for mobile menu, mega menu, search toggle, sticky header, cart updates, focus management (≤2KB gzipped) in `assets/header.js` (FR-013)
- [x] T012 [US1] Add announcement bar to header-group.json and configure default in `sections/header-group.json`
- [x] T013 [US1] Add translation keys for header, footer, announcement bar, search, and cart in `locales/en.default.json` and `locales/en.default.schema.json`

**Checkpoint**: Header & Footer complete — homepage and product page work can begin

---

## Phase 3: User Story 1 — Browse and Discover Products (Priority: P1) 🎯 MVP

**Goal**: Homepage with 25+ configurable sections, 3-level navigation, responsive 320px–2560px

**Independent Test**: Load homepage at all 7 breakpoints, confirm all 25 sections render, navigate 3 menu levels, verify footer links/social

### Foundational Snippets

- [x] T014 [P] [US1] Create product card snippet with hover image swap, sale/sold-out/new badges, quick add, color swatch preview in `snippets/product-card.liquid` (FR-003, FR-029)
- [x] T015 [P] [US1] Create collection card snippet with image fallback, title, product count in `snippets/collection-card.liquid` (FR-004)
- [x] T016 [P] [US1] Create slide snippet for slideshow blocks with heading, subheading, description, button, content positioning, overlay in `snippets/slide.liquid` (FR-002)
- [x] T017 [P] [US1] Create video player snippet supporting YouTube, Vimeo, MP4 with lazy loading, click-to-play, poster image in `snippets/video-player.liquid` (FR-010)

### Slideshow Sections (3 required — FR-002)

- [x] T018 [P] [US1] Create standard slideshow section with up to 12 slides, autoplay, arrows, dots, pause/play, 7 aspect ratios, mobile images in `sections/slideshow.liquid`
- [x] T019 [P] [US1] Create split slideshow section with 50/50 image-content layout, reversible positioning in `sections/slideshow-split.liquid`
- [x] T020 [P] [US1] Create Ken Burns slideshow section with CSS-only zoom/pan animation, reduced-motion support in `sections/slideshow-kenburns.liquid`

### Featured Product Sections (5 required — FR-003)

- [x] T021 [P] [US1] Create featured product section (single) with full details, add-to-cart form, media in `sections/featured-product.liquid`
- [x] T022 [P] [US1] Create featured products grid section with 2–4 columns, 4–16 products, badges in `sections/featured-products-grid.liquid`
- [x] T023 [P] [US1] Create featured products carousel section with swipe, 2–6 items per view, navigation controls in `sections/featured-products-carousel.liquid`
- [x] T024 [P] [US1] Create featured products tabs section with multiple collections loaded via AJAX in `sections/featured-products-tabs.liquid`
- [x] T025 [P] [US1] Create featured products masonry section with CSS Grid mixed-size layout in `sections/featured-products-masonry.liquid`

### Featured Collection Sections (3 required — FR-004, FR-005)

- [x] T026 [P] [US1] Create featured collection section with banner image, product preview, link in `sections/featured-collection.liquid`
- [x] T027 [P] [US1] Create collections grid section with collection cards, configurable columns in `sections/collections-grid.liquid`
- [x] T028 [P] [US1] Create collection list section supporting 10+ collections with horizontal scroll in `sections/collection-list.liquid`

### Image with Text Sections (3 required — FR-006)

- [x] T029 [P] [US1] Create image with text section with side-by-side layout, reversible positioning in `sections/image-with-text.liquid`
- [x] T030 [P] [US1] Create image with text overlay section with full-width image, 9 content positions in `sections/image-with-text-overlay.liquid`
- [x] T031 [P] [US1] Create image with text parallax section with CSS-only scroll effect in `sections/image-with-text-parallax.liquid`

### Core Sections (FR-007, FR-008, FR-009)

- [x] T032 [P] [US1] Create newsletter section with email input, AJAX submission, validation, success/error messaging in `sections/newsletter.liquid`
- [x] T033 [P] [US1] Create rich text section supporting 1000+ characters, h2–h6 headings, lists, bold/italic, links in `sections/rich-text.liquid`
- [x] T034 [P] [US1] Create blog posts section with article card snippet, grid/carousel layout, configurable count in `sections/blog-posts.liquid`
- [x] T035 [P] [US1] Create article card snippet with title, featured image, excerpt, date, author in `snippets/article-card.liquid`

### Video Sections (2 required — FR-010)

- [x] T036 [P] [US1] Create video section with YouTube/Vimeo/MP4 support, controls, poster image in `sections/video.liquid`
- [x] T037 [P] [US1] Create video background section with muted autoplay, mobile fallback image in `sections/video-background.liquid`

### Unique Industry Sections (5 required — FR-051 to FR-055)

- [x] T038 [P] [US1] Create ingredient spotlight section (Aura/beauty) with ingredient blocks, image, benefits, hover/click detail in `sections/ingredient-spotlight.liquid` (FR-052)
- [x] T039 [P] [US1] Create tech specs comparison section (Apex/electronics) with product blocks, side-by-side table, mobile-friendly in `sections/tech-specs-comparison.liquid` (FR-053)
- [x] T040 [P] [US1] Create room visualizer section (Nexus/home-garden) with room image, product overlay positioning in `sections/room-visualizer.liquid` (FR-054)
- [x] T041 [P] [US1] Create before/after slider section with draggable comparison, keyboard accessible in `sections/before-after-slider.liquid` (FR-055)
- [x] T042 [P] [US1] Create testimonials section with author, text, rating, avatar blocks, Schema.org markup in `sections/testimonials.liquid` (FR-051)

### Homepage Assembly

- [x] T043 [US1] Configure homepage template with all 25+ sections in default order in `templates/index.json` (FR-001)
- [x] T044 [US1] Add all section translation keys to `locales/en.default.json` and `locales/en.default.schema.json`
- [x] T045 [US1] Verify all 25 sections render empty states when no content configured (FR-058)

**Checkpoint**: Homepage with 25+ sections fully functional at all breakpoints

---

## Phase 4: User Story 2 — Purchase a Product (Priority: P2)

**Goal**: Complete product page with gallery, variants, cart, 7 product configurations

**Independent Test**: Create 7 test products, navigate each, interact with variants, add to cart, verify prices

### Product Media Gallery (FR-020, FR-021)

- [x] T046 [P] [US2] Create product media gallery snippet with main image, thumbnails, zoom, lazy loading in `snippets/product-gallery.liquid`
- [x] T047 [P] [US2] Create 3D model viewer snippet integrating Shopify model-viewer for 360° rotation, touch gestures in `snippets/model-viewer.liquid` (FR-021)
- [x] T048 [P] [US2] Create AR button snippet with iOS Quick Look / Android Scene Viewer, device detection in `snippets/ar-button.liquid` (FR-021)
- [x] T049 [US2] Create mixed media gallery coordinator handling images, 3D, AR, video with type detection and transitions in `snippets/product-media.liquid` (FR-020)

### Variant Selection (FR-017)

- [x] T050 [P] [US2] Create variant selector snippet with dropdown and radio/swatch display styles in `snippets/variant-selector.liquid`
- [x] T051 [P] [US2] Create color swatch snippet with native Shopify swatches, sold-out/unavailable states, tooltips in `snippets/color-swatch.liquid`
- [x] T052 [US2] Create variant change JavaScript with dynamic price/image/SKU/availability updates, URL History API in `assets/variant-selector.js` (≤3KB gzipped)
- [x] T053 [US2] Implement unavailable combination detection disabling invalid option combos in `assets/variant-selector.js` (FR-017)

### Product Form (FR-018, FR-019)

- [x] T054 [P] [US2] Create quantity selector snippet with plus/minus buttons, direct input, inventory min/max in `snippets/quantity-selector.liquid` (FR-018)
- [x] T055 [US2] Create add-to-cart form with AJAX submission, loading states, success feedback, error handling in `snippets/product-form.liquid` (FR-018)
- [x] T056 [US2] Update price snippet to handle dynamic updates for compare-at, unit pricing, selling plan pricing in `snippets/price.liquid` (FR-019)

### Advanced Product Features (FR-022, FR-023, FR-024, FR-025)

- [x] T057 [P] [US2] Create local pickup snippet with Shopify API, 5+ locations, variant-aware availability in `snippets/local-pickup.liquid` (FR-022) ✅ 2026-02-14
- [x] T058 [P] [US2] Create selling plan selector snippet with one-time vs subscription toggle, price adjustments, savings in `snippets/selling-plan.liquid` (FR-023) ✅ 2026-02-14
- [x] T059 [P] [US2] Create product description snippet supporting 1000+ chars, collapsible rows, metafields in `snippets/product-description.liquid` (FR-025) ✅ 2026-02-14

### Product Section Assembly

- [x] T060 [US2] Rebuild product section with two-column layout, media left + content right, sticky sidebar, mobile stacking in `sections/product.liquid` (FR-016) ✅ 2026-02-14
- [x] T061 [US2] Implement product blocks system with 6 block types (title, price, variant picker, quantity, buy buttons, custom liquid) in `sections/product.liquid` ✅ 2026-02-14
- [x] T062 [US2] Create product page JavaScript module for variant selection, cart add, media, focus management (≤3KB gzipped) in `assets/product.js` ✅ 2026-02-14

### Cart (FR-031 to FR-035)

- [x] T063 [P] [US2] Create cart item snippet with image, title, variant info, price, quantity controls, remove in `snippets/cart-item.liquid` (FR-031) ✅ 2026-02-14
- [x] T064 [P] [US2] Create cart drawer snippet with slide-in panel, overlay, focus trap, header/items/footer structure in `snippets/cart-drawer.liquid` (FR-031) ✅ 2026-02-14
- [x] T065 [US2] Create AJAX cart JavaScript with Shopify Cart API (fetch, add, update, remove), custom events in `assets/cart.js` (≤3KB gzipped) (FR-032) ✅ 2026-02-15
- [x] T066 [US2] Implement cart totals display with subtotal, discounts, shipping estimate, taxes, dynamic updates in `snippets/cart-totals.liquid` (FR-033) ✅ 2026-02-15
- [x] T067 [US2] Implement discount code input with validation, apply/remove, success/error messaging in `snippets/cart-discount.liquid` (FR-033) ✅ 2026-02-15
- [x] T068 [US2] Implement cart notes, free shipping threshold progress bar, and cart recommendations in `snippets/cart-features.liquid` (FR-034) ✅ 2026-02-15
- [x] T069 [US2] Rebuild cart page section with full layout, same items/totals as drawer, continue shopping, no-JS fallback in `sections/cart.liquid` (FR-031) ✅ 2026-02-15
- [x] T070 [US2] Add cart and product translation keys to `locales/en.default.json` and `locales/en.default.schema.json` ✅ 2026-02-15
- [x] T071 [US2] Verify all 7 product configurations render correctly (single, sale, one-option, multi-option, three-option, 100-variant, no-image) (FR-016) ✅ 2026-02-15

**Checkpoint**: Product page + cart fully functional with all 7 product configurations

---

## Phase 5: User Story 5 — Search for Products (Priority: P5)

**Goal**: Predictive search suggestions + search results page with pagination

**Independent Test**: Type partial queries, verify suggestions, submit search, paginate, test no-results

- [x] T072 [US5] Create predictive search JavaScript with debounced fetch, abort controller, result caching (≤2KB) in `assets/search.js` (FR-041, SC-012)
- [x] T073 [US5] Create search result snippet for product/collection/page/article results in `snippets/search-result.liquid` (FR-042)
- [x] T074 [US5] Rebuild search results section with pagination, filter by type, no-results state with suggestions in `sections/search.liquid` (FR-042)
- [x] T075 [US5] Add search translation keys to `locales/en.default.json` and `locales/en.default.schema.json`
- [x] T076 [US5] Update search template to integrate search results section in `templates/search.json`

**Checkpoint**: Search fully functional with predictive suggestions and results page

---

## Phase 6: User Story 6 — Read Content and Engage (Priority: P6)

**Goal**: Blog listing, articles with comments, contact form, social sharing

**Independent Test**: Navigate blog, read articles, post comments, submit contact, use share links

- [x] T077 [P] [US6] Create share links snippet for Facebook, Twitter/X, Pinterest, Email with OG integration in `snippets/share-links.liquid` (FR-040)
- [x] T078 [P] [US6] Extend article card snippet with comment count display and blog-specific styling in `snippets/article-card.liquid` (FR-036)
- [x] T079 [US6] Rebuild blog listing section with post cards, tag filtering, pagination with truncation in `sections/blog.liquid` (FR-036)
- [x] T080 [US6] Rebuild article section with 1000+ char content, rich text formatting, embedded images, comments form in `sections/article.liquid` (FR-037, FR-038)
- [x] T081 [US6] Create contact page template with name, email, message fields, validation, success confirmation in `templates/page.contact.json` and update `sections/page.liquid` (FR-039)
- [x] T082 [US6] Add OG meta tags (og:title, og:description, og:image, og:url) to all shareable pages via `snippets/meta-tags.liquid` (FR-040, FR-045)
- [x] T083 [US6] Add blog, article, contact, and sharing translation keys to `locales/en.default.json` and `locales/en.default.schema.json`

**Checkpoint**: Blog, articles, comments, contact, and sharing fully functional

---

## Phase 7: User Story 3 + User Story 4 — Theme Identity & Content Management (Priority: P3, P4)

**Goal**: 3 industry presets with distinct identities, theme editor validation for 25 sections

**Independent Test**: Switch between presets, verify distinct colors/typography/styling, test all 25 sections in editor

### Preset Configuration (FR-046 to FR-050)

- [x] T084 [US3] Create Aura (Beauty/Wellness) preset with color palette, serif typography, soft styling in `config/settings_data.json` (FR-046)
- [x] T085 [US3] Create Apex (Electronics/Gadgets) preset with color palette, sans-serif typography, tech styling in `config/settings_data.json` (FR-046)
- [x] T086 [US3] Create Nexus (Home & Garden) preset with color palette, mixed typography, organic styling in `config/settings_data.json` (FR-046)
- [x] T087 [US3] Configure preset selection to apply full configuration without manual section adjustment (FR-047)
- [x] T088 [US3] Verify native Shopify color scheme support with multiple schemes assignable to sections (FR-048)
- [x] T089 [US3] Configure spacing and layout tokens in theme settings for consistent visual rhythm (FR-049)

### Listings Directory (FR-050)

- [x] T090 [P] [US3] Create Aura listing with `listing.json` metadata and template overrides in `listings/aura/`
- [x] T091 [P] [US3] Create Apex listing with `listing.json` metadata and template overrides in `listings/apex/`
- [x] T092 [P] [US3] Create Nexus listing with `listing.json` metadata and template overrides in `listings/nexus/`

### Content Management Validation (US4)

- [x] T093 [US4] Verify all 25 section types are addable through theme editor with default configurations (FR-001)
- [x] T094 [US4] Verify slideshow section supports 12 slides with 60-char headings, 40-50 word descriptions, 30-char buttons (FR-002)
- [x] T095 [US4] Verify video sections render YouTube, Vimeo, and MP4 with full controls (FR-010)
- [x] T096 [US4] Verify newsletter validates email input and shows success/error messages (FR-007)

**Checkpoint**: 3 presets active with distinct identities, all sections editable in theme editor

---

## Phase 8: User Story 8 + User Story 10 — Compliance & Developer Experience (Priority: P8, P10)

**Goal**: Collection page, utility pages, JSON-LD, theme check compliance, edge case handling

**Independent Test**: Run `shopify theme check`, test all page templates, verify structured data, test edge cases

### Collection Page (FR-026 to FR-030)

- [x] T097 [US8] Implement Storefront Filtering API with filter groups, price range, checkboxes, active filters display in `sections/collection.liquid` (FR-027)
- [x] T098 [US8] Implement tag-based filtering as legacy fallback with multi-tag support, 20+ tags, 30-char names in `sections/collection.liquid` (FR-027)
- [x] T099 [US8] Implement 7 sort options (price asc/desc, alpha A-Z/Z-A, date new/old, best selling) with URL state in `sections/collection.liquid` (FR-026)
- [x] T100 [US8] Implement numbered pagination with truncation at 5+ pages in collection section (FR-028)
- [x] T101 [US8] Implement "Load More" button with AJAX loading, remaining count in collection section (FR-028)
- [x] T102 [US8] Create collection toolbar with product count, sort dropdown, view toggle, mobile filter toggle in `sections/collection.liquid`
- [x] T103 [US8] Create empty state for collection with clear messaging, clear filters, continue shopping in `snippets/collection-empty.liquid` (FR-058)
- [x] T104 [US8] Create quick view modal snippet with mini gallery, variant selector, add-to-cart, focus trap in `snippets/quick-view.liquid`
- [x] T105 [US8] Create collection JavaScript for AJAX filtering, sorting, pagination, view toggle in `assets/collection.js` (~2KB)
- [x] T106 [US8] Rebuild collection list page with images, fallback to first product image, pagination in `sections/collections.liquid` (FR-030)

### Utility Pages (FR-043, FR-044, FR-045)

- [x] T107 [P] [US8] Rebuild password page with logo (7 ratios), password form, 500+ char merchant message in `sections/password.liquid` (FR-043)
- [x] T108 [P] [US8] Create gift card template with full code, logo, store name, value, expiry, copy-code button in `templates/gift_card.liquid` (FR-044)
- [x] T109 [P] [US8] Rebuild 404 page section with helpful messaging, continue shopping link in `sections/404.liquid`

### Structured Data (FR-060)

- [x] T110 [US10] Create JSON-LD snippet for Product, Offer, AggregateRating, Brand, Image schemas in `snippets/json-ld.liquid`
- [x] T111 [US10] Create JSON-LD snippet for BreadcrumbList schema in `snippets/json-ld.liquid`
- [x] T112 [US10] Create JSON-LD snippet for Organization schema in `snippets/json-ld.liquid`
- [x] T113 [US10] Integrate JSON-LD into product, collection, article, and homepage templates

### Developer Experience (US10)

- [x] T114 [P] [US10] Audit and add LiquidDoc headers to all snippets missing `{% doc %}` blocks (FR-056)
- [x] T115 [P] [US10] Audit and ensure all schema labels use `t:` translation keys in all sections/blocks (FR-056)
- [x] T116 [US10] Verify semantic HTML heading hierarchy (single h1 per page) across all templates (FR-045)
- [x] T117 [US10] Verify canonical URLs present on all pages via `snippets/meta-tags.liquid` (FR-045)

### Content Edge Cases (FR-059)

- [x] T118 [P] [US8] Test single 30-char word titles without break points across all sections (Edge Case: Content)
- [x] T119 [P] [US8] Test 1000+ char descriptions with no paragraph breaks in product and rich text sections (Edge Case: Content)
- [x] T120 [P] [US8] Test 30-char single-word button text across all button instances (Edge Case: Content)
- [x] T121 [P] [US8] Test all sections with empty content (empty state validation) (Edge Case: Content, FR-058)
- [x] T122 [P] [US8] Test product with 100 variants for performance and UI rendering (Edge Case: Product)
- [x] T123 [P] [US8] Test all-sold-out product, no-image product, mixed compare-at pricing (Edge Case: Product)
- [x] T124 [P] [US8] Test collection with zero products and collection missing image (Edge Case: Collection)
- [x] T125 [P] [US8] Test cart with 20+ line items, stock exceeded, discount to zero (Edge Case: Cart)
- [x] T126 [P] [US8] Test 9:16 portrait in 16:9 slot, retina images, PNG transparency (Edge Case: Image)
- [x] T127 [P] [US8] Test 10+ menu items on 320px, 60-char third-level title (Edge Case: Navigation)

**Checkpoint**: Collection page, utility pages, structured data, and edge cases validated

---

## Phase 9: User Story 9 — Performance & Accessibility (Priority: P9)

**Goal**: Lighthouse 90+, WCAG 2.1 AA, JS ≤16KB, keyboard navigation, contrast 4.5:1

**Independent Test**: Run Lighthouse audits, keyboard-only navigation, contrast checker across all color schemes

### Performance (SC-001, SC-002, SC-003, SC-004)

- [✅] T128 [US9] Audit and optimize JavaScript total payload to ≤16KB gzipped across all modules (SC-002)
- [✅] T129 [US9] Audit and optimize LCP to <2.5s on simulated 4G — lazy loading, preloading, critical CSS (SC-003)
- [✅] T130 [US9] Audit and optimize CLS to <0.1 — image dimensions, font loading, layout stability (SC-004)
- [✅] T131 [US9] Run Lighthouse audits on homepage, product, collection, blog, search pages (SC-001)

### Accessibility (SC-006, SC-007)

- [✅] T132 [US9] Implement full keyboard navigation across all interactive elements: Tab, Enter, Escape (SC-006)
- [✅] T133 [US9] Implement focus traps in all modals, drawers, and overlays with return-to-trigger on close (SC-006)
- [✅] T134 [US9] Audit and fix text-to-background contrast ratios to ≥4.5:1 across all color schemes (SC-007)
- [✅] T135 [US9] Implement visible focus indicators on all interactive elements in all color schemes
- [✅] T136 [US9] Audit slideshow autoplay for screen reader accessibility with aria-live regions
- [✅] T137 [US9] Verify all responsive breakpoints (320px, 375px, 425px, 768px, 1024px, 1440px, 2560px) (FR-057)
- [✅] T138 [US9] Test hybrid device behavior (touchscreen laptops) and modal/drawer resize scenarios

### Theme Check Compliance (SC-005)

- [✅] T139 [US9] Run `shopify theme check` and resolve all errors and warnings to zero (SC-005, FR-056)
- [✅] T140 [US9] Verify all 131 Shopify Theme Store checklist items (SC-008)

**Checkpoint**: Performance, accessibility, and compliance benchmarks met

---

## Phase 10: Polish & Final Verification

**Purpose**: Cross-cutting concerns, final assembly, submission readiness

- [✅] T141 [US9] Audit 100% translation key coverage — verify all user-facing text uses `t:` keys, all schema labels use `t:` keys, sentence case, snake_case naming in `locales/en.default.json` and `locales/en.default.schema.json`
- [✅] T142 [US8] Run full 7×7 product configuration × breakpoint test matrix (49 combinations) (SC-009)
- [🟨] T143 [US3] Verify all 3 presets differ in ≥3 dimensions (color palette, primary font, heading font, section spacing, default section order) and all functional tests pass (SC-010)
- [✅] T144 [US8] Verify homepage-to-cart journey completes in under 60 seconds (SC-011)
- [✅] T145 [US5] Verify predictive search returns suggestions within 500ms (SC-012)
- [✅] T146 [US8] Verify every section and template displays meaningful empty states (SC-013)
- [🟨] T147 [US8] Final submission readiness review — Theme Store first-attempt pass (SC-014)

**Checkpoint**: Theme ready for Shopify Theme Store submission

---

## Dependencies & Execution Order

### Phase Dependencies

- **Phase 1 (Setup)**: COMPLETE — no remaining tasks
- **Phase 2 (Header/Footer)**: Can start immediately — BLOCKS Phases 3–10
- **Phase 3 (US1 Homepage)**: Depends on Phase 2 (header/footer for full page testing)
  - T014–T017 (snippets) can start in parallel with Phase 2
  - T018–T042 (sections) can start after T014–T017 snippets complete
  - T043–T045 (assembly) depends on all sections complete
- **Phase 4 (US2 Product/Cart)**: Depends on T014 (product-card) from Phase 3
- **Phase 5 (US5 Search)**: Depends on T004 (predictive search snippet) from Phase 2
- **Phase 6 (US6 Blog)**: Can start after Phase 2
- **Phase 7 (US3+US4 Presets)**: Depends on all sections from Phases 3–6
- **Phase 8 (US8+US10 Compliance)**: Depends on T014 (product-card) and Phase 4 (product/cart)
- **Phase 9 (US9 Performance)**: Depends on Phases 3–8 complete
- **Phase 10 (Polish)**: Depends on all previous phases

### Parallel Opportunities

Tasks marked [P] within each phase can run in parallel. Key parallelization points:

- **Phase 2**: T002, T003, T004, T005 can all run in parallel
- **Phase 3**: All slideshow sections (T018–T020), all featured product sections (T021–T025), all featured collection sections (T026–T028), all image-with-text sections (T029–T031), core sections (T032–T037), and unique sections (T038–T042) can run in parallel after foundational snippets complete
- **Phase 4**: Media gallery snippets (T046–T048), variant snippets (T050–T051), and cart snippets (T063–T064) can run in parallel
- **Phase 5**: All 5 tasks are sequential (small phase)
- **Phase 6**: Share links (T077) and article card (T078) can run in parallel
- **Phase 7**: All 3 presets (T084–T086) and all 3 listings (T090–T092) can run in parallel
- **Phase 8**: Filtering methods (T097–T098), sort (T099), utility pages (T107–T109), JSON-LD (T110–T112), DX audits (T114–T115), and all edge case tests (T118–T127) can run in parallel (note: T100–T101 pagination tasks are sequential — same file)

**68 of 147 tasks are marked [P]** (46% parallelizable)

---

## FR Coverage Matrix

| FR | Task(s) | Phase |
|----|---------|-------|
| FR-001 | T043, T093 | 3, 7 |
| FR-002 | T016, T018–T020, T094 | 3, 7 |
| FR-003 | T014, T021–T025 | 3 |
| FR-004 | T015, T026–T027 | 3 |
| FR-005 | T028 | 3 |
| FR-006 | T029–T031 | 3 |
| FR-007 | T007, T032, T096 | 2, 3, 7 |
| FR-008 | T033 | 3 |
| FR-009 | T034–T035 | 3 |
| FR-010 | T017, T036–T037, T095 | 3, 7 |
| FR-011 | COMPLETE (Phase 01-02) | — |
| FR-012 | T002, T003 | 2 |
| FR-013 | T001, T005, T011 | 2 |
| FR-014 | T006–T009 | 2 |
| FR-015 | T010 | 2 |
| FR-016 | T060, T071 | 4 |
| FR-017 | T050–T053 | 4 |
| FR-018 | T054–T055 | 4 |
| FR-019 | T056 | 4 |
| FR-020 | T046, T049 | 4 |
| FR-021 | T047–T048 | 4 |
| FR-022 | T057 | 4 |
| FR-023 | T058 | 4 |
| FR-024 | T056 (unit pricing in price.liquid) | 4 |
| FR-025 | T059 | 4 |
| FR-026 | T099 | 8 |
| FR-027 | T097–T098 | 8 |
| FR-028 | T100–T101 | 8 |
| FR-029 | T014 (product-card badges) | 3 |
| FR-030 | T106 | 8 |
| FR-031 | T063–T064, T069 | 4 |
| FR-032 | T065 | 4 |
| FR-033 | T066–T067 | 4 |
| FR-034 | T068 | 4 |
| FR-035 | T058, T063 (selling plan in cart) | 4 |
| FR-036 | T079 | 6 |
| FR-037 | T080 | 6 |
| FR-038 | T080 | 6 |
| FR-039 | T081 | 6 |
| FR-040 | T077, T082 | 6 |
| FR-041 | T004, T072 | 2, 5 |
| FR-042 | T073–T074 | 5 |
| FR-043 | T107 | 8 |
| FR-044 | T108 | 8 |
| FR-045 | T082, T116–T117 | 6, 8 |
| FR-046 | T084–T086 | 7 |
| FR-047 | T087 | 7 |
| FR-048 | T088 | 7 |
| FR-049 | T089 | 7 |
| FR-050 | T090–T092 | 7 |
| FR-051 | T042 | 3 |
| FR-052 | T038 | 3 |
| FR-053 | T039 | 3 |
| FR-054 | T040 | 3 |
| FR-055 | T041 | 3 |
| FR-056 | T114–T115, T139 | 8, 9 |
| FR-057 | T137 | 9 |
| FR-058 | T045, T121, T146 | 3, 8, 10 |
| FR-059 | T118–T120 | 8 |
| FR-060 | T110–T113 | 8 |

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- US7 (Rich Media) integrated into US2 Phase 4 (product gallery 3D/AR/video) and US1 Phase 3 (video sections)
- Phases 01-02 (Foundation + Design System) are fully complete — 23 tasks already done
- Total remaining: 147 tasks (T001–T147)
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
