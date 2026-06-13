# Style Pack — Lookbook (Editorial Magazine)

A print magazine rendered as a website. Reference build: tryst-lookbook.vercel.app.

## Movement

Fashion lookbook / editorial spread. Oversized display serif (Fraunces, optical
sizing) for everything large; a geometric sans (Outfit) only for small uppercase
labels, captions, folios and nav. Warm paper + ink + one warm accent (rust).
Hairline rules, page-number flourishes ("Issue No.01", "Fig. 02", "Vol. XIV"),
square edges — **no rounded corners**. Lots of negative space; asymmetric.

## Navigation — centered masthead

Two-row sticky masthead like a magazine cover:
- Row 1 (grid `1fr auto 1fr`): meta left ("Issue No.01 — City"), **centered
  wordmark** in display serif, status chip right; a hairline under the row.
- Row 2: horizontal centered nav (small uppercase sans), with the phone as a
  rust-colored item. ≤760px: row collapses, hamburger reveals the nav stacked.

## Hero archetype — full-bleed cover

A full-bleed cover photo (`min-height ~86vh`) with a dark bottom gradient and
**overlaid** text at bottom-left: small uppercase kicker → giant serif h1 with an
italic accent clause → short cover line → an underlined uppercase text link CTA
(rust underline). A folio mark ("Vol. XIV · 4.8★") top-right. The h1 is the only
`<h1>`.

## Section paradigm — magazine spreads + index

Each section opens with a **spread rule**: a centered label flanked by hairlines
(`The Salon`, `Services — A Short Index`, `Information`). Then:
- **Story spread**: asymmetric two-column. Left = body copy with a serif
  **drop-cap** (`::first-letter` float, accent color) + uppercase margin-notes.
  Right = one tall figure (4:5) with a "Fig. 01" caption.
- **Services as a numbered index** (NOT cards): an `<ol>` of rows, each a grid of
  `[number] [serif name big] / [sans description]`, separated by hairlines. Reads
  like a contents page.
- **Filmstrip gallery**: a horizontally-scrolling row of 4:5 figures with
  scroll-snap + "Fig. 0x" captions; lightbox on click. (Not a static grid.)
- **Boutique/feature spread**: ink full-bleed band, an offset two-photo pair on
  one side, a large italic **pull-quote** + copy + dot-separated tags on the other.
- **Reviews as pull-quotes**: one oversized featured quote (giant serif, rust
  quotation marks) then a two-column row of smaller real quotes with `cite`.
- **Information** ("colophon" energy): three columns — Hours ledger, Visit block,
  "Good to know" list — each under a small uppercase heading with a top rule;
  full-width map below.
- **Colophon footer**: centered big wordmark, sub, dot-separated contact meta,
  fine-print copyright.

## Grid & interaction

Wide max (~1280px) with large page edges (`clamp(1.25rem,4vw,4rem)`). Asymmetric
columns (1.1fr/0.9fr). Square corners throughout. Horizontal-scroll filmstrip.
Subtle grayscale→full on image hover. Reveal fade-up.

## Type & color logic

Fraunces 400–600 + italic for all display and pull-quotes; Outfit 400–600 for
labels/captions/nav/folios only. Paper (`#f3ede2` family), ink (`#16130f`), one
warm accent (rust `#b5512f`) — re-sample the accent from the business. Ink bands
for feature/footer.
