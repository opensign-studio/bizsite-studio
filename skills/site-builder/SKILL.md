---
name: site-builder
description: >
  This skill should be used when the user asks to "build a website",
  "make a site for a business", "redesign a business website", or after
  business research is complete. It covers design-system derivation,
  static-site scaffolding, favicon and font generation, accessibility,
  testing, and optional add-ons (Supabase, Google APIs, booking, etc.).
version: 0.1.0
---

# Site Builder

Build a polished, fast, zero-dependency static website for a researched small business. Optimized to look boutique-professional on the first try.

Inputs: the fact sheet and photo folder from `business-research`.

## Stack (default — deviate only on request)

Plain HTML + CSS + ES-module JS. No framework, no build step. Hosts anywhere (Vercel zero-config), runs locally with any static server. Tests via Vitest. Read `references/site-template.md` for the exact file layout and code patterns; `references/design-playbook.md` for the visual system and the layout rules that were learned the hard way.

## Workflow

1. **Derive the design system from the business itself.** Pull the palette from their actual photos and signage (feature-wall color, awning, cabinetry, logo). Pair a serif display font with a geometric sans (e.g., Cormorant Garamond + Jost). Self-host fonts (see template doc — Google Fonts css2 API, download woff2s, rewrite the CSS).
2. **Scaffold** the project per `references/site-template.md`: single source of truth for hours/open-now logic in `js/hours.js`, sections in one `index.html`, design tokens in CSS custom properties.
3. **Generate brand assets**: favicon set via Pillow (monogram on brand-color rounded square; .ico + .svg + PNG sizes + apple-touch + webmanifest). The wordmark in the nav is letterspaced display type — no logo file needed.
4. **Write content from facts only.** Services come from what reviews/listings document. No prices unless published. No email unless public. Real review quotes. JSON-LD LocalBusiness (subtype it: HairSalon, Restaurant, …) generated from the same hours data the UI uses.
5. **Write the tests** (see `references/testing-checklist.md`): hours/timezone logic, real-info assertions, asset existence, alt text, structure. Tests are the no-fabrication safety net — they hard-fail on placeholder text, mailto:, or hours drift between JS and JSON-LD.
6. **Test in a real browser** before presenting: serve locally, check console errors and network 404s, click the lightbox and mobile nav, view mobile layout. See the gotchas in `references/testing-checklist.md` (occluded-window rendering freezes screenshots — verify states via JS, not pixels).

## Layout rules that must be right the first time

- **Gallery = uniform square grid** (`aspect-ratio:1`, `object-fit:cover`, 3 cols → 2 → 1). Never CSS-columns masonry with mixed aspect ratios — portrait photos render as skinny strips. The lightbox shows the uncropped original, so cropping tiles loses nothing.
- **Map = wide and short**: full-width band, ~380px tall, below the hours/contact cards (which sit side by side). Never let the map stretch to match a tall sidebar. Use the keyless Google Maps embed (`https://www.google.com/maps?q=<encoded name + address>&output=embed`) — it also visually verifies the listing data.
- **Reveal-on-scroll**: elements already inside the first viewport get `.is-visible` immediately at init; only below-fold elements wait on IntersectionObserver. Respect `prefers-reduced-motion`.
- **Photo curation beats photo quantity**: drop dated photos even if usable (compare timestamps/decor across the set); lead with the newest distinctive interior shot.
- Hero photo in an arch (`border-radius: 999px 999px R R`) with a floating rating badge reads "boutique" instantly; pair with a live open/closed status chip.

## Add-ons

When the user needs a capability beyond the static template — database, booking, contact forms, Google APIs, CMS, analytics — check `references/addons/` for a guide before improvising. Each add-on is one markdown file describing when to use it, setup, env vars, and exactly where it hooks into the template. To extend the plugin with a new capability, add a new file there following `references/addons/README.md`.
