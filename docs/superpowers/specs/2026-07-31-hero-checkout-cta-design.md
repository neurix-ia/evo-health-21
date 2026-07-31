# Hero Checkout CTA — Design

**Date:** 2026-07-31  
**Repo:** `neurix-ia/evo-health-21`  
**Scope:** Landing page `index.html` only

## Goal

Add a prominent **“Garanta Sua Vaga”** CTA in the dark hero banner (below the subtitle) that sends users to the existing Método Evo checkout. Also point the header nav CTA to the same checkout URL. Style both CTAs yellow/gold with dark blue text.

## Context

- Checkout already exists in `#inscricao`:  
  `https://pay2.metodoevo.com.br/?uid=24cd0bc1-c0bd-4d42-8098-419fb90e019c`
- Header `Garanta sua Vaga` currently links to `#inscricao` (scroll only).
- Hero banner currently has logo + subtitle only — no CTA in the marked area below the subtitle.
- Existing `.btn-gold` uses gold gradient; text today is brand teal (`#0d5f72`). User wants **yellow background + dark blue text**.

## Decisions

| Topic | Decision |
|--------|----------|
| Approach | Reuse/extend gold button styling; update header + add hero CTA |
| Checkout URL | Same as section CTA (`pay2.metodoevo...uid=24cd0bc1-...`) |
| Header CTA | Direct checkout (option A) |
| Hero CTA | Direct checkout, larger, centered under subtitle |
| Open behavior | `target="_blank"` + `rel="noopener"` (match section CTA) |
| Colors | Yellow/gold fill (`--gold-primary` / `--gold-gradient`); text dark blue `#0a2744` |
| Out of scope | Pricing copy, regulamento, deploy pipeline, making repo private |

## UI / Components

### 1. Shared checkout href

Single URL string reused by:

- Header `.btn-nav`
- New hero CTA
- Existing `#inscricao` gold button (unchanged href)

### 2. Header

- Change `href` from `#inscricao` to checkout URL.
- Restyle `.btn-nav` (or a modifier) to yellow/gold background + dark blue text, keeping pill shape and nav size.

### 3. Hero banner

- After `.hero-banner-subtitle`, add:

```html
<a href="https://pay2.metodoevo.com.br/?uid=24cd0bc1-c0bd-4d42-8098-419fb90e019c" class="btn btn-gold btn-lg hero-banner-cta" target="_blank" rel="noopener">
  Garanta Sua Vaga
</a>
```

- CSS: center CTA under subtitle with top margin; ensure mobile spacing in existing hero media query.

### 4. Color tweak

- Ensure `.btn-gold` (and header CTA using the same palette) use text color `#0a2744` for contrast on yellow.

## Data flow

Static HTML anchors → external checkout. No JS, env vars, or backend.

## Testing

- Click header CTA → checkout opens in new tab.
- Click hero CTA → same URL in new tab.
- Section “Garantir Minha Vaga — R$ 97” still works.
- Hero CTA visible and centered on desktop and ~375px mobile.
- Contrast: yellow button + dark blue label readable on dark dotted hero.

## Non-goals / security note (informational)

Public GitHub allows reading the checkout URL; it does not allow strangers to push changes. The URL is also visible in the live site HTML. Privatizing the repo is optional hygiene, not required to protect the payment link.
