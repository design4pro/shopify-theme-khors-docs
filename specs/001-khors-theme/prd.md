# Khors Theme - Product Requirements Document (PRD)

> **Dla Claude:** WYMAGANY SUB-SKILL: Użyj superpowers:executing-plans do implementacji tego planu zadanie po zadaniu.

**Cel:** Stworzenie premium szablonu Shopify klasy światowej, spełniającego standardy 2025/2026, z trzema presetami branżowymi i architekturą Agent-Native.

**Architektura:** Shopify OS 2.0 z JSON templates, CSS BEM/Layers, Progressive Enhancement JS, Universal Commerce Protocol (UCP).

**Tech Stack:** Liquid, CSS (BEM + Layers), Vanilla JS (ES6+), Shopify CLI 3.0

**Development Store:** `khors-theme-design4pro.myshopify.com`

**Komenda dev:** `shopify theme dev --store khors-theme-design4pro.myshopify.com`

---

## Spis Treści

1. [Wizja i Cel Projektu](#1-wizja-i-cel-projektu)
2. [Presety Branżowe](#2-presety-branżowe-industry-presets)
3. [Wymagania Techniczne](#3-wymagania-techniczne)
4. [Shopify Theme Store Checklist](#4-shopify-theme-store-checklist)
5. [Content Testing Matrix](#5-content-testing-matrix)
6. [Architektura Agent-Native (UCP)](#6-architektura-agent-native-ucp)
7. [Funkcjonalności UX/UI](#7-funkcjonalności-uxui)
8. [Integracja AI](#8-integracja-ai-shopify-magic--sidekick)
9. [SEO i Structured Data](#9-seo-i-structured-data)
10. [Plan Weryfikacji](#10-plan-weryfikacji-5-stage-shopify-process)
11. [Harmonogram Rozwoju](#11-harmonogram-rozwoju)
12. [Metryki Sukcesu](#12-metryki-sukcesu)
13. [Ryzyka i Mitygacja](#13-ryzyka-i-mitygacja)
14. [Appendix](#appendix)

---

## 1. Wizja i Cel Projektu

### 1.1 Misja
Stworzenie szablonu **Khors**, który redefiniuje standardy:
- **Szybkości** (Lighthouse 90+)
- **Dostępności** (WCAG 2.1 Level AA)
- **Konwersji** (CRO-optimized)
- **AI-Native** (Universal Commerce Protocol)

### 1.2 Unikalna Propozycja Wartości (USP)
Khors to **opinionated** szablon zorientowany na konkretne branże, nie generyczne rozwiązanie "dla wszystkich". Każdy preset jest dopracowany pod specyfikę biznesową swojej kategorii.

### 1.3 Cele Biznesowe

| Cel | Metryka | Target |
|-----|---------|--------|
| Akceptacja Theme Store | Przejście review | Za pierwszym razem |
| Performance | Lighthouse Score | 90+ wszystkie kategorie |
| Dostępność | WCAG Level | AA 100% |
| Merchant Adoption | Rating | > 4.5/5 |

---

## 2. Presety Branżowe (Industry Presets)

| Preset | Nazwa Kodowa | Branża | Rozmiar Katalogu | USP |
|--------|--------------|--------|------------------|-----|
| 01 | **Aura** | Beauty/Wellness | Mały (2-10 produktów) | Storytelling, luksusowa estetyka, wideo |
| 02 | **Apex** | Electronics/Gadgets | Średni (11-100+ produktów) | Specyfikacje techniczne, porównywarka, Dark Mode |
| 03 | **Nexus** | Home & Garden | Duży (500+ produktów) | Zaawansowane filtrowanie, Mega Menu, wydajność |

### 2.1 Wymagania Struktury /listings (Standard 2025)

```
/listings/
├── aura/
│   ├── listing.json          # Metadata presetu
│   └── templates/
│       ├── index.json
│       ├── product.json
│       └── collection.json
├── apex/
│   ├── listing.json
│   └── templates/
│       └── ...
└── nexus/
    ├── listing.json
    └── templates/
        └── ...
```

---

## 3. Wymagania Techniczne

### 3.1 Standardy Kodowania

#### Liquid
- Wyłącznie `{% render %}` (zakaz `{% include %}`)
- Logika biznesowa wyciągnięta przed pętle
- Tag `{% liquid %}` dla multiline code
- LiquidDoc dla wszystkich snippetów

#### CSS
- Architektura **BEM** (Block__Element--Modifier)
- CSS Layers (`@layer`) dla zarządzania specyficznością
- Zakaz zewnętrznych frameworków (Bootstrap, Tailwind)
- Mobile-first (`min-width` media queries)
- Maksymalnie 1 poziom zagnieżdżania
- Zakaz `!important` i selektorów ID

#### JavaScript
- **Progressive Enhancement** - podstawowe funkcje bez JS
- Vanilla JS (ES6+), zakaz jQuery
- Maksymalny rozmiar: **16 KB** (minified)
- Atrybuty `defer` dla wszystkich skryptów
- Prywatne metody z prefiksem `#`

### 3.2 Wydajność (Core Web Vitals)

| Metryka | Cel Minimalny | Cel Optymalny |
|---------|---------------|---------------|
| Lighthouse Performance | 60 | 90+ |
| LCP (Largest Contentful Paint) | < 2.5s | < 1.5s |
| FID (First Input Delay) | < 100ms | < 50ms |
| CLS (Cumulative Layout Shift) | < 0.1 | < 0.05 |
| INP (Interaction to Next Paint) | < 200ms | < 100ms |

### 3.3 Dostępność (WCAG 2.1 Level AA)

- [ ] Pełna nawigacja klawiaturą
- [ ] Focus trap w modalach
- [ ] Kontrast tekstu min. 4.5:1
- [ ] Wszystkie obrazy z atrybutem `alt`
- [ ] Poprawna hierarchia nagłówków (tylko 1x `<h1>`)
- [ ] Semantyczny HTML (`<nav>`, `<main>`, `<article>`)
- [ ] Aria-labels dla elementów interaktywnych

---

## 4. Shopify Theme Store Checklist

> **KRYTYCZNE:** Ta sekcja zawiera wszystkie 131 wymagań Shopify Theme Store podzielone na **Required** (obowiązkowe) i **Recommended** (zalecane). Szablon musi spełnić 100% wymagań obowiązkowych, aby przejść review.

### 4.1 Home Page Requirements

**Minimum 25 sekcji na stronie głównej:**

| Typ Sekcji | Ilość Min | Status |
|------------|-----------|--------|
| Slideshow | 3 | Required |
| Featured Products | 5 | Required |
| Featured Collections | 3 | Required |
| Collection List | 1 | Required |
| Image with Text | 3 | Required |
| Newsletter | 1 | Required |
| Rich Text | 1 | Required |
| Blog Posts | 1 | Required |
| Video | 2 | Required |
| Unique Sections | 5+ | Required |

**Wymagania dla każdej sekcji:**

#### Required
- [ ] Sekcja widoczna na stronie głównej
- [ ] Responsywność (mobile/desktop)
- [ ] Prawidłowe renderowanie bez danych
- [ ] Możliwość dodawania/usuwania w edytorze

#### Recommended
- [ ] Animacje wejścia (intersection observer)
- [ ] Lazy loading obrazów
- [ ] Skeleton loading states

---

### 4.2 Header Requirements

#### Required
- [ ] Logo widoczne w różnych proporcjach:
  - [ ] 16:9 (landscape)
  - [ ] 4:3 (landscape)
  - [ ] 3:2 (landscape)
  - [ ] 1:1 (square)
  - [ ] 9:16 (portrait)
  - [ ] 3:4 (portrait)
  - [ ] 2:3 (portrait)
- [ ] PNG z przezroczystym tłem działa prawidłowo
- [ ] Fallback text (30-40 znaków bez spacji) wyświetla się gdy brak logo
- [ ] Logo z myślnikiem w nazwie (np. "My-Store") renderuje poprawnie
- [ ] Menu nawigacyjne:
  - [ ] 10+ pozycji w menu głównym
  - [ ] Długie tytuły 30 znaków (jedno słowo)
  - [ ] Długie tytuły 30-60 znaków (wiele słów)
  - [ ] 3 poziomy zagnieżdżenia:
    - [ ] Single tier (bez dropdown)
    - [ ] Two tier (1 poziom dropdown)
    - [ ] Three tier (2 poziomy dropdown)
- [ ] Ikona koszyka z licznikiem
- [ ] Ikona konta użytkownika
- [ ] Wyszukiwarka (pole lub ikona)

#### Recommended
- [ ] Mega Menu z obrazami promocyjnymi
- [ ] Sticky header podczas scrollowania
- [ ] Mobile drawer menu z gesturami
- [ ] Announcement bar slot

---

### 4.3 Footer Requirements

#### Required
- [ ] Minimum 5 kolumn/bloków treści
- [ ] Multiple menus z:
  - [ ] 10+ pozycji każde
  - [ ] Tytuły 30 znaków (jedno słowo)
  - [ ] Tytuły 30-60 znaków (wiele słów)
- [ ] Wszystkie ikony social media:
  - [ ] Facebook
  - [ ] Instagram
  - [ ] Twitter/X
  - [ ] YouTube
  - [ ] TikTok
  - [ ] Pinterest
  - [ ] LinkedIn
  - [ ] Snapchat
- [ ] Newsletter form:
  - [ ] Pole email input
  - [ ] Przycisk submit
  - [ ] Obsługa błędów (walidacja)
  - [ ] Komunikat sukcesu

#### Recommended
- [ ] Payment icons
- [ ] Country/Region selector
- [ ] Copyright z dynamicznym rokiem
- [ ] Back to top button

---

### 4.4 Announcement Bar Requirements

#### Required
- [ ] Tekst plain 60-100 znaków
- [ ] Rich text z:
  - [ ] Łamanie linii
  - [ ] Akapity
- [ ] Linki:
  - [ ] Wewnętrzne
  - [ ] Zewnętrzne
  - [ ] Otwieranie w tym samym oknie
  - [ ] Otwieranie w nowym oknie

#### Recommended
- [ ] Multiple announcement bars (slider)
- [ ] Countdown timer
- [ ] Dismiss button
- [ ] Różne kolory dla różnych wiadomości

---

### 4.5 Slideshow Requirements

#### Required
- [ ] Maximum **12 slajdów** (konfigurowalne)
- [ ] Każdy slideshow ma niezależne ustawienia autoplay
- [ ] Kontrolki działają podczas autoplay:
  - [ ] Previous/Next arrows
  - [ ] Dot navigation
  - [ ] Pause/Play button
- [ ] Obrazy w różnych rozmiarach:
  - [ ] 2048px (retina)
  - [ ] 1024px (standard)
- [ ] Różne proporcje obrazów:
  - [ ] 16:9, 4:3, 3:2, 1:1
  - [ ] Portrait i landscape
- [ ] Treść slajdu:
  - [ ] Heading (60 znaków)
  - [ ] Subheading (60 znaków)
  - [ ] Description (40-50 słów)
  - [ ] Button text (30 znaków, jedno i wiele słów)
  - [ ] Button link (internal/external)

#### Recommended
- [ ] Wideo w tle (YouTube, Vimeo, MP4)
- [ ] Parallax effect
- [ ] Ken Burns effect na obrazach
- [ ] Mobile-specific images

---

### 4.6 Featured Product Sections

#### Required
- [ ] **5 sekcji Featured Products** na stronie głównej
- [ ] Duplikaty produktu nie niszczą layoutu
- [ ] Różne warianty tego samego produktu pokazują się poprawnie
- [ ] Obsługa produktów:
  - [ ] Z obrazem
  - [ ] Bez obrazu (fallback title lub placeholder)
  - [ ] Z wieloma obrazami
  - [ ] Z wariantami
  - [ ] Sold out
  - [ ] Na wyprzedaży (compare at price)

#### Recommended
- [ ] Quick View modal
- [ ] Add to Cart bez przekierowania
- [ ] Variant selector inline

---

### 4.7 Featured Collection Sections

#### Required
- [ ] **3 sekcje Featured Collections** na stronie głównej
- [ ] Różne rozmiary kolekcji (1, 5, 10, 50+ produktów)
- [ ] Multiple collections nie niszczą layoutu
- [ ] Kolekcje:
  - [ ] Z featured image
  - [ ] Bez featured image (pokazuje pierwszy produkt lub tytuł)
- [ ] Produkty w kolekcji:
  - [ ] Z obrazem
  - [ ] Bez obrazu

#### Recommended
- [ ] Configurable product count
- [ ] View All link
- [ ] Carousel vs Grid toggle

---

### 4.8 Collection List Section

#### Required
- [ ] Maximum **10+ kolekcji** wyświetlanych
- [ ] Kolekcje bez obrazu:
  - [ ] Pokazują obraz pierwszego produktu LUB
  - [ ] Pokazują tekst tytułu
- [ ] Długie nazwy kolekcji (30-60 znaków) nie łamią layoutu

#### Recommended
- [ ] Configurable columns
- [ ] Hover effects
- [ ] Custom placeholder images

---

### 4.9 Image with Text Sections

#### Required
- [ ] **3 sekcje Image with Text** na stronie głównej
- [ ] Obrazy w rozmiarach:
  - [ ] 2048px (retina)
  - [ ] 1024px (standard)
- [ ] Różne proporcje:
  - [ ] 16:9, 4:3, 3:2, 1:1
  - [ ] Portrait i landscape
- [ ] Treść:
  - [ ] Heading (60 znaków)
  - [ ] Description (200+ znaków)
  - [ ] Button z linkiem

#### Recommended
- [ ] Image position (left/right)
- [ ] Background color options
- [ ] Vertical alignment options

---

### 4.10 Newsletter Section

#### Required
- [ ] Pole email input
- [ ] Przycisk submit
- [ ] Obsługa błędów (nieprawidłowy email)
- [ ] Komunikat sukcesu po zapisie
- [ ] Opis 60-100 znaków

#### Recommended
- [ ] GDPR checkbox
- [ ] Double opt-in information
- [ ] Custom success message

---

### 4.11 Rich Text Section

#### Required
- [ ] Minimum **1000 znaków** treści
- [ ] Wiele akapitów
- [ ] Formatowanie:
  - [ ] Bold, italic, underline
  - [ ] Listy (ul, ol)
  - [ ] Nagłówki (h2-h6)
- [ ] Linki:
  - [ ] Wewnętrzne
  - [ ] Zewnętrzne

#### Recommended
- [ ] Alignment options
- [ ] Custom typography settings
- [ ] Max-width control

---

### 4.12 Blog Posts Section

#### Required
- [ ] Wyświetla posty z różnymi proporcjami obrazów
- [ ] Długie tytuły (30-60 znaków) nie łamią layoutu
- [ ] Informacje o poście:
  - [ ] Tytuł
  - [ ] Featured image
  - [ ] Excerpt
  - [ ] Data publikacji
  - [ ] Autor

#### Recommended
- [ ] Configurable post count
- [ ] Category filter
- [ ] Read more link

---

### 4.13 Video Section

#### Required
- [ ] **2 sekcje Video** na stronie głównej
- [ ] Obsługa źródeł:
  - [ ] YouTube
  - [ ] Vimeo
  - [ ] MP4 (hosted)
- [ ] Multiple sekcje wideo nie niszczą strony
- [ ] Kontrolki wideo:
  - [ ] Play/Pause
  - [ ] Mute/Unmute
  - [ ] Fullscreen

#### Recommended
- [ ] Autoplay on scroll
- [ ] Loop option
- [ ] Poster image before play
- [ ] Lazy loading

---

### 4.14 Unique Sections (Custom)

#### Required
- [ ] Minimum **5 unikalnych sekcji** (nie kopiowanych z Dawn)
- [ ] Każda sekcja ma unikalne features
- [ ] Sekcje odzwierciedlają charakter branżowy presetów

**Propozycje unikalnych sekcji:**

| Sekcja | Preset | Funkcja |
|--------|--------|---------|
| Ingredient Spotlight | Aura | Showcase składników z hover info |
| Tech Specs Table | Apex | Porównywarka specyfikacji |
| Room Planner | Nexus | Wizualizacja produktów w pomieszczeniu |
| Before/After Slider | Aura | Efekty produktów kosmetycznych |
| Product Comparison | Apex | Side-by-side comparison tool |

---

### 4.15 Password Page

#### Required
- [ ] Logo/nazwa sklepu widoczne
- [ ] Logo w różnych proporcjach:
  - [ ] 16:9, 4:3, 3:2, 1:1
  - [ ] Portrait i landscape
- [ ] Formularz hasła:
  - [ ] Pole input
  - [ ] Przycisk submit
  - [ ] Obsługa błędów
  - [ ] Komunikat sukcesu
- [ ] Wiadomość merchantów **500+ znaków**
- [ ] Obrazy tła w różnych proporcjach:
  - [ ] 2048px (retina)
  - [ ] 1024px (standard)

#### Recommended
- [ ] Social links
- [ ] Newsletter signup
- [ ] Countdown to launch

---

### 4.16 Collection List Page

#### Required
- [ ] Wszystkie kolekcje widoczne
- [ ] Różne proporcje obrazów kolekcji
- [ ] Kolekcje bez obrazu pokazują:
  - [ ] Obraz pierwszego produktu LUB
  - [ ] Tytuł kolekcji
- [ ] Paginacja dla wielu kolekcji

#### Recommended
- [ ] Alphabetical sorting
- [ ] Grid/List view toggle
- [ ] Search collections

---

### 4.17 Collection Page

#### Required
- [ ] **Sortowanie:**
  - [ ] Price (low to high)
  - [ ] Price (high to low)
  - [ ] Alphabetically (A-Z)
  - [ ] Alphabetically (Z-A)
  - [ ] Date (newest first)
  - [ ] Date (oldest first)
  - [ ] Best selling
- [ ] **Filtrowanie:**
  - [ ] Storefront Filtering API
  - [ ] Tag-based filtering (legacy support)
  - [ ] Tagi 30 znaków (jedno słowo)
  - [ ] 20+ tagów nie niszczą layoutu
  - [ ] Kombinacje filtrów działają prawidłowo
- [ ] **Paginacja:**
  - [ ] Numerowana paginacja
  - [ ] Obcięcie przy 5+ stronach (1, 2, 3 ... 10)
  - [ ] Load More button
  - [ ] Infinite scrolling (opcja)
- [ ] **Product Cards:**
  - [ ] Różne proporcje obrazów (16:9, 4:3, 3:2, 1:1)
  - [ ] Badge "Sold Out"
  - [ ] Badge "Sale" (gdy compare at price)
  - [ ] Disable/replace Add to Cart dla sold out

#### Recommended
- [ ] Quick View modal
- [ ] Sidebar filters (desktop)
- [ ] Filter chips (mobile)
- [ ] Active filter indicators
- [ ] Clear all filters button
- [ ] Products per page selector
- [ ] View toggle (grid/list)

---

### 4.18 Product Page

#### Required - Product Configurations Testing

Szablon musi obsługiwać **7 konfiguracji produktów:**

| Konfiguracja | Opis | Status |
|--------------|------|--------|
| Single Product | Bez wariantów | Required |
| Sale Product | Z compare at price | Required |
| One-Option Product | 1 opcja (np. Size) | Required |
| Multi-Option Product | 2+ opcje, różne stany magazynowe | Required |
| Three-Option Product | 3 opcje (max Shopify) | Required |
| 100-Variant Product | Maximum wariantów | Required |
| No-Image Product | Bez żadnych obrazów | Required |

#### Required - Core Functionality

- [ ] **Variant Selection:**
  - [ ] Dropdown selectors
  - [ ] Color swatches (native + custom)
  - [ ] Dynamiczna zmiana ceny przy zmianie wariantu
  - [ ] Dynamiczna zmiana obrazu przy zmianie wariantu
  - [ ] Dynamiczna zmiana SKU przy zmianie wariantu
  - [ ] Strikethrough/disable dla sold out wariantów
  - [ ] Disable dla unavailable kombinacji
- [ ] **Add to Cart:**
  - [ ] Button disable gdy sold out
  - [ ] Button disable gdy unavailable
  - [ ] Błąd przy dodaniu więcej niż dostępna ilość
  - [ ] Quantity selector
- [ ] **Pricing:**
  - [ ] Regular price
  - [ ] Compare at price (przekreślona)
  - [ ] Unit price (dynamiczna zmiana przy zmianie wariantu)
  - [ ] Shop Pay Installments banner (opcjonalny)
- [ ] **Images:**
  - [ ] Główny obraz
  - [ ] Thumbnails/gallery
  - [ ] Zoom on hover/click
  - [ ] Różne proporcje (16:9, 4:3, 3:2, 1:1)
- [ ] **Content:**
  - [ ] Title (30-60 znaków)
  - [ ] Description min **1000 znaków**, wiele akapitów
  - [ ] Vendor
  - [ ] SKU
  - [ ] Barcode (opcjonalnie)

#### Required - Rich Media

- [ ] **3D Model:**
  - [ ] Przeglądanie modelu (desktop)
  - [ ] Obracanie modelu (desktop/mobile)
  - [ ] Gesty touch na mobile
- [ ] **AR (Augmented Reality):**
  - [ ] "View in your space" button (mobile only)
  - [ ] Przeglądanie obiektu w AR
  - [ ] Prawidłowe wymiary
- [ ] **Video:**
  - [ ] YouTube embed
  - [ ] Vimeo embed
  - [ ] MP4 hosted
  - [ ] Kontrolki: play/pause
  - [ ] Kontrolki: mute/unmute
- [ ] Rich media w product card nie niszczy layoutu kolekcji

#### Required - Local Pickup

- [ ] Banner dla **5+ lokalizacji** pickup
- [ ] "Check availability at other stores" link
- [ ] Zmiana tekstu "View store information" dla 1 lokalizacji
- [ ] Banner usunięty gdy pickup niedostępny
- [ ] Dynamiczna aktualizacja przy zmianie wariantu
- [ ] Obsługa sold out w konkretnych lokalizacjach

#### Required - Selling Plans (Subscriptions)

- [ ] Wybór planu subskrypcyjnego na stronie produktu
- [ ] Różne plany dla różnych produktów
- [ ] Cena subskrypcyjna vs jednorazowa

#### Recommended

- [ ] Sticky Add to Cart (mobile)
- [ ] Product recommendations
- [ ] Recently viewed products
- [ ] Share buttons (social)
- [ ] Wishlist button
- [ ] Reviews section integration
- [ ] Size guide modal
- [ ] Ingredient list (Aura preset)
- [ ] Tech specs table (Apex preset)
- [ ] Shipping estimator

---

### 4.19 Blog Page

#### Required
- [ ] Wszystkie posty widoczne
- [ ] Filtrowanie po tagach
- [ ] Tagi 30 znaków nie łamią layoutu
- [ ] Paginacja:
  - [ ] Numerowana
  - [ ] Obcięcie przy 5+ stronach
- [ ] Post information:
  - [ ] Tytuł (30-60 znaków)
  - [ ] Featured image (różne proporcje)
  - [ ] Excerpt
  - [ ] Autor
  - [ ] Data
  - [ ] Liczba komentarzy

#### Recommended
- [ ] Grid/List view toggle
- [ ] Search posts
- [ ] Category navigation

---

### 4.20 Article Page

#### Required
- [ ] Treść artykułu min **1000 znaków**, wiele akapitów
- [ ] Linki w treści:
  - [ ] Wewnętrzne
  - [ ] Zewnętrzne
- [ ] Obrazy z rich text editor wyświetlają się prawidłowo
- [ ] **Komentarze:**
  - [ ] Pole input (name, email, comment)
  - [ ] Przycisk submit
  - [ ] Obsługa błędów (walidacja)
  - [ ] Komunikat sukcesu
  - [ ] Paginacja komentarzy (opcjonalna - dla wielu komentarzy)
- [ ] Author information
- [ ] Date published
- [ ] Tags

#### Recommended
- [ ] Social share buttons
- [ ] Related posts
- [ ] Table of contents
- [ ] Reading time estimate
- [ ] Comment moderation notice

---

### 4.21 Cart Requirements

#### Required
- [ ] Wszystkie produkty w koszyku widoczne
- [ ] Scrolling dla wielu produktów
- [ ] **Quantity updates:**
  - [ ] Increase/decrease buttons
  - [ ] Direct input
  - [ ] Automatyczna aktualizacja totalu
- [ ] **Automatic discounts:**
  - [ ] Widoczne w koszyku
  - [ ] Aktualizują się dynamicznie przy zmianie ilości
- [ ] Usunięcie produktu gdy quantity = 0
- [ ] **Błąd przy przekroczeniu dostępnej ilości:**
  - [ ] Komunikat błędu
  - [ ] Nie pozwala dodać więcej niż dostępne
- [ ] Product information:
  - [ ] Image
  - [ ] Title
  - [ ] Variant info
  - [ ] Price
  - [ ] Line total
- [ ] Cart totals:
  - [ ] Subtotal
  - [ ] Discounts (if any)
  - [ ] Estimated total
- [ ] Checkout button

#### Required - Selling Plans in Cart
- [ ] Applied selling plans widoczne
- [ ] Subscription frequency visible
- [ ] Option to change plan (opcjonalne)

#### Required - Unit Pricing in Cart
- [ ] Unit price widoczny przy produktach z unit pricing

#### Recommended
- [ ] Cart drawer (AJAX, no page reload)
- [ ] Cart notes field (z opcją włączenia/wyłączenia)
- [ ] Discount code input
- [ ] Free shipping threshold indicator
- [ ] Cross-sell recommendations
- [ ] Gift wrap option
- [ ] Estimated delivery date

---

### 4.22 Search Page

#### Required
- [ ] **Predictive Search:**
  - [ ] Podpowiedzi podczas wpisywania
  - [ ] Produkty w podpowiedziach
  - [ ] Kolekcje w podpowiedziach
  - [ ] Strony w podpowiedziach
  - [ ] Artykuły w podpowiedziach
- [ ] Wyniki wyszukiwania:
  - [ ] Produkty
  - [ ] Kolekcje
  - [ ] Strony
  - [ ] Artykuły
- [ ] Paginacja wyników:
  - [ ] Numerowana
  - [ ] Load More button (opcja)
  - [ ] Infinite scroll (opcja)
- [ ] Brak wyników:
  - [ ] Komunikat "No results found"
  - [ ] Sugestie lub popular products

#### Recommended
- [ ] Filtrowanie wyników
- [ ] Sortowanie wyników
- [ ] View toggle (grid/list)
- [ ] Search within collection
- [ ] Recent searches

---

### 4.23 Generic Page Requirements

#### Required
- [ ] Treść strony widoczna
- [ ] Tytuły 30-60 znaków renderują poprawnie
- [ ] Minimum **3000 znaków** treści z multiple paragraphs
- [ ] Obrazy z rich text editor wyświetlają się jak w edytorze
- [ ] Linki (internal/external) działają
- [ ] **Testy dla WSZYSTKICH szablonów stron:**
  - [ ] page.json (default)
  - [ ] page.contact.json
  - [ ] page.faq.json (jeśli istnieje)
  - [ ] Inne custom templates

#### Recommended
- [ ] Sidebar navigation
- [ ] Breadcrumbs
- [ ] Table of contents

---

### 4.24 Contact Form Requirements

#### Required
- [ ] Pola formularza:
  - [ ] Name
  - [ ] Email
  - [ ] Message
- [ ] Przycisk submit
- [ ] Obsługa błędów (walidacja)
- [ ] Komunikat sukcesu

#### Recommended
- [ ] Phone field
- [ ] Subject dropdown
- [ ] CAPTCHA/honeypot
- [ ] File attachment

---

### 4.25 Gift Card Page

#### Required
- [ ] Kod karty w pełni widoczny (nie obcięty)
- [ ] Logo w różnych proporcjach:
  - [ ] 16:9, 4:3, 3:2, 1:1
  - [ ] Portrait i landscape
- [ ] Nazwa sklepu widoczna
- [ ] Wartość karty
- [ ] Data ważności
- [ ] Copy code button
- [ ] Print button (opcjonalne)

#### Recommended
- [ ] QR code
- [ ] Add to Apple Wallet
- [ ] Send as email

---

### 4.26 Link Sharing (Social)

#### Required
- [ ] Share linki działają:
  - [ ] Facebook
  - [ ] Twitter/X
  - [ ] Pinterest
  - [ ] Email
- [ ] **OG Image** wyświetla się prawidłowo:
  - [ ] Test Facebook Debugger
  - [ ] Test Twitter Card Validator
- [ ] OG Tags:
  - [ ] og:title
  - [ ] og:description
  - [ ] og:image
  - [ ] og:url

#### Recommended
- [ ] Copy link button
- [ ] WhatsApp share
- [ ] LinkedIn share

---

### 4.27 Local Pickup Requirements

> **Uwaga:** Wymaga konfiguracji lokalizacji w Shopify Admin

#### Required
- [ ] Banner na produkcie dla **5+ lokalizacji**
- [ ] "Check availability at other stores" link/button
- [ ] Lista lokalizacji z dostępnością
- [ ] Dynamiczna zmiana tekstu:
  - [ ] "Pick up available at [Location]" dla 1 lokalizacji
  - [ ] "Check availability" dla wielu lokalizacji
- [ ] Banner usunięty gdy:
  - [ ] Produkt niedostępny do pickup
  - [ ] Wariant sold out we wszystkich lokalizacjach
- [ ] Dynamiczna aktualizacja przy zmianie wariantu

#### Recommended
- [ ] Map view lokalizacji
- [ ] Distance from user (geolocation)
- [ ] Store hours
- [ ] Directions link

---

### 4.28 Unit Pricing Requirements

> **Uwaga:** Unit pricing wymagany dla niektórych krajów EU (DE, FR, etc.)

#### Required
- [ ] Unit price na **stronie produktu**
- [ ] Unit price na **kartach kolekcji**
- [ ] Unit price w **koszyku**
- [ ] Unit price w **zamówieniu klienta** (order confirmation)
- [ ] Dynamiczna zmiana unit price przy zmianie wariantu
- [ ] Prawidłowy format: €X.XX / unit (kg, L, m, etc.)

#### Recommended
- [ ] Unit price w quick view
- [ ] Unit price w search results

---

### 4.29 Rich Media Requirements

#### Required - 3D Models
- [ ] Przeglądanie modelu 360° (desktop)
- [ ] Obracanie gestem (mobile touch)
- [ ] Zoom in/out
- [ ] Reset view button
- [ ] Loading indicator

#### Required - AR (Augmented Reality)
- [ ] "View in your space" button widoczny tylko na mobile
- [ ] AR Quick Look (iOS)
- [ ] Scene Viewer (Android)
- [ ] Prawidłowe wymiary produktu w AR

#### Required - Video
- [ ] YouTube: embed działa
- [ ] Vimeo: embed działa
- [ ] MP4: hosted video działa
- [ ] Kontrolki:
  - [ ] Play/Pause
  - [ ] Mute/Unmute
  - [ ] Fullscreen
  - [ ] Progress bar
- [ ] Autoplay opcja (muted)

#### Recommended
- [ ] Poster image przed odtworzeniem
- [ ] Lazy loading video
- [ ] Picture-in-picture support

---

### 4.30 Selling Plans (Subscriptions)

> **Uwaga:** Wymaga aplikacji subscription (np. Recharge, Bold)

#### Required
- [ ] **Na stronie produktu:**
  - [ ] Opcja jednorazowego zakupu
  - [ ] Opcje subskrypcji (różne frequencies)
  - [ ] Cena subskrypcyjna (często z rabatem)
  - [ ] Przełączanie między opcjami aktualizuje cenę
- [ ] **W koszyku:**
  - [ ] Applied selling plan widoczny
  - [ ] Subscription frequency displayed
  - [ ] Cena z uwzględnieniem planu
- [ ] **W historii zamówień klienta:**
  - [ ] Applied selling plan widoczny
  - [ ] Subscription details

#### Recommended
- [ ] Subscription benefits explanation
- [ ] Flexibility info (pause, cancel)
- [ ] Save percentage indicator

---

## 5. Content Testing Matrix

> **KRYTYCZNE:** Przed submission każda sekcja musi być przetestowana z poniższymi wartościami

### 5.1 Text Content Testing

| Element | Test Value | Status |
|---------|------------|--------|
| Tytuł - jedno słowo | 30 znaków (np. "Supercalifragilisticexpiali") | Required |
| Tytuł - wiele słów | 30-60 znaków (np. "Amazing Product Title Here Now") | Required |
| Opis - krótki | 60-100 znaków | Required |
| Opis - długi | 200-500 znaków | Required |
| Opis - bardzo długi | 1000+ znaków, wiele akapitów | Required |
| Rich text | 3000+ znaków z formatowaniem | Required |
| Button text - jedno słowo | 30 znaków | Required |
| Button text - wiele słów | 30 znaków, 3-4 słowa | Required |

### 5.2 Image Testing

| Proporcja | Rozmiar Retina | Rozmiar Standard | Orientacja |
|-----------|---------------|------------------|------------|
| 16:9 | 2048 × 1152 px | 1024 × 576 px | Landscape |
| 4:3 | 2048 × 1536 px | 1024 × 768 px | Landscape |
| 3:2 | 2048 × 1365 px | 1024 × 683 px | Landscape |
| 1:1 | 2048 × 2048 px | 1024 × 1024 px | Square |
| 9:16 | 1152 × 2048 px | 576 × 1024 px | Portrait |
| 3:4 | 1536 × 2048 px | 768 × 1024 px | Portrait |
| 2:3 | 1365 × 2048 px | 683 × 1024 px | Portrait |

### 5.3 Edge Cases Testing

| Scenario | Expected Behavior |
|----------|-------------------|
| Produkt bez obrazu | Pokazuje placeholder lub tytuł |
| Kolekcja bez obrazu | Pokazuje obraz pierwszego produktu lub tytuł |
| Menu z 10+ pozycjami | Nie łamie layoutu, scrollowalne lub truncated |
| 100 wariantów produktu | Selector działa, strona responsive |
| 20+ tagów na kolekcji | Filtrowanie działa, nie łamie layoutu |
| 5+ stron paginacji | Pokazuje truncated pagination (1, 2, 3 ... 10) |
| Logo z myślnikiem | Renderuje prawidłowo (np. "My-Store") |
| Duplikaty produktów w sekcji | Layout nie się nie psuje |

### 5.4 Responsive Testing

| Breakpoint | Width | Required Tests |
|------------|-------|----------------|
| Mobile S | 320px | All pages render |
| Mobile M | 375px | All pages render |
| Mobile L | 425px | All pages render |
| Tablet | 768px | All pages render |
| Laptop | 1024px | All pages render |
| Desktop | 1440px | All pages render |
| Large Desktop | 2560px | All pages render |

---

## 6. Architektura Agent-Native (UCP)

### 6.1 Universal Commerce Protocol

**Lokalizacja manifestu:** `/.well-known/ucp.json`

**Wymagane Capabilities:**
| Capability | Opis | Endpoint |
|------------|------|----------|
| Discovery | Semantyczne wyszukiwanie produktów | `/api/ucp/search` |
| Cart Management | CRUD operacje na koszyku | `/api/ucp/cart` |
| Checkout | Finalizacja transakcji | `/api/ucp/checkout` |
| Negotiation | Negocjacje cen (B2B) | `/api/ucp/negotiate` |

### 6.2 Wymagania Danych

- Każdy wariant musi mieć unikalny **SKU**
- Poprawne numery **GTIN** (EAN/UPC)
- Jednostki w standardzie **UN/CEFACT**
- Atrybuty ustandaryzowane (np. zawsze "Color", nie "Shade")

### 6.3 Zabezpieczenia

- Rate Limits dla agentów AI
- Margin Threshold (minimalna marża)
- OAuth 2.0 dla Identity Linking
- Agent Payment Protocol (AP2)

---

## 7. Funkcjonalności UX/UI

### 7.1 Globalne Systemy

| System | Opis |
|--------|------|
| Style Panels | Globalne ustawienia typografii i odstępów |
| Color Schemes | Natywne schematy kolorów Shopify |
| Layout Settings | Szerokość strony, marginesy |

### 7.2 Sekcje Wymagane - Summary

#### Nagłówek i Nawigacja
- [ ] Header z logo, menu, koszyk, konto
- [ ] Mega Menu z obrazami promocyjnymi
- [ ] Sticky header (opcjonalny)
- [ ] Mobile drawer menu
- [ ] Menu 3 poziomy zagnieżdżenia
- [ ] 10+ pozycji menu

#### Strona Główna (25 sekcji)
- [ ] 3x Slideshow (12 slajdów max)
- [ ] 5x Featured Products
- [ ] 3x Featured Collections
- [ ] 1x Collection List
- [ ] 3x Image with Text
- [ ] 1x Newsletter
- [ ] 1x Rich Text
- [ ] 1x Blog Posts
- [ ] 2x Video
- [ ] 5x Unique Sections

#### Strona Produktu (PDP)
- [ ] Galeria ze zoomem
- [ ] Native Color Swatches
- [ ] Sticky Add-to-Cart (mobile)
- [ ] Metafields support
- [ ] Related Products
- [ ] Reviews section
- [ ] 3D/AR/Video support
- [ ] Local Pickup
- [ ] Selling Plans
- [ ] Unit Pricing

#### Kolekcje
- [ ] Facet navigation (API + tagi)
- [ ] Quick View modal
- [ ] 3 opcje paginacji (numbered, load more, infinite)
- [ ] Sort options (7 typów)

#### Koszyk
- [ ] Cart Drawer (AJAX)
- [ ] Cross-sell recommendations
- [ ] Discount code input
- [ ] Free shipping threshold
- [ ] Cart notes (opcjonalne)

#### Stopka
- [ ] 5+ kolumn
- [ ] Multiple menus
- [ ] Social links (wszystkie platformy)
- [ ] Payment icons
- [ ] Newsletter

### 7.3 Mikro-interakcje

- [ ] Subtelne animacje hover/focus
- [ ] Loading states dla AJAX
- [ ] Toast notifications
- [ ] Smooth scroll

---

## 8. Integracja AI (Shopify Magic & Sidekick)

### 8.1 Sekcje AI-Ready

- Modularny Liquid markup dla generowania bloków
- Dynamiczne konteksty dla AI Image Editor
- Schema Localization dla automatycznego tłumaczenia

### 8.2 Smart Search

- Predictive Search API
- Korekta literówek i synonimy
- Wyniki: produkty + FAQ + strony

### 8.3 Personalizacja Real-Time

- Logika Liquid zmieniająca layout na podstawie UTM/zachowania
- AI-driven merchandising (sortowanie produktów)

---

## 9. SEO i Structured Data

### 9.1 JSON-LD Required

- [ ] Product
- [ ] ProductGroup
- [ ] Offer
- [ ] BreadcrumbList
- [ ] Organization
- [ ] FAQPage (jeśli FAQ section)
- [ ] Review (jeśli reviews)

### 9.2 Technical SEO

- [ ] Semantyczne nagłówki H1-H6
- [ ] Automatyczne atrybuty `alt`
- [ ] Canonical URLs
- [ ] Meta tags (OG, Twitter)
- [ ] Sitemap support

---

## 10. Plan Weryfikacji (5-Stage Shopify Process)

| Etap | Obszar | Wymagania |
|------|--------|-----------|
| 1 | Podstawy techniczne | Poprawność ZIP, brak błędów Liquid, Theme Check |
| 2 | Wydajność i SEO | Lighthouse CI > 90, poprawne znaczniki |
| 3 | Dostępność | WCAG 2.1 AA, nawigacja klawiaturą, screen readers |
| 4 | Design i UX | Unikalność (nie może przypominać Dawn), 5+ unique sections |
| 5 | Pre-launch | Demo store, dokumentacja, nazewnictwo presetów |

### 10.1 Pre-Submission Checklist

#### Technical
- [ ] Theme Check: 0 errors, 0 warnings
- [ ] Lighthouse: 90+ all categories
- [ ] All required sections implemented
- [ ] All 25 home page sections working

#### Content Testing
- [ ] All text length tests passed
- [ ] All image ratio tests passed
- [ ] All edge cases handled

#### Functionality
- [ ] 7 product configurations tested
- [ ] Local Pickup working
- [ ] Selling Plans working
- [ ] Unit Pricing working
- [ ] Rich Media (3D, AR, Video) working

#### Accessibility
- [ ] WCAG 2.1 Level AA compliant
- [ ] Keyboard navigation complete
- [ ] Screen reader tested

---

## 11. Harmonogram Rozwoju

### Faza 1: Fundament (Tygodnie 1-2)
- [ ] Inicjalizacja projektu (Shopify CLI 3.0)
- [ ] Struktura katalogów z `/listings`
- [ ] Globalne ustawienia w `settings_schema.json`
- [ ] Bazowy layout (`theme.liquid`)

### Faza 2: System Designu (Tygodnie 3-5)
- [ ] CSS Layers architecture
- [ ] Color Schemes implementation
- [ ] Typography system
- [ ] Spacing/layout utilities
- [ ] Block library podstawy

### Faza 3: Core Sections (Tygodnie 6-10)
- [ ] Header/Footer (pełne wymagania checklisty)
- [ ] Announcement Bar
- [ ] 3x Slideshow sections
- [ ] 5x Featured Product sections
- [ ] 3x Featured Collection sections
- [ ] 1x Collection List
- [ ] 3x Image with Text
- [ ] 1x Newsletter
- [ ] 1x Rich Text
- [ ] 1x Blog Posts
- [ ] 2x Video sections
- [ ] 5x Unique sections
- [ ] Product page (wszystkie konfiguracje)
- [ ] Collection page (filtering, sorting, pagination)
- [ ] Cart drawer + Cart page
- [ ] Search (predictive + results page)
- [ ] Blog + Article pages
- [ ] Password page
- [ ] 404 page
- [ ] Gift Card page

### Faza 4: Advanced Features (Tygodnie 11-12)
- [ ] Rich Media (3D, AR, Video)
- [ ] Local Pickup
- [ ] Selling Plans (Subscriptions)
- [ ] Unit Pricing
- [ ] Quick View modal
- [ ] Color Swatches (native + custom)

### Faza 5: Presety (Tydzień 13)
- [ ] Aura (Beauty) configuration
- [ ] Apex (Electronics) configuration
- [ ] Nexus (Home) configuration
- [ ] Demo stores setup

### Faza 6: AI & UCP (Tydzień 14)
- [ ] UCP manifest
- [ ] JSON-LD implementation
- [ ] Predictive search enhancement
- [ ] AI-ready sections

### Faza 7: Testy i Dokumentacja (Tygodnie 15-16)
- [ ] Content Testing Matrix - wszystkie testy
- [ ] Edge cases testing
- [ ] Responsive testing wszystkie breakpointy
- [ ] Lighthouse audit
- [ ] WCAG testing
- [ ] Theme Check validation
- [ ] Merchant documentation

### Faza 8: Submission (Tydzień 17+)
- [ ] Final ZIP preparation
- [ ] Partner Dashboard submission
- [ ] Review response handling

---

## 12. Metryki Sukcesu

| KPI | Target |
|-----|--------|
| Lighthouse Score | 90+ (wszystkie kategorie) |
| Theme Check | 0 błędów, 0 ostrzeżeń |
| WCAG Compliance | 100% Level AA |
| Checklist Compliance | 100% Required items |
| Time to First Sale | < 3 miesiące po publikacji |
| Merchant Satisfaction | > 4.5/5 rating |

---

## 13. Ryzyka i Mitygacja

| Ryzyko | Prawdopodobieństwo | Impact | Mitygacja |
|--------|-------------------|--------|-----------|
| Odrzucenie przez Shopify | Niskie (po tej checkliście) | Wysoki | 100% zgodność z checklistą, wczesne testy |
| Performance issues | Średnie | Wysoki | CI/CD z Lighthouse, budżet 16KB JS |
| Konkurencja (Dawn-like) | Wysokie | Średni | 5+ unique sections, silna identyfikacja |
| Rich Media complexity | Średnie | Średni | Stopniowa implementacja, MVP |
| Local Pickup edge cases | Średnie | Średni | Extensive testing z różną liczbą lokalizacji |
| Selling Plans complexity | Średnie | Niski | Integracja z popular apps (Recharge) |

---

## Appendix A: Aktualna Struktura Projektu

```
khors-theme/
├── assets/           # 4 pliki (critical.css, ikony SVG)
├── blocks/           # 2 bloki (text, group)
├── config/           # settings_schema.json (wymaga aktualizacji)
├── layout/           # theme.liquid, password.liquid
├── locales/          # en.default.json, en.default.schema.json
├── sections/         # 16 sekcji (podstawowe)
├── snippets/         # 3 snippety
├── templates/        # 13 szablonów JSON
└── plans/            # Dokumentacja planów
    └── tmp/          # Wstępne dokumenty
```

## Appendix B: Wymagane Aktualizacje Config

1. **theme_info**: Zmiana "Skeleton" → "Khors"
2. **Color Schemes**: Dodanie natywnych schematów kolorów
3. **Typography**: Rozbudowa o secondary font
4. **Layout**: Dodanie więcej opcji szerokości

## Appendix C: Decyzje z Brainstorming Session

| Funkcja | Decyzja | Uzasadnienie |
|---------|---------|--------------|
| Rich Media (3D, AR, Video) | ✅ Pełne wsparcie | Wymagane przez checklistę |
| Selling Plans (Subscriptions) | ✅ Pełne wsparcie | Wymagane przez checklistę |
| Local Pickup | ✅ Pełne wsparcie | Wymagane przez checklistę |
| Unit Pricing | ✅ Pełne wsparcie | Wymagane dla EU markets |
| Quick View | ✅ Modal | Recommended, dobry UX |
| Pagination | ✅ Wszystkie 3 opcje | Numbered, Load More, Infinite |
| Blog Comments | ✅ Pełna obsługa | Wymagane przez checklistę |
| Color Swatches | ✅ Native + Custom | Elastyczność dla merchantów |
| Cart Notes | ✅ Z opcją włączenia | Recommended |
| Navigation | ✅ Mega Menu + 3 poziomy | Wymagane przez checklistę |
| Filtering | ✅ API + Tag-based | Storefront API + legacy |
| Search | ✅ Predictive + strona | Pełne wymagania |
| Slideshow max slides | 12 | Wystarczające dla większości |
| Shop Pay Installments | ✅ Z opcją | Recommended |
| Lighthouse target | 90+ | Theme Store requirement |

## Appendix D: Test Products Setup

Przed testowaniem utworzyć następujące produkty w development store:

1. **Test-Single**: Produkt bez wariantów
2. **Test-Sale**: Produkt z compare at price
3. **Test-OneOption**: Produkt z 1 opcją (Size: S, M, L)
4. **Test-MultiOption**: Produkt z 2 opcjami, różne stany magazynowe
5. **Test-ThreeOption**: Produkt z 3 opcjami (Color, Size, Material)
6. **Test-100Variants**: Produkt ze 100 wariantami
7. **Test-NoImage**: Produkt bez żadnych obrazów
8. **Test-3DModel**: Produkt z modelem 3D
9. **Test-Video**: Produkt z YouTube/Vimeo video
10. **Test-Subscription**: Produkt z selling plan

---

*Dokument wersja: 2.0*
*Data aktualizacji: 2026-02-01*
*Rozbudowa o Shopify Theme Store Checklist*
*Autor: Claude Code + Materiały źródłowe*
