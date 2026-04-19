# Section Schema Contracts

**Branch**: `001-khors-theme` | **Date**: 2026-02-06

## Universal Section Contract

Every section MUST follow this schema pattern:

```json
{% schema %}
{
  "name": "t:sections.section_name.name",
  "tag": "section",
  "class": "section-name",
  "settings": [
    {
      "type": "color_scheme",
      "id": "color_scheme",
      "label": "t:sections.all.color_scheme.label",
      "default": "scheme-1"
    }
  ],
  "blocks": [
    {
      "type": "@theme"
    }
  ],
  "presets": [
    {
      "name": "t:sections.section_name.presets.name"
    }
  ]
}
{% endschema %}
```

## Required Schema Properties

| Property | Required | Notes |
|----------|----------|-------|
| `name` | YES | Must use `t:` translation key |
| `tag` | YES | Usually `"section"` |
| `class` | YES | BEM block name matching filename |
| `settings` | YES | Array of setting definitions |
| `blocks` | YES | At minimum `[{ "type": "@theme" }]` |
| `presets` | YES* | Required for addable sections, omit for page-specific (product, cart, etc.) |

*Page-specific sections (product.liquid, cart.liquid, etc.) do NOT have presets because they cannot be freely added/removed.

## Section Categories and Contracts

### Homepage Sections (25 minimum)

#### Slideshow Sections (3 required)

**slideshow.liquid** — Standard slideshow:
```json
{
  "name": "t:sections.slideshow.name",
  "settings": [
    { "type": "checkbox", "id": "autoplay", "label": "t:sections.slideshow.settings.autoplay.label", "default": true },
    { "type": "range", "id": "autoplay_speed", "min": 3, "max": 10, "step": 1, "unit": "s", "label": "t:sections.slideshow.settings.speed.label", "default": 5 },
    { "type": "select", "id": "slide_height", "label": "t:sections.slideshow.settings.height.label", "options": [...] },
    { "type": "color_scheme", "id": "color_scheme" }
  ],
  "blocks": [
    {
      "type": "slide",
      "name": "t:sections.slideshow.blocks.slide.name",
      "limit": 12,
      "settings": [
        { "type": "image_picker", "id": "image" },
        { "type": "text", "id": "heading" },
        { "type": "text", "id": "subheading" },
        { "type": "richtext", "id": "description" },
        { "type": "text", "id": "button_text" },
        { "type": "url", "id": "button_link" }
      ]
    }
  ]
}
```

#### Featured Product Sections (5 required)

Common settings contract for all featured product sections:
```json
{
  "settings": [
    { "type": "text", "id": "heading" },
    { "type": "collection", "id": "collection" },
    { "type": "range", "id": "products_to_show", "min": 2, "max": 12 },
    { "type": "select", "id": "columns_desktop", "options": [2, 3, 4] },
    { "type": "checkbox", "id": "show_vendor" },
    { "type": "checkbox", "id": "show_price" },
    { "type": "checkbox", "id": "show_badge" },
    { "type": "color_scheme", "id": "color_scheme" }
  ]
}
```

Variants: `featured-products-grid.liquid`, `featured-products-carousel.liquid`, `featured-products-tabs.liquid`, `featured-products-masonry.liquid`, `featured-product.liquid` (single)

#### Featured Collection Sections (3 required)

```json
{
  "settings": [
    { "type": "text", "id": "heading" },
    { "type": "collection_list", "id": "collection_list" },
    { "type": "range", "id": "collections_to_show", "min": 2, "max": 12 },
    { "type": "color_scheme", "id": "color_scheme" }
  ]
}
```

#### Image with Text Sections (3 required)

```json
{
  "settings": [
    { "type": "image_picker", "id": "image" },
    { "type": "select", "id": "image_position", "options": ["left", "right"] },
    { "type": "text", "id": "heading" },
    { "type": "richtext", "id": "description" },
    { "type": "text", "id": "button_text" },
    { "type": "url", "id": "button_link" },
    { "type": "color_scheme", "id": "color_scheme" }
  ]
}
```

#### Newsletter Section (1 required)

```json
{
  "settings": [
    { "type": "text", "id": "heading" },
    { "type": "richtext", "id": "description" },
    { "type": "text", "id": "button_text", "default": "Subscribe" },
    { "type": "color_scheme", "id": "color_scheme" }
  ]
}
```

#### Video Sections (2 required)

```json
{
  "settings": [
    { "type": "video_url", "id": "video_url", "accept": ["youtube", "vimeo"] },
    { "type": "video", "id": "video" },
    { "type": "image_picker", "id": "cover_image" },
    { "type": "checkbox", "id": "autoplay", "default": false },
    { "type": "checkbox", "id": "loop", "default": false },
    { "type": "color_scheme", "id": "color_scheme" }
  ]
}
```

#### Unique Industry Sections (5 required)

| Section | Key Settings | Blocks |
|---------|-------------|--------|
| `ingredient-spotlight.liquid` | heading, layout, color_scheme | ingredient (image, name, description, benefits) |
| `tech-specs-comparison.liquid` | heading, columns, color_scheme | product (product_picker, specs as metafields) |
| `room-visualizer.liquid` | heading, room_image, color_scheme | product (product_picker, position_x, position_y) |
| `before-after-slider.liquid` | heading, before_image, after_image, color_scheme | (none — settings only) |
| `testimonials.liquid` | heading, color_scheme | testimonial (author, text, rating, avatar) |

### Navigation Sections

#### header.liquid

```json
{
  "name": "t:sections.header.name",
  "settings": [
    { "type": "image_picker", "id": "logo" },
    { "type": "range", "id": "logo_width", "min": 50, "max": 300 },
    { "type": "link_list", "id": "menu" },
    { "type": "checkbox", "id": "sticky_header", "default": true },
    { "type": "checkbox", "id": "transparent_header", "default": false },
    { "type": "checkbox", "id": "show_search", "default": true },
    { "type": "checkbox", "id": "show_account", "default": true },
    { "type": "color_scheme", "id": "color_scheme" }
  ]
}
```

#### footer.liquid

```json
{
  "name": "t:sections.footer.name",
  "settings": [
    { "type": "checkbox", "id": "show_newsletter", "default": true },
    { "type": "checkbox", "id": "show_social", "default": true },
    { "type": "checkbox", "id": "show_payment_icons", "default": true },
    { "type": "color_scheme", "id": "color_scheme" }
  ],
  "blocks": [
    {
      "type": "menu",
      "name": "t:sections.footer.blocks.menu.name",
      "settings": [
        { "type": "text", "id": "heading" },
        { "type": "link_list", "id": "menu" }
      ]
    },
    {
      "type": "text",
      "name": "t:sections.footer.blocks.text.name",
      "settings": [
        { "type": "text", "id": "heading" },
        { "type": "richtext", "id": "content" }
      ]
    }
  ]
}
```

#### announcement-bar.liquid

```json
{
  "name": "t:sections.announcement_bar.name",
  "settings": [
    { "type": "richtext", "id": "text" },
    { "type": "url", "id": "link" },
    { "type": "checkbox", "id": "link_new_window", "default": false },
    { "type": "color_scheme", "id": "color_scheme" }
  ]
}
```

### Page-Specific Sections (no presets)

| Section | Key Settings | Notes |
|---------|-------------|-------|
| `product.liquid` | Media gallery, variant selector, selling plans, local pickup | Most complex section |
| `collection.liquid` | Sort options, filter type, pagination type, columns | Filtering API integration |
| `cart.liquid` | Show notes, show discount input, cross-sell | AJAX cart drawer companion |
| `blog.liquid` | Posts per page, show author, show date, show tags | Pagination required |
| `article.liquid` | Show comments, show sharing, show author | Comment form integration |
| `search.liquid` | Results per page, show filters | Predictive search companion |
| `password.liquid` | Background image, logo display | Standalone layout |

## Color Scheme Integration

Every section that renders visible content MUST include a `color_scheme` setting:

```json
{
  "type": "color_scheme",
  "id": "color_scheme",
  "label": "t:sections.all.color_scheme.label",
  "default": "scheme-1"
}
```

The section wrapper applies the scheme:
```liquid
<section class="section-name color-{{ section.settings.color_scheme }}">
  ...
</section>
```
