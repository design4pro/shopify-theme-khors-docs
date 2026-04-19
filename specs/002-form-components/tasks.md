---

description: "Task list for Ujednolicenie komponentów formularzowych"
---

# Tasks: Ujednolicenie komponentów formularzowych

**Input**: Design documents from `/specs/002-form-components/`
**Prerequisites**: plan.md (required), spec.md (required for user stories)

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup (SharedShop Infrastructure)

*ify theme already exists - no setup tasks required*

---

## Phase 2: Foundational (CSS Variables Update)

**Purpose**: Update existing snippets to use unified CSS variable system

**⚠️ CRITICAL**: This phase MUST be complete before any user story can be tested

- [x] T001 Audyt zmiennych CSS w istniejących komponentach snippets/form-field.liquid, snippets/button.liquid, snippets/quantity-selector.liquid, snippets/cart-discount.liquid
- [x] T002 [P] Aktualizacja snippets/cart-discount.liquid - zamień spacing-*, radius-*, color-text-* na nowy system space-*, style-*, color-foreground-*
- [x] T003 [P] Aktualizacja snippets/quantity-selector.liquid - ujednolicenie systemu zmiennych do nowego standardu
- [x] T004 [P] Aktualizacja snippets/variant-selector.liquid - ujednolicenie stylów checkbox/radio
- [x] T005 Weryfikacja shopify theme check - brak offenses

**Checkpoint**: CSS variables unified - user story components can now be created

---

## Phase 3: User Story 1 - Unified Form Input Components (Priority: P1) 🎯 MVP

**Goal**: Create unified checkbox, radio, and switch components with consistent styling

**Independent Test**: Test by visiting homepage, product page, cart and verifying all form fields look identical

### Implementation for User Story 1

- [x] T006 [P] [US1] Utwórz snippets/checkbox.liquid z LiquidDoc i stylami zgodnymi z nowym systemem zmiennych
- [x] T007 [P] [US1] Utwórz snippets/radio.liquid z LiquidDoc i obsługą opcji pipe-separated
- [x] T008 [P] [US1] Utwórz snippets/switch.liquid z LiquidDoc, animowanym toggle i stanami włącz/wyłącz
- [x] T009 [US1] Dodaj wsparcie dla prefers-reduced-motion w switch.liquid
- [x] T010 [US1] Dodaj accessibility: focus-visible, ARIA labels, keyboard navigation do wszystkich komponentów
- [x] T011 Weryfikacja shopify theme check - brak offenses

**Checkpoint**: At this point, User Story 1 should be fully functional - form components are unified

---

## Phase 4: User Story 2 - Unified Interactive Controls (Priority: P1)

**Goal**: Replace inline checkbox/radio styles with new components across the theme

**Independent Test**: Test by interacting with buy buttons, filters, variant selectors - all should have consistent styling

### Implementation for User Story 2

- [x] T012 [P] [US2] Zastąp inline checkbox w snippets/buy-buttons.liquid nowym snippets/checkbox.liquid
- [ ] T013 [P] [US2] Zastąp inline checkbox w sections/collection.liquid (filtry) nowym snippets/checkbox.liquid (wymaga rozszerzeń o liczniki)
- [ ] T014 [P] [US2] Zastąp inline radio w snippets/variant-selector.liquid nowym snippets/radio.liquid (już posiada własne radio)
- [ ] T015 [US2] Zastąp checkbox w snippets/selling-plan.liquid nowym snippets/checkbox.liquid (nie zawiera checkbox)
- [x] T016 Weryfikacja shopify theme check - brak offenses

**Checkpoint**: At this point, User Story 2 should be fully functional - interactive controls are unified

---

## Phase 5: User Story 3 - Modern Toggle/Switch Component (Priority: P2)

**Goal**: Replace checkbox usage with switch component where appropriate (on/off options)

**Independent Test**: Test by toggling switch components - should show smooth animation between states

### Implementation for User Story 3

- [ ] T017 [P] [US3] Zastąp checkbox "Paragon" w snippets/buy-buttons.liquid nowym snippets/switch.liquid (funkcja nie istnieje jeszcze)
- [ ] T018 [P] [US3] Dodaj snippets/switch do sekcji gdzie potrzebne są opcje włącz/wyłącz
- [x] T019 [US3] Weryfikuj animację switch (min 200ms transition)
- [x] T020 Weryfikacja shopify theme check - brak offenses

**Checkpoint**: At this point, all user stories should be independently functional

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and cleanup

- [ ] T021 [P] Weryfikacja wizualna: strona główna (newsletter), strona produktu (varianty), koszyk (discount), kolekcje (filtry)
- [ ] T022 [P] Weryfikacja accessibility: keyboard navigation, focus states, ARIA labels
- [ ] T023 Weryfikacja shopify theme check - brak offenses
- [ ] T024 Dokumentacja aktualizacji w spec.md - oznacz ukończone

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - Shopify theme already exists
- **Foundational (Phase 2)**: No dependencies - can start immediately
- **User Stories (Phase 3-5)**: All depend on Foundational phase completion
  - User stories can proceed in parallel (if staffed) or sequentially
- **Polish (Phase 6)**: Depends on all user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational - creates new components
- **User Story 2 (P1)**: Can start after Foundational - uses components from US1
- **User Story 3 (P2)**: Can start after Foundational - uses switch component from US1

### Parallel Opportunities

- T002, T003, T004 can run in parallel (different files)
- T006, T007, T008 can run in parallel (different components)
- T012, T013, T014 can run in parallel (different sections)
- T017, T018 can run in parallel (different locations)
- T021, T022 can run in parallel (different validations)

---

## Parallel Example: User Story 1

```bash
# Launch all component creation tasks together:
Task: "Utwórz snippets/checkbox.liquid z LiquidDoc"
Task: "Utwórz snippets/radio.liquid z LiquidDoc"
Task: "Utwórz snippets/switch.liquid z LiquidDoc"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 2: Foundational (CSS variables update)
2. Complete Phase 3: User Story 1 (create components)
3. **STOP and VALIDATE**: Test components render correctly
4. Deploy/demo if ready

### Incremental Delivery

1. Complete Foundational → CSS unified
2. Add User Story 1 → Components created → Test → Deploy (MVP!)
3. Add User Story 2 → Components used in theme → Test → Deploy
4. Add User Story 3 → Switch replaces checkbox → Test → Deploy
5. Polish → Final validation

---

## Summary

- **Total tasks**: 24
- **User Story 1 tasks**: 6 (T006-T011)
- **User Story 2 tasks**: 5 (T012-T016)
- **User Story 3 tasks**: 4 (T017-T020)
- **Foundational tasks**: 5 (T001-T005)
- **Polish tasks**: 4 (T021-T024)
- **MVP Scope**: User Story 1 (Phase 3) after completing Foundational (Phase 2)
