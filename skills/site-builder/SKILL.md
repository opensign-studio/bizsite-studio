---
name: site-builder
description: >
  This skill should be used when the user asks to "build a website",
  "make a site for a business", "redesign a business website", or after
  business research is complete. It covers design-system derivation,
  static-site scaffolding, favicon and font generation, accessibility,
  testing, multiple distinct design directions (style packs), and optional
  add-ons (Supabase, Google APIs, booking, etc.).
version: 0.2.0
---

# Site Builder

Build a polished, fast, zero-dependency static website for a researched small business. Optimized to look professional on the first try — and to look *different* from the last one.

Inputs: the fact sheet and photo folder from `business-research`.

## Stack (default — deviate only on request)

Plain HTML + CSS + ES-module JS. No framework, no build step. Hosts anywhere (Vercel zero-config), runs locally with any static server. Tests via Vitest. Read `references/site-template.md` for the exact file layout and code patterns; `references/style-packs/README.md` to pick the design direction; `references/design-playbook.md` for the shared craft (palette, fonts, favicons).

## Workflow

1. **Pick a style pack — vary the STRUCTURE, not just the paint.** Read
   `references/style-packs/README.md` and choose a direction that fits the
   business (boutique-editorial, lookbook, atelier-noir, …); confirm with the
   owner if unsure. The pack decides the skeleton: hero archetype, navigation,
   section paradigm, grid, interactions. **Never default every site to the same
   layout — that produces reskins, which is the #1 thing to avoid.** Then derive
   the palette and fonts from the business's own photos/signage per
   `references/design-playbook.md` (each pack names its own font personality —
   don't reuse one pairing everywhere; avoid Inter). Self-host fonts (Google
   Fonts css2 API → woff2 → rewrite CSS).
2. **Scaffold** the project per `references/site-template.md`: single source of truth for hours/open-now logic in `js/hours.js`, sections in one `index.html`, design tokens in CSS custom properties. Lay the sections out per the chosen pack.
3. **Generate brand assets**: favicon set via Pillow (monogram on brand-color rounded square; .ico + .svg + PNG sizes + apple-touch + webmanifest). The wordmark in the nav is letterspaced display type — no logo file needed.
4. **Write content from facts only.** Services come from what reviews/listings document. No prices unless published. No email unless public. Real review quotes. JSON-LD LocalBusiness (subtype it: HairSalon, Restaurant, …) generated from the same hours data the UI uses.
5. **Write the tests** (see `references/testing-checklist.md`): hours/timezone logic, real-info assertions, asset existence, alt text, structure. Tests are the no-fabrication safety net — they hard-fail on placeholder text, mailto:, or hours drift between JS and JSON-LD.
6. **Test in a real browser** before presenting: serve locally, check console errors and network 404s, click the lightbox and mobile nav, view mobile layout. See the gotchas in `references/testing-checklist.md` (occluded-window rendering freezes screenshots — verify states via JS, not pixels).

## Full build in one pass (the whole pipeline)

When asked to build a complete site for a business ("build a site for X",
"make X a website"), run the whole bizsite-studio pipeline in one continuous
pass, using the sibling skills in order — don't stop midway for questions that
research or sensible defaults can answer:

1. **Research** with `business-research` — verify every fact (hours, phone,
   address, founding year, rating, reviews, services, amenities, socials) and
   acquire the business's real photos. Never proceed on unverified/fabricated info.
2. **Pick a style pack + build** (this skill) — choose the design direction,
   derive palette/fonts from the brand, scaffold, favicons, self-host fonts, tests.
3. **Test** — unit tests + live browser checks (incl. the 390px mobile check). Fix
   everything before showing the user.
4. **Launch (ask first)** — present the local site, then offer `launch-and-domains`
   (GitHub repo, Vercel main-only deploy, ranked domain table).

Create the project in a kebab-case folder named for the business, under the Open
Sign workspace `sites/<slug>/` (one repo per client). Track progress with the task
list. Never invent contact info, prices, reviews, or socials — leave unverifiable
things out and say so. For capabilities beyond the static template, check
`references/addons/` before improvising.

## Layout rules that must be right the first time

- **Image crops stay balanced — ~4:5, never 3:5 strips.** Tall portrait crops look bad and got rejected; use `aspect-ratio:1` or `4/5` with `object-fit:cover`. The lightbox shows the uncropped original, so cropping tiles loses nothing.
- **Gallery** is either a uniform grid (`aspect-ratio:1`, 3→2→1) or the pack's filmstrip (lookbook) — never CSS-columns masonry with mixed aspect ratios. Always wire the working lightbox.
- **Map = wide and short**: full-width band, ~380px tall. Use the keyless Google Maps embed (`https://www.google.com/maps?q=<encoded name + address>&output=embed`) — it also visually verifies the listing data.
- **Reveal-on-scroll**: elements already inside the first viewport get `.is-visible` immediately at init; only below-fold elements wait on IntersectionObserver. Respect `prefers-reduced-motion`.
- **Photo curation beats photo quantity**: drop dated photos even if usable; lead with the newest distinctive shot.
- **Hero treatment is the pack's call** (arch + badge in boutique-editorial, full-bleed cover in lookbook, full-viewport cinematic in atelier-noir) — always pair it with a live open/closed status chip.
- **Mobile is not optional.** Verify every build at ~390px: hamburger nav works, any side-rail collapses to a top bar, grids reflow, and there is zero horizontal overflow. A reliable check is an in-page 390px `<iframe>` of the same-origin page — read its `documentElement.scrollWidth` and computed styles to confirm the breakpoints fire.

## Add-ons

When the user needs a capability beyond the static template — database, booking, contact forms, Google APIs, CMS, analytics — check `references/addons/` for a guide before improvising. Each add-on is one markdown file describing when to use it, setup, env vars, and exactly where it hooks into the template. To extend the plugin with a new capability, add a new file there following `references/addons/README.md`.
