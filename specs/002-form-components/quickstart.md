# Quickstart: Ujednolicenie komponentów formularzowych

## Przegląd

Celem jest ujednolicenie wszystkich komponentów formularzowych w motywie Shopify do spójnego, nowoczesnego wyglądu zgodnego z systemem zmiennych CSS.

## Wymagania

- Shopify CLI 3.0
- Node.js (dla Shopify CLI)
- Dostęp do development store: `khors-theme-design4pro.myshopify.com`

## Kroki implementacji

### Krok 1: Utwórz snippet checkbox.liquid

Lokalizacja: `snippets/checkbox.liquid`

```liquid
{% doc %}
  Renders a styled checkbox input with label and help text.

  @param {string} name - Field name attribute (required)
  @param {string} id - Field id attribute (required)
  @param {string} value - Checkbox value
  @param {boolean} checked - Whether checkbox is checked
  @param {boolean} disabled - Whether checkbox is disabled
  @param {string} label - Label text (required)
  @param {string} help_text - Help text shown below
  @param {string} class - Additional CSS classes

  @example Basic checkbox
    {% render 'checkbox',
      name: 'newsletter',
      id: 'newsletter-signup',
      label: 'Sign up for newsletter',
      checked: false
    %}

  @example Checked checkbox
    {% render 'checkbox',
      name: 'terms',
      id: 'terms-accept',
      label: 'I accept the terms',
      checked: true,
      required: true
    %}
{% enddoc %}

{% liquid
  assign checked = checked | default: false
  assign disabled = disabled | default: false
%}

<div class="checkbox{% if class != blank %} {{ class }}{% endif %}">
  <label class="checkbox__label">
    <input
      type="checkbox"
      name="{{ name }}"
      id="{{ id }}"
      value="{{ value | default: 'on' }}"
      {% if checked %}checked{% endif %}
      {% if disabled %}disabled{% endif %}
      class="checkbox__input"
    >
    <span class="checkbox__box"></span>
    <span class="checkbox__text">{{ label }}</span>
  </label>
  {% if help_text != blank %}
    <p class="checkbox__help">{{ help_text }}</p>
  {% endif %}
</div>

{% stylesheet %}
  @layer components {
    .checkbox {
      display: flex;
      flex-direction: column;
      gap: var(--space-2);
    }

    .checkbox__label {
      display: inline-flex;
      align-items: flex-start;
      gap: var(--space-3);
      cursor: pointer;
    }

    .checkbox__input {
      position: absolute;
      opacity: 0;
      width: 0;
      height: 0;
    }

    .checkbox__box {
      flex-shrink: 0;
      width: 20px;
      height: 20px;
      border: 1px solid var(--color-border);
      border-radius: var(--style-border-radius-inputs);
      background-color: var(--color-background);
      transition: all 0.2s ease;
      position: relative;
    }

    .checkbox__input:checked + .checkbox__box {
      background-color: var(--color-accent);
      border-color: var(--color-accent);
    }

    .checkbox__input:checked + .checkbox__box::after {
      content: '';
      position: absolute;
      left: 6px;
      top: 2px;
      width: 5px;
      height: 10px;
      border: solid white;
      border-width: 0 2px 2px 0;
      transform: rotate(45deg);
    }

    .checkbox__input:focus-visible + .checkbox__box {
      outline: 2px solid var(--color-accent);
      outline-offset: 2px;
    }

    .checkbox__input:disabled + .checkbox__box {
      opacity: 0.5;
      cursor: not-allowed;
    }

    .checkbox__text {
      font-size: var(--font-size-base);
      color: var(--color-foreground);
      line-height: 1.4;
    }

    .checkbox__help {
      margin: 0;
      padding-left: calc(20px + var(--space-3));
      font-size: var(--font-size-sm);
      color: var(--color-foreground-secondary);
    }
  }
{% endstylesheet %}
```

### Krok 2: Utwórz snippet radio.liquid

Lokalizacja: `snippets/radio.liquid`

Analogicznie do checkbox, z obsługą `options` jako pipe-separated string.

### Krok 3: Utwórz snippet switch.liquid

Lokalizacja: `snippets/switch.liquid`

Podobny do checkbox, ale z stylem przełącznika (toggle switch).

```liquid
/* CSS dla switch */
.switch__slider {
  width: 44px;
  height: 24px;
  border-radius: 24px;
  background-color: var(--color-border);
  transition: background-color 0.2s ease;
}

.switch__input:checked + .switch__slider {
  background-color: var(--color-accent);
}

.switch__slider::before {
  content: '';
  position: absolute;
  width: 20px;
  height: 20px;
  left: 2px;
  top: 2px;
  background-color: white;
  border-radius: 50%;
  transition: transform 0.2s ease;
}

.switch__input:checked + .switch__slider::before {
  transform: translateX(20px);
}
```

### Krok 4: Aktualizuj cart-discount.liquid

Znajdź i zamień:
- `spacing-*` → `space-*`
- `radius-*` → `style-*`
- `color-text-*` → `color-foreground*`

### Krok 5: Aktualizuj quantity-selector.liquid

Zunifikuj system zmiennych.

### Krok 6: Weryfikacja

```bash
shopify theme check
```

Sprawdź wizualnie:
- Strona główna (newsletter)
- Strona produktu (variant selector, buy buttons)
- Koszyk (discount, quantity)
- Strona kolekcji (filtry)

## Użycie komponentów

```liquid
{% render 'checkbox',
  name: 'newsletter',
  id: 'newsletter-signup',
  label: 'Sign up for newsletter'
%}

{% render 'radio',
  name: 'color',
  id: 'color-select',
  label: 'Select color',
  options: 'red:Red|blue:Blue|green:Green'
%}

{% render 'switch',
  name: 'notifications',
  id: 'notif-enable',
  label: 'Enable notifications',
  checked: true
%}
```
