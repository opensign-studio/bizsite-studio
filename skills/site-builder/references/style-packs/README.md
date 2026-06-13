# Style Packs

A library of **distinct site directions**. Each pack is a full *structural*
template — not a color/font swap. Picking a pack decides the skeleton; the
business decides the palette and fonts (see `../design-playbook.md` for the
shared craft: palette derivation, font self-hosting, favicons, micro-interactions).

## The rule (learned the hard way)

A "style" is **not** a palette + font swap over one fixed layout — that only
produces reskins. A real direction commits to a distinct aesthetic *movement*
with its own:

- **Hero archetype** — full-bleed cover · split · centered · side-by-side index
- **Navigation** — top bar · centered masthead · fixed vertical side-rail
- **Section paradigm** — cards · magazine spreads · full-viewport panels · numbered index
- **Grid & rhythm** — symmetric · asymmetric · strict Swiss grid · horizontal scroll
- **Interaction** — reveal-on-scroll · scroll-snap panels · filmstrip drag
- **Type & color** — decided *after* structure

### Anti-"AI-slop" rules (always)

No excessive centered layouts. No purple gradients. No uniform rounded corners
everywhere. Avoid Inter as the default — commit to a real type personality.
Keep image crops balanced (~4:5; never 3:5 strips). Make it look hand-crafted.

## Choosing a pack

Match the business's character to a direction, then confirm with the owner:

| Pack | Feels like | Good for |
|------|-----------|----------|
| `boutique-editorial.md` | Elegant, refined, classic | salons, boutiques, fine dining, florists |
| `lookbook.md` | Editorial magazine, fashion-forward | salons, studios, galleries, apparel |
| `atelier-noir.md` | Dark, immersive, luxury | high-end spas, barbers, tattoo, nightlife, fitness |
| *(future)* swiss-grid | Precise, contemporary, minimal | architecture, design, tech-leaning services |
| *(future)* warm-organic | Friendly, rounded, approachable | cafés, bakeries, kids/pets, wellness |

Every pack still obeys the same non-negotiables: real content only (no
fabrication), the `js/hours.js` single-source-of-truth, the JS hooks
(`.nav-toggle`/`#nav-menu`/`body.nav-open`, `[data-status]`, `[data-hours-table]`,
`[data-lightbox]`, `.reveal`/`data-delay`, `[data-year]`), the favicon set, and
the full test suite in `../testing-checklist.md`. Verify on mobile every time.

## Reference implementations

Live, tested builds of each pack (same business, three directions):
tryst-salon.vercel.app (boutique-editorial), tryst-lookbook.vercel.app (lookbook),
tryst-atelier.vercel.app (atelier-noir). Source under the Open Sign workspace
`sites/_demos/`. When building a new pack, add a file here following this format.
