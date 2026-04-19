# Implementation Plan: Ujednolicenie komponentów formularzowych

**Branch**: `002-form-components` | **Date**: 2026-03-01 | **Spec**: [spec.md](./spec.md)
**Input**: Feature specification from `/specs/002-form-components/spec.md`

## Summary

Ujednolicenie wszystkich komponentów formularzowych w motywie Shopify (input, select, textarea, button, checkbox, radio, switch/toggle) poprzez:
1. Aktualizację istniejących snippetów do używania nowego systemu zmiennych CSS
2. Ujednolicenie stylów focus states i hover states
3. Stworzenie brakujących komponentów (checkbox, radio, switch)
4. Zapewnienie pełnej dostępności (WCAG 2.1 AA)

## Technical Context

**Language/Version**: Liquid (Shopify OS 2.0), CSS3, Vanilla JavaScript ES6+
**Primary Dependencies**: Shopify CLI 3.0, brak zewnętrznych bibliotek
**Storage**: N/A (Shopify-managed)
**Testing**: `shopify theme check` (zero offenses wymagane)
**Target Platform**: Shopify themes (web)
**Project Type**: single (Shopify theme)
**Performance Goals**: Lighthouse score > 90
**Constraints**: Theme check zero offenses, WCAG 2.1 AA compliance
**Scale/Scope**: ~10 komponentów do ujednolicenia/stworzenia

## Constitution Check

- ✅ **One Codebase, Multiple Configurations** - presety przez JSON, nie hardcoded
- ✅ **Shopify OS 2.0 Standards** - sekcje/bloki/snippety z schema i LiquidDoc
- ✅ **Coding Standards** - BEM naming, mobile-first, vanilla JS, no external deps
- ✅ **Theme Check Compliance** - zero offenses wymagane
- ✅ **Git Workflow** - PR do develop, nie do main

*Brak naruszeń constitution - plan gotowy do realizacji.*

## Project Structure

### Documentation (this feature)

```
specs/002-form-components/
├── plan.md              # This file
├── spec.md              # Feature specification
├── research.md          # Phase 0 (N/A - brak niejasności)
├── data-model.md        # Phase 1: Entities i komponenty
├── quickstart.md        # Phase 1: Implementacja
└── tasks.md            # Phase 2: /speckit.tasks
```

### Source Code (repository root)

```
snippets/
├── form-field.liquid    # ✅ Istnieje - zaktualizować zmienne
├── button.liquid        # ✅ Istnieje - OK
├── checkbox.liquid      # ❌ NOWY - do stworzenia
├── radio.liquid         # ❌ NOWY - do stworzenia
├── switch.liquid        # ❌ NOWY - do stworzenia
└── ... (inne snippety)

sections/                # Sprawdzić niespójności
├── cart.liquid          # ⚠️ cart-discount snippet
├── collection.liquid    # ⚠️ filtry
└── ...

assets/
├── components.css       # Globalne style komponentów
└── critical.css         # Critical CSS
```

**Structure Decision**: Snippety w `snippets/` - reużywalne komponenty z LiquidDoc

## Complexity Tracking

*Brak naruszeń constitution - nie wymagane.*

---

# Phase 1: Design & Contracts

## Data Model

### Komponenty do utworzenia/zaktualizowania

| Komponent | Typ | Stan | Akcja |
|-----------|------|------|-------|
| form-field | snippet | ✅ istnieje | aktualizacja zmiennych |
| button | snippet | ✅ istnieje | ✅ OK |
| checkbox | snippet | ❌ brak | NOWY |
| radio | snippet | ❌ brak | NOWY |
| switch | snippet | ❌ brak | NOWY |
| quantity-selector | snippet | ✅ istnieje | aktualizacja zmiennych |
| cart-discount | snippet | ✅ istnieje | aktualizacja zmiennych |
| variant-selector | snippet | ✅ istnieje | aktualizacja stylów |

### CSS Design Tokens

```css
/* Nowy system (wymagany) */
--space-*: spacing (2, 3, 4, ...)
--color-*: foreground, background, border, accent, error, success
--style-border-radius-inputs: 4px - 8px
--font-size-*: sm, base, lg
--font-weight-*: medium, semibold

/* Stary system (do usunięcia) */
--spacing-*, --radius-*, --font-size-*, --color-text-*
```

### Interfejsy komponentów (LiquidDoc)

#### checkbox.liquid
- `name`, `id`, `value`, `checked`, `disabled`, `label`, `help_text`

#### radio.liquid
- `name`, `id`, `value`, `checked`, `disabled`, `label`, `options` (array)

#### switch.liquid
- `name`, `id`, `checked`, `disabled`, `label`, `help_text`

---

## Quickstart

### Krok 1: Utwórz checkbox.liquid
```liquid
{% doc %}
  Renders a styled checkbox input with label and help text.
  @param {string} name - Field name
  @param {string} id - Field ID
  @param {string} label - Label text
  ...
{% enddoc %}
```

### Krok 2: Utwórz radio.liquid
```liquid
{% doc %}
  Renders styled radio button group.
  @param {string} name - Radio group name
  @param {string} options - Pipe-separated options
  ...
{% enddoc %}
```

### Krok 3: Utwórz switch.liquid
```liquid
{% doc %}
  Renders toggle switch for on/off options.
  @param {string} name - Field name
  @param {boolean} checked - Initial state
  ...
{% enddoc %}
```

### Krok 4: Aktualizuj cart-discount.liquid
- Zamień `spacing-*` na `space-*`
- Zamień `radius-*` na `style-*`
- Zamień `color-text-*` na `color-foreground*`

### Krok 5: Aktualizuj quantity-selector.liquid
- Usuń mieszankę starego/nowego systemu
- Używaj tylko nowego systemu zmiennych

### Walidacja
```bash
shopify theme check
```

---

**Plan gotowy.** Następny krok: `/speckit.tasks` aby wygenerować listę zadań.
