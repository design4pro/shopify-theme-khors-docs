# Quickstart: Khors Premium Shopify Theme

**Branch**: `001-khors-theme` | **Date**: 2026-02-06 | **Phase**: 1 (Design)

## Prerequisites

| Tool | Version | Installation |
|------|---------|-------------|
| Node.js | 18+ | [nodejs.org](https://nodejs.org/) |
| Shopify CLI | 3.0+ | `npm install -g @shopify/cli` |
| Ruby | 3.0+ | Required by Shopify CLI internals |
| Git | 2.30+ | [git-scm.com](https://git-scm.com/) |

## Development Store

**Store URL**: `khors-theme-design4pro.myshopify.com`

This is a Shopify Partner development store. You need Shopify Partner credentials to connect.

## Setup Steps

### 1. Clone Repository

```bash
git clone <repo-url>
cd khors-theme
```

### 2. Switch to Development Branch

```bash
git checkout develop
```

All feature work branches from `develop`. Never work directly on `main`.

### 3. Start Local Development

```bash
shopify theme dev --store khors-theme-design4pro.myshopify.com
```

This starts a local preview server with hot reload. Changes to Liquid, CSS, and JS files reflect immediately in the browser.

### 4. Verify Theme Check

```bash
shopify theme check
```

Must report **zero errors and zero warnings**. Run this before every commit.

## Common Commands

| Command | Purpose |
|---------|---------|
| `shopify theme dev --store khors-theme-design4pro.myshopify.com` | Local preview with hot reload |
| `shopify theme check` | Lint theme for errors/warnings |
| `shopify theme push --store khors-theme-design4pro.myshopify.com` | Deploy to development store |
| `shopify theme pull --store khors-theme-design4pro.myshopify.com` | Pull changes from store |

## Git Workflow

### Creating a Feature Branch

```bash
git checkout develop
git pull origin develop
git checkout -b task/X.X-feature-name
```

### Completing Work

```bash
# Verify theme check passes
shopify theme check

# Stage and commit
git add sections/new-section.liquid snippets/new-snippet.liquid
git commit -m "feat(section): add slideshow section with 12-slide support"

# Push and create PR to develop (NEVER to main)
git push -u origin task/X.X-feature-name
gh pr create --base develop --title "feat: add slideshow section"
```

## File Organization

### Creating a New Section

1. Create `sections/section-name.liquid`
2. Add `{% schema %}` with settings, blocks, presets
3. Add translation keys to `locales/en.default.schema.json`
4. Add section to relevant JSON template (e.g., `templates/index.json`)
5. Run `shopify theme check`

### Creating a New Snippet

1. Create `snippets/snippet-name.liquid`
2. Add `{% doc %}` header with description, params, example
3. Use via `{% render 'snippet-name', param: value %}`
4. Run `shopify theme check`

### Creating a New Block

1. Create `blocks/block-name.liquid`
2. Add `{% schema %}` with settings and presets
3. Block delegates rendering to snippet if complex
4. Add translation keys to `locales/en.default.schema.json`
5. Run `shopify theme check`

### Adding JavaScript

1. Create `assets/module-name.js`
2. Load in section via `{% javascript %}` or in layout via `<script defer>`
3. Use custom events for cross-component communication
4. Verify total JS stays under 16KB gzipped

### Adding CSS

1. Component-specific styles: Use `{% stylesheet %}` within the section/block
2. Shared styles: Add to `assets/components.css` in `@layer components`
3. Utilities: Add to `assets/utilities.css` in `@layer utilities`
4. Critical path: Add to `assets/critical.css` in `@layer reset` or `@layer base`

## Testing Checklist

Before creating a PR, verify:

- [ ] `shopify theme check` — zero errors, zero warnings
- [ ] Local preview renders correctly at 320px, 768px, 1440px
- [ ] Empty states render meaningfully (no content configured)
- [ ] Keyboard navigation works on all new interactive elements
- [ ] Translation keys exist for all user-facing strings
- [ ] LiquidDoc headers present on all new snippets
- [ ] No `!important`, no ID selectors, no `&` nesting in CSS
- [ ] BEM naming convention followed for all CSS classes
