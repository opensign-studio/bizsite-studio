# Design Playbook

The visual system that produced the Tryst Hair Salon result. Reuse the bones; re-skin per business.

## Palette derivation

Sample 4–6 colors from the business's own photos: one **ink** (darkest interior tone, e.g. navy cabinetry → `#1a2634`), one **accent** (their feature color — wall paint, awning, logo), one **warm neutral background** (cream `#faf7f1` family, never pure white), one **metallic/luxe accent** (brass `#b18a4f`) for kickers and stars, optionally one deep contrast (wine). Define all as CSS custom properties. Dark sections use ink; light sections alternate cream gradients.

## Typography

- Display: high-contrast serif (Cormorant Garamond 500–700 + italic) for h1–h3 and stat numbers.
- Body/UI: light geometric sans (Jost 300–600), generous letterspacing on uppercase labels.
- Brand wordmark = business name in display serif, `letter-spacing:0.34em` with matching `text-indent` to re-center, small letterspaced subtitle underneath in the metallic accent. This IS the logo.
- Fluid sizes via `clamp()`; h1 ~`clamp(2.9rem, 6.4vw, 4.9rem)` with an italic accent-colored phrase.

## Self-hosting fonts

1. `curl -sSL -A "<browser UA>" "https://fonts.googleapis.com/css2?family=...&display=swap" -o /tmp/fonts.css` (browser UA → woff2 URLs).
2. Download each `fonts.gstatic.com` URL, rewrite the CSS to local filenames, ship as `fonts/fonts.css`. Keeps unicode-range subsets; works offline.
3. Also grab one TTF (request css2 without UA → TTF URLs) for Pillow favicon rendering.

## Favicon (Pillow)

Rounded square (radius ≈ 22% of size) in ink color, business initial in the display TTF at ~62% size optically centered, small metallic underline bar at 80% height. Render 512/192/180/32/16 PNG + multi-size .ico; hand-write an equivalent favicon.svg. Reference all in `<head>` + site.webmanifest.

## Section order (one page)

1. **Sticky header**: translucent + backdrop blur, shadow only after scroll; wordmark left, uppercase nav, phone pill button right; hamburger → slide-down panel ≤720px.
2. **Hero**: status chip (live open/closed) → h1 with italic accent phrase → one-paragraph lede → two CTAs (call = primary pill, secondary ghost) → fact row (rating / founded year / walk-ins) above a hairline. Right: best interior photo in an arch (`border-radius:999px 999px 22px 22px`, `aspect-ratio:4/5`, heavy soft shadow) + floating white rating badge card. Photo column goes `order:-1` on mobile.
3. **Ribbon**: ink background, one row of uppercase micro-items with small icons (services/walk-ins). Cheap, looks expensive.
4. **About**: overlapping photo pair (main 4:3 + inset square with thick cream border) opposite kicker + title + lede + em-dash list.
5. **Services**: 3×2 white cards — tinted rounded icon square (inline SVG line icons), serif h3, two-line description. Hover: translateY(-5px) + deeper shadow. End with a "call for pricing" note — never invent prices.
6. **Gallery**: uniform square grid (see SKILL.md rule) with hover zoom + gradient overlay; lightbox with prev/next/esc/caption.
7. **Feature section** (boutique/specialty): ink background, copy + tag pills left, 2×2 photo collage right (first figure spans 2 rows).
8. **Reviews**: 3 white cards, oversized serif open-quote glyph, metallic stars, real quotes, "Google review" footer. Below: rating line + link to the Google reviews search URL.
9. **Visit**: hours card (table from `hours.js`, today-row highlighted with a "TODAY" pill, open/closed chip on top) + contact card (address→directions link, tel:, socials, amenity pills) side by side; full-width 380px map embed below.
10. **Footer**: ink; wordmark + blurb, visit column, hours column, copyright with JS year, back-to-top.

## Micro-interactions

`.reveal` fade-up (0.7s, stagger via `data-delay`), instant for above-fold and `prefers-reduced-motion`. Status chip dot: green glow when open, wine when closed. All buttons pill-shaped, uppercase, letterspaced.
