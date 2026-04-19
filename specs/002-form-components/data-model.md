# Data Model: Ujednolicenie komponentów formularzowych

## Komponenty

### 1. form-field (snippet - istniejący)

Uniwersalny wrapper dla pól formularza.

| Parametr | Typ | Wymagany | Opis |
|----------|-----|----------|------|
| type | string | tak | 'text', 'email', 'password', 'number', 'tel', 'textarea', 'select' |
| name | string | tak | name attribute |
| id | string | tak | id attribute |
| label | string | tak | Etykieta pola |
| value | string | nie | Wartość pola |
| placeholder | string | nie | Placeholder |
| required | boolean | nie | Czy pole wymagane |
| disabled | boolean | nie | Czy pole disabled |
| state | string | nie | 'error', 'success' |
| error_message | string | nie | Komunikat błędu |
| help_text | string | nie | Tekst pomocy |
| autocomplete | string | nie | Wartość autocomplete |
| rows | number | nie | Liczba wierszy textarea |
| select_options | string | nie | Opcje dla select (pipe-separated) |

### 2. checkbox (snippet - NOWY)

Stylowany checkbox z etykietą.

| Parametr | Typ | Wymagany | Opis |
|----------|-----|----------|------|
| name | string | tak | name attribute |
| id | string | tak | id attribute |
| value | string | nie | Wartość checkbox |
| checked | boolean | nie | Czy zaznaczony |
| disabled | boolean | nie | Czy disabled |
| label | string | tak | Etykieta |
| help_text | string | nie | Tekst pomocy |
| class | string | nie | Dodatkowe klasy CSS |

### 3. radio (snippet - NOWY)

Grupa przycisków radiowych.

| Parametr | Typ | Wymagany | Opis |
|----------|-----|----------|------|
| name | string | tak | Nazwa grupy radio |
| id | string | tak | id attribute |
| options | string | tak | Pipe-separated: 'value1:Label 1|value2:Label 2' |
| value | string | nie | Wybrana wartość |
| disabled | boolean | nie | Czy disabled |
| label | string | tak | Etykieta grupy |
| help_text | string | nie | Tekst pomocy |
| class | string | nie | Dodatkowe klasy CSS |

### 4. switch (snippet - NOWY)

Przełącznik on/off z animacją.

| Parametr | Typ | Wymagany | Opis |
|----------|-----|----------|------|
| name | string | tak | name attribute |
| id | string | tak | id attribute |
| checked | boolean | nie | Czy włączony |
| disabled | boolean | nie | Czy disabled |
| label | string | tak | Etykieta |
| help_text | string | nie | Tekst pomocy |
| class | string | nie | Dodatkowe klasy CSS |

### 5. button (snippet - istniejący)

Przycisk z wieloma wariantami.

| Parametr | Typ | Wymagany | Opis |
|----------|-----|----------|------|
| text | string | tak | Tekst przycisku |
| url | string | nie | URL (renderuje jako <a>) |
| variant | string | nie | 'primary', 'secondary', 'outline', 'ghost' |
| size | string | nie | 'small', 'medium', 'large' |
| full_width | boolean | nie | Czy na całą szerokość |
| disabled | boolean | nie | Czy disabled |
| loading | boolean | nie | Czy ładowanie |
| icon | string | nie | Ikona |
| icon_position | string | nie | 'left', 'right' |

---

## CSS Design Tokens

### Spójny system zmiennych

```css
/* Spacing */
--space-1: 0.25rem;  /* 4px */
--space-2: 0.5rem;   /* 8px */
--space-3: 0.75rem;  /* 12px */
--space-4: 1rem;     /* 16px */
--space-5: 1.25rem;  /* 20px */
--space-6: 1.5rem;   /* 24px */

/* Colors */
--color-foreground: #1a1a1a;
--color-foreground-secondary: #6b6b6b;
--color-background: #ffffff;
--color-background-2: #f5f5f5;
--color-border: #e5e5e5;
--color-border-hover: #cccccc;
--color-accent: #3b82f6;
--color-accent-rgb: 59, 130, 246;
--color-error: #dc2626;
--color-success: #16a34a;

/* Border Radius */
--style-border-radius-inputs: 6px;

/* Typography */
--font-size-sm: 0.875rem;
--font-size-base: 1rem;
--font-size-lg: 1.125rem;
--font-weight-medium: 500;
--font-weight-semibold: 600;
```

---

## Accessibility Requirements

- Wszystkie inputy muszą mieć associated `<label>`
- Checkbox/radio/switch muszą mieć `role="switch"` lub `role="radio"`
- Focus states: `outline: 2px solid var(--color-accent)`
- Keyboard navigation: Tab, Space, Enter
- ARIA labels gdzie potrzebne
- `prefers-reduced-motion` dla animacji
