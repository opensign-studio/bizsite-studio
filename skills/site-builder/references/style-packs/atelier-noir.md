# Style Pack — Atelier Noir (Immersive Dark)

A dark, cinematic, high-end experience. Reference build: tryst-atelier.vercel.app.

## Movement

Luxury atelier at night. Near-black canvas, warm gold hairlines and accents,
cream text. A characterful grotesque display (Bricolage Grotesque, optical
sizing) for headlines + a light sans (Outfit) for body/labels. Big, confident,
restrained. Gold is rare and intentional (accents, hover, today-row, one CTA).

## Navigation — fixed vertical side-rail

A **fixed left rail** (`~150px`, full height, gold hairline right border):
wordmark at top, vertical dot-nav centered (each item a small uppercase label
with a gold dot that glows on hover), and the phone number rotated
(`writing-mode: vertical-rl`) at the bottom. Main content sits in `.canvas`
with `margin-left` = rail width.
≤900px: rail becomes a 60px **top bar**, `.canvas` margin clears, hamburger
reveals a slide-down nav.

## Hero archetype — full-viewport cinematic

`min-height:100vh` with a full-bleed background photo and a strong left-to-right
dark gradient. Content left: status chip → uppercase overline → giant grotesque
h1 with a gold accent word → sub → a gold solid CTA + a hairline-outline CTA. A
"Scroll ↓" hint bottom-right. Only `<h1>`.

## Section paradigm — full-bleed panels

Tall panels separated by faint hairlines, each opening with an overline + grotesque
h2:
- **Intro/about**: copy + a balanced two-photo grid (4:5), then a 4-up **stat
  counter** strip (large gold numbers on hairline cells: rating, year, services,
  walk-ins).
- **Services as a horizontal-scroll rail** (NOT a grid): bordered dark cards with
  a gold number, scroll-snap, lift + gold border on hover.
- **Gallery**: 3-col dark grid; images slightly desaturated, brighten + gold
  border frame on hover; lightbox.
- **Boutique = full-bleed image panel** (`~80vh`) with a side dark gradient and
  overlaid copy + gold tags.
- **Reviews**: 3 dark cards with a gold top-border, gold stars, real quotes.
- **Visit**: dark bordered blocks — Hours ledger + Contact + a photo block;
  gold today-row; full-width dark map (subtle `grayscale/invert` filter).
- **Footer**: dark bar, copyright + back-to-top.

## Grid & interaction

Content offset by the rail; generous panel padding. Horizontal scroll for
services. Square edges, hairline borders (`rgba(gold,0.28)`), no soft pillowy
shadows — depth comes from value contrast and gold lines. Reveal fade-up;
optional scroll-snap on hero/boutique panels.

## Type & color logic

Bricolage Grotesque 700–800 display + Outfit 400–500 body/labels. Black
(`#0e0d0c`/`#161412`/`#1d1a17` layers), gold (`#c9a44c` + soft `#ddc488`), cream
text (`#ece6da`). Re-sample the accent metal/jewel tone from the business if it
has one; otherwise gold is the default luxe accent. Status dot uses a soft green
when open, gold when closed.
