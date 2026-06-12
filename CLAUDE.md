# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Papuchón** is a static, single-page menu website for a Chilean cocktail bar/restaurant. All content is in Spanish.

## Running the Site

There is no build step. Open `index.html` directly in a browser, or serve it with any static file server:

```bash
python -m http.server 8000
# or
npx http-server .
```

No package.json, no dependencies to install, no compilation required.

## Architecture

The entire application is a single self-contained HTML file (`index.html`, ~1,426 lines). It has three parts:

- **Inline `<style>` block** — the entire stylesheet, using CSS custom properties defined in `:root`
- **HTML body** — a hero section followed by `<main class="menu-page">` containing 21 `<article>` menu sections across 5 bar categories
- **Inline `<script>` block** — ~5 lines using the `IntersectionObserver` API to trigger `.reveal` scroll animations

There are no external JS dependencies, no framework, and no API calls. Menu items are hardcoded HTML.

## CSS Conventions

All theme values are CSS custom properties set in `:root`:

```css
--gold: #C9A84C   --gold-lt: #E8C96A   --gold-pale: #F4DFA0
--black: #070707  --dark: #0D0D0D      --dark2: #141414
--cream: #F2E2C4  --dim: #9A7E50       --border: rgba(201,168,76,.22)
```

Class naming follows a BEM-adjacent prefix convention: `.hero-*`, `.sec-*`, `.item-*`, `.footer-*`. Typography uses `clamp()` throughout for fluid sizing (e.g., `clamp(2.4rem, 7vw, 5.2rem)`). Responsive breakpoints are at `max-width: 600px` and `max-width: 480px`.

Fonts (loaded via Google Fonts):
- `Playfair Display` — headings and section titles
- `Cormorant Garamond` — body text and prices
- `IM Fell English SC` — decorative labels

## Content Structure

Menu sections are `<article>` elements each containing a `.sec-header` (full-bleed photo + section title) and a `.sec-body > .items-grid` (2-column CSS grid of `.item` elements). Section numbers are rendered via CSS `counter-increment`.

The 21 sections span 5 bar categories:
1. Barra Coctelería (Mojitos, Internacional, Efervescente, Sours)
2. Barra Cervezas (Botellín, Schops, Agregados)
3. Barra Vinos y Espumantes (Espumantes, Sauvignon Blanc, Chardonnay, Carmenere, Cabernet Sauvignon)
4. Barra Destilados (Whisky, Ron, Pisco, Vodka, Gin, Licores)
5. Barra Jugos y Bebidas (Jugos, Bebidas)

## Images

Section background images are external Unsplash URLs with query params (`?w=1200&h=560&auto=format&fit=crop&q=90`). The restaurant logo is embedded as a base64-encoded PNG `<img src="data:image/png;base64,...">` — no external logo dependency.

## Git History Note

The `index.html` was deleted in the most recent commit (`5a52d07`). To restore it:

```bash
git checkout 29c1b1d -- index.html
```
