# Data Model: Khors Premium Shopify Theme

**Branch**: `001-khors-theme` | **Date**: 2026-02-06 | **Phase**: 1 (Design)

## Overview

Khors operates entirely within Shopify's managed data layer. There is no custom database — all data lives in Shopify's product catalog, content management, and theme settings systems. This document maps the 7 specification entities to their Shopify Liquid object representations.

## Entity Mappings

### 1. Preset

A named configuration bundle producing a visually distinct store experience.

**Shopify Storage**: `config/settings_data.json` (presets object) + `listings/` directory

**Liquid Access**:
```liquid
{{ settings.type_primary_font }}
{{ settings.color_schemes.scheme-1.settings.background }}
```

**Schema**:
```json
{
  "presets": {
    "Aura": {
      "type_primary_font": "serif_font_value",
      "color_schemes": { ... },
      "sections": { ... }
    },
    "Apex": { ... },
    "Nexus": { ... }
  }
}
```

**Theme Store Listing**: Each preset has a `listings/<preset>/listing.json` containing:
- Preset name and description
- Preview screenshot references
- Template overrides (`listings/<preset>/templates/*.json`)

**Properties**:

| Property | Type | Shopify Source | Notes |
|----------|------|---------------|-------|
| name | string | `settings_data.json` key | "Aura", "Apex", "Nexus" |
| color_palette | object | `settings.color_schemes` | 3 schemes × 6 vars = 18 colors per preset |
| typography | object | `settings.type_primary_font`, `settings.type_secondary_font` | Font family, weight, size |
| section_defaults | object | `settings_data.json` sections | Default section configuration per preset |
| listing_metadata | object | `listings/<preset>/listing.json` | Theme Store display metadata |

---

### 2. Section

A full-width, independently configurable page module.

**Shopify Storage**: `sections/*.liquid` files with `{% schema %}` blocks

**Liquid Access**:
```liquid
{{ section.settings.heading }}
{{ section.id }}
{% for block in section.blocks %}
  {{ block.settings.text }}
{% endfor %}
```

**Properties**:

| Property | Type | Shopify Source | Notes |
|----------|------|---------------|-------|
| id | string | `{{ section.id }}` | Auto-generated unique identifier |
| type | string | Schema `name` | e.g., "slideshow", "featured-products" |
| settings | object | `{{ section.settings }}` | Defined in `{% schema %}` settings array |
| blocks | array | `{{ section.blocks }}` | Nested block instances |
| class | string | `{{ section.settings.color_scheme }}` | CSS class for color scheme |

**Constraints**:
- Schema `name` MUST use `t:` translation key
- Settings types: text, textarea, richtext, image_picker, url, select, checkbox, range, color, color_scheme, font_picker, link_list, collection, product, blog, page, video_url, html
- Blocks typically use `"type": "@theme"` for theme-level blocks
- Presets define default configurations for theme editor "Add section" menu

---

### 3. Block

A nestable UI component within a section.

**Shopify Storage**: `blocks/*.liquid` files with `{% schema %}` blocks

**Liquid Access**:
```liquid
{{ block.settings.text }}
{{ block.type }}
{{ block.shopify_attributes }}
{{ block.id }}
```

**Properties**:

| Property | Type | Shopify Source | Notes |
|----------|------|---------------|-------|
| id | string | `{{ block.id }}` | Auto-generated unique identifier |
| type | string | `{{ block.type }}` | Block type from schema |
| settings | object | `{{ block.settings }}` | Defined in block's `{% schema %}` |
| shopify_attributes | string | `{{ block.shopify_attributes }}` | Theme editor integration attributes |

**Delegation Pattern**: Blocks configure settings through the theme editor, then delegate rendering to snippets:
```liquid
{%- comment -%} blocks/button.liquid {%- endcomment -%}
<div {{ block.shopify_attributes }}>
  {% render 'button', text: block.settings.text, variant: block.settings.variant %}
</div>
```

---

### 4. Product Configuration

One of 7 required product setups exercising different rendering paths.

**Shopify Storage**: Shopify Admin (product catalog)

**Liquid Access**:
```liquid
{{ product.title }}
{{ product.description }}
{{ product.vendor }}
{{ product.variants }}
{{ product.options }}
{{ product.media }}
{{ product.selected_or_first_available_variant }}
{{ product.has_only_default_variant }}
{{ product.available }}
{{ product.compare_at_price }}
{{ product.price }}
```

**7 Required Configurations**:

| Configuration | Key Properties | Rendering Path |
|---------------|---------------|----------------|
| Single Product | `has_only_default_variant: true` | No variant selector, simple price |
| Sale Product | `compare_at_price > price` | Crossed-out original + sale price |
| One-Option | `options.size == 1` | Single dropdown/swatch selector |
| Multi-Option | `options.size == 2`, mixed availability | Multiple selectors, availability matrix |
| Three-Option | `options.size == 3` | Three selectors, complex availability |
| 100-Variant | `variants.size == 100` | Performance-critical selector rendering |
| No-Image | `media.size == 0` | Placeholder image/text fallback |

**Media Types** (via `product.media`):

| Type | Liquid Filter | HTML Output |
|------|--------------|-------------|
| Image | `media | image_url` | `<img>` with responsive srcset |
| Video | `media | video_tag` | `<video>` with controls |
| External Video | `media | external_video_tag` | YouTube/Vimeo iframe |
| 3D Model | `media | model_viewer_tag` | `<model-viewer>` web component |

---

### 5. Color Scheme

A named set of coordinated colors assignable to individual sections.

**Shopify Storage**: `config/settings_schema.json` (color_scheme type)

**Liquid Access**:
```liquid
{{ settings.color_schemes.scheme-1.settings.background }}
{{ settings.color_schemes.scheme-1.settings.text }}
{{ section.settings.color_scheme }}
```

**CSS Custom Properties** (set by `snippets/css-variables.liquid`):

| Property | CSS Variable | Purpose |
|----------|-------------|---------|
| background | `--color-background` | Section background color |
| text | `--color-text` | Primary text color |
| accent | `--color-accent` | Links, highlights |
| button | `--color-button` | Button background |
| button_text | `--color-button-text` | Button text color |
| border | `--color-border` | Borders, dividers |

**Per-Preset Schemes**:

| Preset | Scheme 1 | Scheme 2 | Scheme 3 |
|--------|----------|----------|----------|
| Aura (Beauty) | Soft pastels, serif | Warm neutrals | Dark luxury |
| Apex (Electronics) | Dark mode, monospace | Light tech | High contrast |
| Nexus (Home) | Earth tones, natural | Bright modern | Minimal white |

---

### 6. Variant

A specific combination of product options with own price, SKU, inventory, and image.

**Shopify Storage**: Shopify Admin (product variants)

**Liquid Access**:
```liquid
{{ variant.id }}
{{ variant.title }}
{{ variant.price }}
{{ variant.compare_at_price }}
{{ variant.available }}
{{ variant.sku }}
{{ variant.barcode }}
{{ variant.image }}
{{ variant.unit_price }}
{{ variant.unit_price_measurement }}
{{ variant.inventory_quantity }}
{{ variant.inventory_policy }}
{{ variant.option1 }}
{{ variant.option2 }}
{{ variant.option3 }}
```

**JavaScript Integration** (for dynamic updates):

```javascript
// Variant change event
document.dispatchEvent(new CustomEvent('khors:variant:changed', {
  detail: {
    variantId: variant.id,
    price: variant.price,
    compareAtPrice: variant.compare_at_price,
    available: variant.available,
    image: variant.featured_image,
    sku: variant.sku,
    unitPrice: variant.unit_price
  }
}));
```

**Availability Matrix**: For products with multiple options, an availability matrix pre-computed in Liquid maps option combinations to variant availability:

```liquid
{% liquid
  assign variant_json = product.variants | json
%}
<script type="application/json" id="product-variants-{{ section.id }}">
  {{ variant_json }}
</script>
```

---

### 7. Selling Plan

A subscription or recurring purchase option attached to a product.

**Shopify Storage**: Shopify Admin (via subscription app — Recharge, Bold, etc.)

**Liquid Access**:
```liquid
{% for group in product.selling_plan_groups %}
  {{ group.name }}
  {{ group.app_id }}
  {% for plan in group.selling_plans %}
    {{ plan.name }}
    {{ plan.id }}
    {% for adjustment in plan.price_adjustments %}
      {{ adjustment.value }}
      {{ adjustment.value_type }}
      {{ adjustment.order_count }}
    {% endfor %}
  {% endfor %}
{% endfor %}
```

**Cart Line Item Access**:
```liquid
{% for item in cart.items %}
  {% if item.selling_plan_allocation %}
    {{ item.selling_plan_allocation.selling_plan.name }}
    {{ item.selling_plan_allocation.per_delivery_price | money }}
  {% endif %}
{% endfor %}
```

**Properties**:

| Property | Type | Shopify Source | Notes |
|----------|------|---------------|-------|
| id | integer | `selling_plan.id` | Unique plan identifier |
| name | string | `selling_plan.name` | Display name (e.g., "Deliver every 30 days") |
| group_name | string | `selling_plan_group.name` | Group name (e.g., "Subscribe & Save") |
| price_adjustments | array | `selling_plan.price_adjustments` | Discount rules per delivery |
| value_type | string | `adjustment.value_type` | "percentage", "fixed_amount", "price" |
| recurring | boolean | `selling_plan.recurring` | Whether plan recurs |

**Form Integration**: Selling plan ID must be included in the add-to-cart form:
```liquid
<input type="hidden" name="selling_plan" value="{{ selling_plan.id }}">
```

## Entity Relationships

```
Preset (3)
├── defines → Color Scheme (3 per preset = 9 total)
├── configures → Section defaults (via settings_data.json)
└── provides → Listing metadata (via listings/)

Section (30+)
├── contains → Block (0-n via @theme blocks)
├── applies → Color Scheme (1 per section)
└── renders → Snippet (via {% render %})

Product Configuration (7 types)
├── has → Variant (1-100 per product)
├── has → Media (images, video, 3D models)
└── supports → Selling Plan (0-n per product)

Variant
├── belongs to → Product Configuration
├── has → Price, Compare-at Price, Unit Price
├── has → SKU, Barcode, Inventory
└── optionally → Image, Selling Plan
```
