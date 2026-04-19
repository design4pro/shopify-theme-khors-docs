# JavaScript API Contracts

**Branch**: `001-khors-theme` | **Date**: 2026-02-06

## Architecture

- **No build step**: Raw ES6+ files in `assets/` directory
- **Loading**: `<script defer src="{{ 'module.js' | asset_url }}">` in layout or sections
- **Communication**: Custom events on `document`
- **Components**: Web Components with `#private` methods where needed
- **Budget**: Total ≤ 16KB gzipped

## Custom Event Contracts

All cross-component communication uses `CustomEvent` on `document`. Event names follow the `khors:domain:action` pattern.

### Cart Events

```javascript
// Fired after item added to cart
document.dispatchEvent(new CustomEvent('khors:cart:item-added', {
  detail: {
    items: [{ id, quantity, variant_id, product_title }],
    cart: { item_count, total_price }
  }
}));

// Fired after cart updated (quantity change, remove)
document.dispatchEvent(new CustomEvent('khors:cart:updated', {
  detail: {
    cart: { items, item_count, total_price, total_discount }
  }
}));

// Fired when cart drawer should open
document.dispatchEvent(new CustomEvent('khors:cart:open'));

// Fired when cart drawer should close
document.dispatchEvent(new CustomEvent('khors:cart:close'));
```

### Variant Events

```javascript
// Fired when variant selection changes
document.dispatchEvent(new CustomEvent('khors:variant:changed', {
  detail: {
    sectionId: 'template--product',
    variant: {
      id: 12345,
      price: 2999,
      compare_at_price: 3999,
      available: true,
      sku: 'ABC-123',
      image: { src, alt, width, height },
      unit_price: 1499,
      unit_price_measurement: { reference_unit: 'kg', reference_value: 1 }
    }
  }
}));

// Fired when variant is unavailable (sold out)
document.dispatchEvent(new CustomEvent('khors:variant:unavailable', {
  detail: { sectionId: 'template--product' }
}));
```

### Search Events

```javascript
// Fired when predictive search results are ready
document.dispatchEvent(new CustomEvent('khors:search:results', {
  detail: {
    query: 'search term',
    results: {
      products: [],
      collections: [],
      pages: [],
      articles: []
    }
  }
}));

// Fired when search input is cleared or closed
document.dispatchEvent(new CustomEvent('khors:search:close'));
```

### Media Events

```javascript
// Fired when media type changes in product gallery
document.dispatchEvent(new CustomEvent('khors:media:changed', {
  detail: {
    sectionId: 'template--product',
    mediaType: 'image' | 'video' | 'model' | 'external_video',
    mediaId: 12345
  }
}));
```

## Module Contracts

### assets/variant-selector.js (~3KB)

```javascript
/**
 * Handles product variant selection and dynamic updates.
 * Listens for option changes, computes selected variant,
 * dispatches khors:variant:changed event.
 *
 * @element [data-variant-selector]
 * @attribute data-section-id - Parent section ID
 * @attribute data-product-json - JSON element ID containing variant data
 */
class VariantSelector {
  // Public API
  constructor(element) {}  // Initialize with container element
  get selectedVariant() {} // Returns current variant or null

  // Private
  #variants = [];
  #onOptionChange(event) {}
  #findVariant(options) {}
  #updatePrice(variant) {}
  #updateImage(variant) {}
  #updateAvailability(variant) {}
  #updateUrl(variant) {}
  #dispatchEvent(variant) {}
}
```

### assets/cart-drawer.js (~3KB)

```javascript
/**
 * AJAX cart drawer with add, update, remove operations.
 * Uses Shopify Cart API (/cart/*.js endpoints).
 *
 * @element [data-cart-drawer]
 * @listens khors:cart:open
 * @listens khors:cart:close
 * @listens khors:cart:item-added
 * @dispatches khors:cart:updated
 */
class CartDrawer {
  // Public API
  constructor(element) {}
  open() {}
  close() {}

  // Private
  #isOpen = false;
  #focusTrap = null;
  #addItem(formData) {}       // POST /cart/add.js
  #updateItem(key, qty) {}    // POST /cart/change.js
  #removeItem(key) {}         // POST /cart/change.js with qty: 0
  #renderCart(cart) {}
  #trapFocus() {}
  #releaseFocus() {}
}
```

### assets/slideshow.js (~2KB)

```javascript
/**
 * Slideshow with autoplay, navigation, and accessibility.
 * Uses CSS scroll-snap for smooth transitions.
 *
 * @element [data-slideshow]
 * @attribute data-autoplay - Enable autoplay (true/false)
 * @attribute data-speed - Autoplay interval in seconds
 */
class Slideshow {
  // Public API
  constructor(element) {}
  play() {}
  pause() {}
  next() {}
  prev() {}
  goTo(index) {}

  // Private
  #currentIndex = 0;
  #autoplayTimer = null;
  #intersectionObserver = null;
  #onKeydown(event) {}   // Arrow keys, Home, End
  #updateDots() {}
  #announceSlide() {}    // aria-live region update
}
```

### assets/predictive-search.js (~2KB)

```javascript
/**
 * Predictive search using Shopify Predictive Search API.
 * Debounced input, AbortController for request cancellation.
 *
 * @element [data-predictive-search]
 * @dispatches khors:search:results
 * @dispatches khors:search:close
 */
class PredictiveSearch {
  // Public API
  constructor(element) {}
  open() {}
  close() {}

  // Private
  #abortController = null;
  #debounceTimer = null;
  #cache = new Map();
  #onInput(event) {}
  #fetchResults(query) {} // GET /search/suggest.json
  #renderResults(data) {}
  #onKeydown(event) {}    // Arrow navigation, Escape to close
}
```

### assets/media-controller.js (~2KB)

```javascript
/**
 * Controls 3D model viewer, video playback, and AR launch.
 * Lazy loads model-viewer library on demand.
 *
 * @element [data-media-controller]
 * @listens khors:media:changed
 */
class MediaController {
  // Public API
  constructor(element) {}

  // Private
  #activeMedia = null;
  #onMediaChange(event) {}
  #initModelViewer(element) {}  // Lazy load <model-viewer>
  #initVideo(element) {}        // Play/pause controls
  #pauseAllMedia() {}           // Pause when switching media
}
```

### assets/khors.js (~1KB)

```javascript
/**
 * Shared utilities and initialization.
 * Entry point loaded on all pages.
 */

// Utility: Debounce function
function debounce(fn, delay) {}

// Utility: Trap focus within element
function trapFocus(element) {}

// Utility: Release focus trap
function releaseFocus() {}

// Utility: Format money (cents to formatted string)
function formatMoney(cents, format) {}

// Utility: Fetch with error handling
async function fetchJSON(url, options) {}

// Auto-initialize components on DOM ready
document.addEventListener('DOMContentLoaded', () => {
  // Initialize components based on data attributes
  document.querySelectorAll('[data-variant-selector]').forEach(el => new VariantSelector(el));
  document.querySelectorAll('[data-cart-drawer]').forEach(el => new CartDrawer(el));
  document.querySelectorAll('[data-slideshow]').forEach(el => new Slideshow(el));
  document.querySelectorAll('[data-predictive-search]').forEach(el => new PredictiveSearch(el));
  document.querySelectorAll('[data-media-controller]').forEach(el => new MediaController(el));
});
```

## Error Handling Contract

All JS modules MUST:
1. Catch fetch errors and display user-friendly messages
2. Never throw unhandled exceptions
3. Degrade gracefully when JS fails (progressive enhancement)
4. Log errors to console in development only

```javascript
// Standard error pattern
try {
  const response = await fetchJSON(url);
  // handle success
} catch (error) {
  if (error.name === 'AbortError') return; // Intentional abort
  console.error('[Khors]', error.message);
  // Show user-friendly error via aria-live region
}
```

## Data Attribute Convention

All JS hooks use `data-` attributes, never CSS classes:

| Attribute | Purpose |
|-----------|---------|
| `data-variant-selector` | Variant selector container |
| `data-cart-drawer` | Cart drawer container |
| `data-slideshow` | Slideshow container |
| `data-predictive-search` | Search input container |
| `data-media-controller` | Media gallery container |
| `data-section-id` | Links component to section for event scoping |
| `data-product-json` | ID of script element containing variant JSON |
