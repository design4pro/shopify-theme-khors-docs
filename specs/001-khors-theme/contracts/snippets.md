# Snippet Parameter Contracts

**Branch**: `001-khors-theme` | **Date**: 2026-02-06

## Universal Snippet Contract

Every snippet MUST have a `{% doc %}` header (LiquidDoc). Parameters are passed via `{% render %}` — snippets cannot access global variables.

```liquid
{% doc %}
  Brief description of what this snippet renders.

  @param {type} param_name - Description of the parameter
  @param {type} [optional_param] - Optional parameter with default behavior

  @example
  {% render 'snippet-name', param_name: value %}
{% enddoc %}
```

## Existing Snippet Contracts

### button.liquid

```liquid
{% doc %}
  Renders a button or link styled as a button.

  @param {string} text - Button label text
  @param {string} [url] - Link destination URL
  @param {string} [variant] - Visual style: button--primary, button--secondary, button--outline, button--ghost
  @param {string} [size] - Size modifier: button--small, button--medium, button--large
  @param {boolean} [full_width] - Whether button takes full container width
  @param {string} [icon] - Icon name: loading, cart, arrow-right, heart, search, user, check
  @param {string} [icon_position] - Icon placement: left, right
  @param {boolean} [loading] - Show loading spinner state

  @example
  {% render 'button', text: 'Add to cart', variant: 'button--primary', icon: 'cart' %}
{% enddoc %}
```

### image.liquid

```liquid
{% doc %}
  Renders a responsive image with srcset and lazy loading.

  @param {image} image - Shopify image object
  @param {string} [alt] - Alt text override (defaults to image.alt)
  @param {string} [sizes] - Sizes attribute for responsive images
  @param {string} [class] - Additional CSS classes
  @param {boolean} [lazy] - Enable lazy loading (default: true)
  @param {number} [width] - Max width for srcset generation
  @param {number} [height] - Height for aspect ratio

  @example
  {% render 'image', image: section.settings.image, sizes: '(min-width: 768px) 50vw, 100vw' %}
{% enddoc %}
```

### icon.liquid

```liquid
{% doc %}
  Renders an inline SVG icon.

  @param {string} name - Icon identifier (e.g., cart, search, account, heart, arrow-right)
  @param {string} [size] - Size modifier: icon--small, icon--medium, icon--large
  @param {string} [class] - Additional CSS classes

  @example
  {% render 'icon', name: 'cart', size: 'icon--medium' %}
{% enddoc %}
```

### price.liquid

```liquid
{% doc %}
  Renders product pricing with support for regular, compare-at, and unit pricing.

  @param {variant} variant - Shopify variant object
  @param {boolean} [show_compare_at] - Show crossed-out compare-at price (default: true)
  @param {boolean} [show_unit_price] - Show unit pricing if available (default: true)
  @param {string} [class] - Additional CSS classes

  @example
  {% render 'price', variant: product.selected_or_first_available_variant %}
{% enddoc %}
```

### badge.liquid

```liquid
{% doc %}
  Renders a status badge (Sale, Sold Out, New, etc.).

  @param {string} text - Badge label text
  @param {string} [variant] - Badge style: badge--sale, badge--sold-out, badge--new, badge--custom
  @param {string} [class] - Additional CSS classes

  @example
  {% render 'badge', text: 'Sale', variant: 'badge--sale' %}
{% enddoc %}
```

### form-field.liquid

```liquid
{% doc %}
  Renders a form input field with label and error handling.

  @param {string} name - Input name attribute
  @param {string} label - Visible label text
  @param {string} [type] - Input type: text, email, password, textarea (default: text)
  @param {string} [value] - Pre-filled value
  @param {boolean} [required] - Whether field is required (default: false)
  @param {string} [error] - Error message to display
  @param {string} [autocomplete] - Autocomplete attribute value

  @example
  {% render 'form-field', name: 'email', label: 'Email', type: 'email', required: true %}
{% enddoc %}
```

### pagination.liquid

```liquid
{% doc %}
  Renders pagination controls with numbered pages and truncation.

  @param {paginate} paginate - Shopify paginate object
  @param {string} [type] - Pagination style: numbered, load-more, infinite (default: numbered)
  @param {string} [class] - Additional CSS classes

  @example
  {% render 'pagination', paginate: paginate, type: 'numbered' %}
{% enddoc %}
```

### header-logo.liquid

```liquid
{% doc %}
  Renders the store logo or text fallback.

  @param {image} [logo] - Logo image from settings
  @param {number} [logo_width] - Logo display width in pixels
  @param {string} [class] - Additional CSS classes

  @example
  {% render 'header-logo', logo: section.settings.logo, logo_width: section.settings.logo_width %}
{% enddoc %}
```

### social-links.liquid

```liquid
{% doc %}
  Renders social media icon links for configured platforms.

  @param {string} [class] - Additional CSS classes

  @example
  {% render 'social-links' %}
{% enddoc %}
```

### breadcrumb.liquid

```liquid
{% doc %}
  Renders breadcrumb navigation with structured data.

  @param {string} [class] - Additional CSS classes

  @example
  {% render 'breadcrumb' %}
{% enddoc %}
```

## Planned Snippet Contracts

### product-card.liquid

```liquid
{% doc %}
  Renders a product card for collection grids and featured product sections.

  @param {product} product - Shopify product object
  @param {boolean} [show_vendor] - Show vendor name (default: false)
  @param {boolean} [show_badge] - Show sale/sold-out badges (default: true)
  @param {boolean} [show_quick_view] - Enable quick view button (default: false)
  @param {string} [image_ratio] - Image aspect ratio: landscape, portrait, square (default: square)
  @param {string} [class] - Additional CSS classes

  @example
  {% render 'product-card', product: product, show_badge: true, image_ratio: 'square' %}
{% enddoc %}
```

### variant-selector.liquid

```liquid
{% doc %}
  Renders variant selection controls (dropdowns or color swatches).

  @param {product} product - Shopify product object
  @param {string} [type] - Selector type: dropdown, swatches (default: dropdown)
  @param {string} [section_id] - Parent section ID for event scoping

  @example
  {% render 'variant-selector', product: product, type: 'swatches', section_id: section.id %}
{% enddoc %}
```

### cart-item.liquid

```liquid
{% doc %}
  Renders a single cart line item with quantity controls.

  @param {line_item} item - Shopify cart line item object
  @param {boolean} [show_remove] - Show remove button (default: true)

  @example
  {% render 'cart-item', item: item %}
{% enddoc %}
```

### video-player.liquid

```liquid
{% doc %}
  Renders a video player supporting YouTube, Vimeo, and hosted MP4.

  @param {string} [video_url] - YouTube or Vimeo URL
  @param {video} [video] - Shopify hosted video object
  @param {image} [cover_image] - Poster image before playback
  @param {boolean} [autoplay] - Autoplay on visible (muted, default: false)
  @param {boolean} [loop] - Loop playback (default: false)

  @example
  {% render 'video-player', video_url: section.settings.video_url, cover_image: section.settings.cover_image %}
{% enddoc %}
```

### json-ld.liquid

```liquid
{% doc %}
  Renders JSON-LD structured data for SEO.

  @param {string} type - Schema.org type: Product, BreadcrumbList, Organization
  @param {product} [product] - Product object (for Product type)
  @param {array} [breadcrumbs] - Breadcrumb items array (for BreadcrumbList type)

  @example
  {% render 'json-ld', type: 'Product', product: product %}
{% enddoc %}
```

### share-links.liquid

```liquid
{% doc %}
  Renders social sharing buttons for products and articles.

  @param {string} url - Page URL to share
  @param {string} title - Page title for share text
  @param {string} [image] - Image URL for Pinterest sharing
  @param {string} [class] - Additional CSS classes

  @example
  {% render 'share-links', url: request.origin | append: product.url, title: product.title %}
{% enddoc %}
```
