# Feature Specification: Ujednolicenie komponentów formularzowych

**Feature Branch**: `002-form-components`
**Created**: 2026-03-01
**Status**: In Progress
**Input**: User description: "większość projektu jest gotowa. Skupmy się teraz na szczegółach. Przygotuj plan dopracowania i ujednolicenia elementów: input, select (listbox, dropdown), textarea, button, switch, toggle, etc. Wszystkie muszą mieć spójny nowoczesny wygląd."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Unified Form Input Components (Priority: P1)

Użytkownik widzi spójne, nowoczesne pola formularzy na całej stronie - od formularza kontaktowego, przez newsletter, po kod rabatowy w koszyku. Każde pole ma takie same style obramowania, paddingu, focus state i animacje.

**Why this priority**: Pola formularza są punktem kontaktu użytkownika z serwisem - ich spójność buduje zaufanie i profesjonalny wygląd.

**Independent Test**: Testowane przez odwiedzenie strony głównej, strony produktu, koszyka i sprawdzenie wizualnej spójności wszystkich pól input/textarea/select.

**Acceptance Scenarios**:

1. **Given** użytkownik na stronie głównej, **When** przewija do sekcji newslettera, **Then** pole email ma takie same style jak pole kodu rabatowego w koszyku
2. **Given** użytkownik na stronie produktu, **When** klika w pole wyboru wariantu, **Then** wszystkie elementy formularza używają tego samego systemu zmiennych CSS
3. **Given** użytkownik na stronie kontaktowej, **When** wypełnia formularz, **Then** pola tekstowe, select i textarea mają identyczne style wizualne

---

### User Story 2 - Unified Interactive Controls (Priority: P1)

Użytkownik korzysta z przycisków, checkboxów, radio buttons i switch/toggle, które mają spójny wygląd i zachowanie na całej stronie.

**Why this priority**: Interaktywne elementy sterujące są kluczowe dla używalności - muszą być rozpoznawalne i spójne.

**Independent Test**: Testowane przez interakcję z różnymi elementami na stronie - przyciskami CTA, filtrami, opcjami wariantów.

**Acceptance Scenarios**:

1. **Given** użytkownik na stronie produktu, **When** klika przycisk "Dodaj do koszyka", **Then** przycisk ma takie same style jak przycisk subskrypcji newslettera
2. **Given** użytkownik w koszyku, **When** zaznacza opcję "Paragon", **Then** checkbox/switch ma spójny wygląd z checkboxem w formularzu kontaktowym
3. **Given** użytkownik na stronie kolekcji, **When** wybiera filtry, **Then** checkboxy filtrów wyglądają tak samo jak checkboxy wariantów

---

### User Story 3 - Modern Toggle/Switch Component (Priority: P2)

Użytkownik widzi nowoczesne przełączniki (switch/toggle) zamiast standardowych checkboxów w miejscach gdzie potrzebna jest aktywacja/deaktywacja opcji.

**Why this priority**: Switch/toggle to nowoczesny wzorzec UI - użytkownicy oczekują go dla opcji włącz/wyłącz.

**Independent Test**: Testowane przez włączenie/wyłączenie opcji w formularzu i sprawdzenie wizualnej przejrzystości stanu.

**Acceptance Scenarios**:

1. **Given** użytkownik w formularzu, **When** przełącza opcję "Zapisz mnie do newslettera", **Then** widzi animowany switch z wyraźnym stanem włączony/wyłączony
2. **Given** użytkownik na stronie produktu, **When** klika w opcję "Paragon", **Then** switch pokazuje wyraźną zmianę koloru przy aktywacji

---

### Edge Cases

- Co się dzieje gdy użytkownik korzysta z urządzenia bez myszy (tylko klawiatura) - wszystkie elementy muszą być w pełni dostępne z klawiatury
- Jak system zachowuje się gdy JavaScript jest wyłączony - formularze muszą działać bez JS (progressive enhancement)
- Jak wyglądają elementy w trybie wysokiego kontrastu - muszą spełniać wymagania WCAG

---

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUSI zapewnić spójny wygląd wszystkich pól input, textarea i select na stronie poprzez ujednolicony system zmiennych CSS
- **FR-002**: System MUSI używać nowego systemu zmiennych (space-*, color-*, style-*) we wszystkich komponentach formularzowych
- **FR-003**: Użytkownik MUSI mieć dostęp do komponentów checkbox i radio button z spójnymi stylami wizualnymi
- **FR-004**: System MUSI zapewnić komponent switch/toggle dla opcji włącz/wyłącz z animowanym przejściem stanów
- **FR-005**: Wszystkie komponenty MUSZĄ spełniać wymagania dostępności (ARIA, keyboard navigation, focus states)
- **FR-006**: System MUSI zachować kompatybilność wsteczną z istniejącymi snippetami używającymi form-field.liquid

### Key Entities

- **Form Input Components**: input (text, email, password, number, tel, search), textarea, select
- **Interactive Controls**: button, checkbox, radio, switch/toggle
- **CSS Design Tokens**: space-*, color-*, radius-*, font-size-*, font-weight-*

---

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Wszystkie pola formularza (input, textarea, select) na stronie głównej, produktu, koszyka i kontaktowej wyglądają identycznie pod względem: padding, border-radius, kolorystyki, focus states
- **SC-002**: 100% komponentów formularzowych używa nowego systemu zmiennych CSS (bez starych zmiennych spacing-*, radius-*, font-size-*)
- **SC-003**: Switch/toggle component posiada płynną animację przejścia (min. 200ms) między stanami włączony/wyłączony
- **SC-004**: Wszystkie interactive controls (button, checkbox, radio, switch) mają wyraźne, spójne focus states dla keyboard navigation
- **SC-005**: Każdy komponent przechodzi weryfikację accessibility (widoczny focus, poprawne ARIA labels, keyboard operable)
