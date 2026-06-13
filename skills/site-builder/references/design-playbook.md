# Design Playbook — shared craft

This file is the **shared craft** every site uses regardless of look: palette
derivation, typography fundamentals, font self-hosting, favicons, and
micro-interactions.

**Structure is NOT in this file.** A site's skeleton (hero archetype, navigation,
section paradigm, grid, interactions) comes from a **style pack** in
`style-packs/` — pick one per build. Do not default every site to the same
layout; that produces reskins. Read `style-packs/README.md` first, choose a pack
that matches the business, then apply the craft below using that pack's structure.

**Anti-"AI-slop" (always):** no excessive centered layouts, no purple gradients,
no uniform rounded corners everywhere (intentional only in boutique-editorial),
avoid Inter as the default, keep image crops ~4:5 (never 3:5 strips), verify
mobile every time.

## Palette derivation

Sample 4–6 colors from the business's own photos: one **ink** (darkest interior tone, e.g. navy cabinetry → `#1a2634`), one **accent** (their feature color — wall paint, awning, logo), one **warm neutral background** (cream `#faf7f1` family, never pure white), one **metallic/luxe accent** (brass `#b18a4f`) for kickers and stars, optionally one deep contrast (wine). Define all as CSS custom properties. The pack decides how they're deployed (light bands vs. a dark canvas vs. paper spreads).

## Typography

Each style pack names its own font personalities — **don't reuse one pairing
everywhere** (that's a tell of reskinning). Examples in use: Cormorant Garamond +
Jost (boutique-editorial), Fraunces + Outfit (lookbook), Bricolage Grotesque +
Outfit (atelier-noir). General rules:

- Pair one **display** voice (serif or characterful grotesque) with one **sans**
  for small uppercase labels/UI; commit to a real personality (avoid Inter).
- Brand wordmark = business name set in the pack's display face — this IS the logo.
- Fluid sizes via `clamp()`; the h1 carries an accent-colored phrase.

## Self-hosting fonts

1. `curl -sSL -A "<browser UA>" "https://fonts.googleapis.com/css2?family=...&display=swap" -o /tmp/fonts.css` (browser UA → woff2 URLs).
2. Download each `fonts.gstatic.com` URL, rewrite the CSS to local filenames, ship as `fonts/fonts.css`. Keeps unicode-range subsets; works offline.
3. Also grab one TTF (request css2 without UA → TTF URLs) for Pillow favicon rendering.

## Favicon (Pillow)

Rounded square (radius ≈ 22% of size) in ink color, business initial in the display TTF at ~62% size optically centered, small metallic underline bar at 80% height. Render 512/192/180/32/16 PNG + multi-size .ico; hand-write an equivalent favicon.svg. Reference all in `<head>` + site.webmanifest.

## Section structure → see the chosen style pack

The page skeleton (header type, hero archetype, the order and treatment of
About / Services / Gallery / Feature / Reviews / Visit / Footer, grid logic) is
defined by the **style pack** you picked in `style-packs/`. Every pack covers the
same real content and keeps the same JS hooks; they differ in *how* it's laid out
(cards vs. numbered index vs. full-bleed panels, top-bar vs. masthead vs.
side-rail, etc.). Do not paste the boutique-editorial structure into every build.

Constant across packs: services end with a "call for pricing" note (never invent
prices); the gallery uses the uniform-grid OR filmstrip rule (see SKILL.md / pack)
with a working lightbox; Visit builds its hours table from `js/hours.js` with the
today-row highlighted and a live open/closed chip; the map is the keyless Google
Maps embed.

## Micro-interactions

`.reveal` fade-up (0.7s, stagger via `data-delay`), instant for above-fold and
`prefers-reduced-motion`. Status chip dot: green glow when open, accent/wine when
closed. Button shape follows the pack (pill + uppercase in boutique-editorial;
square solid/outline in lookbook and atelier-noir) — match the pack, don't
default to pills everywhere.
