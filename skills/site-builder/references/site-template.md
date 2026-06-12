# Site Template

File layout and the code patterns to reproduce. The Tryst reference implementation lives at `github.com/djmorgan26/tryst-salon` — consult it for full code.

## Layout

```
<business-name>/
├── index.html              # entire site, semantic sections
├── css/styles.css          # tokens + components, ~700 lines
├── js/hours.js             # hours data + open-now logic (pure, testable)
├── js/main.js              # DOM: status chips, hours table, nav, reveal, lightbox
├── images/                 # optimized photos (deployed)
├── assets/photos/          # original photos (git-tracked, .vercelignore'd)
├── assets/fonts/           # TTF for favicon generation
├── fonts/                  # self-hosted woff2 + fonts.css
├── favicon.ico/.svg, favicon-32.png, apple-touch-icon.png, icon-192/512.png
├── site.webmanifest, robots.txt
├── vercel.json             # cleanUrls, cache headers, ignoreCommand
├── package.json            # type:module, vitest devDep, test + dev scripts
├── tests/hours.test.js, tests/site.test.js
└── README.md               # run/test/deploy + fact sources
```

## js/hours.js — single source of truth

- `HOURS`: array indexed 0=Sunday…6=Saturday, `{day, open, close}` in minutes-since-midnight, `null` = closed.
- `formatTime(mins)` → "9:30 AM"; `formatRange(entry)` → "9:30 AM – 8 PM" / "Closed".
- `salonClock(date)` → `{weekday, minutes}` **in the business's IANA timezone** via `Intl.DateTimeFormat(...).formatToParts` (handle `hour === 24` → 0). Never use the visitor's local clock directly.
- `getStatus(date)` → `{isOpen, label, detail}` with "until 8 PM today" / "opens today|tomorrow|<Day> at 10 AM" by scanning the next 7 days.

`main.js` renders from this module: `[data-status]` chips (refreshed every 60s), `[data-hours-table]` rows Monday-first with today highlighted. The JSON-LD `openingHoursSpecification` must encode the same data — a test enforces it.

## index.html essentials

- Meta description with the city + real phone; OG tags; theme-color.
- JSON-LD: correct `@type` subtype, address, `telephone` E.164, `priceRange`, `foundingDate`, `aggregateRating` (only with real numbers), `openingHoursSpecification`, `sameAs` (verified socials only).
- Every `<img>`: real descriptive alt, explicit width/height, `loading="lazy"` except hero (`fetchpriority="high"`).
- Phone everywhere as `tel:+1XXXXXXXXXX`; directions via `https://www.google.com/maps/dir/?api=1&destination=<encoded>`; reviews link via maps search URL.
- `<script type="module" src="js/main.js">` at body end.

## main.js behaviors

Status chips; hours table; mobile nav (body class toggle, aria-expanded, Esc closes, header shadow on scroll); reveal-on-scroll (above-fold = immediate, below-fold = IntersectionObserver threshold 0.12, rootMargin -40px bottom, reduced-motion fallback); lightbox built once in JS (dialog role, prev/next/esc/arrow keys, caption from alt, body scroll lock); footer year.

## vercel.json

```json
{
  "cleanUrls": true,
  "trailingSlash": false,
  "ignoreCommand": "[ \"$VERCEL_GIT_COMMIT_REF\" != \"main\" ]",
  "headers": [
    { "source": "/images/(.*)", "headers": [{ "key": "Cache-Control", "value": "public, max-age=604800, stale-while-revalidate=86400" }] },
    { "source": "/fonts/(.*)",  "headers": [{ "key": "Cache-Control", "value": "public, max-age=31536000, immutable" }] }
  ]
}
```

`.vercelignore`: node_modules, assets, tests, package-lock.json, .gitignore, README.md. `.gitignore`: node_modules/, .DS_Store, .vercel.

## Responsive breakpoints

980px: 2-col grids → 1 col, hero photo first, services/reviews → 2 col, gallery → 2 col. 720px: hamburger nav, single-col cards, gallery → 1 col. Test both.
