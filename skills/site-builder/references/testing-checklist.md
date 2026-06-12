# Testing Checklist

Both layers are mandatory before presenting the site.

## Layer 1 — Vitest (run in any sandbox)

`tests/hours.test.js` — pure logic:
- HOURS data matches the verified hours exactly (assert each day's minutes).
- formatTime edge cases (12 AM/PM, :30 minutes); formatRange closed days.
- salonClock converts UTC→business timezone for both DST and standard time (construct dates with explicit offsets: `new Date('2026-06-10T14:00:00-04:00')`).
- getStatus: open mid-day; open exactly at opening; closed exactly at closing; "opens today at…" before opening; "opens tomorrow at…" on a closed day; "opens <Day> at…" across a weekend gap.

`tests/site.test.js` — parse index.html as a string:
- **Real-info assertions**: exact phone string + tel: link; exact street address; banned strings absent (`lorem ipsum`, `example.com`, `placeholder`, `555-`, `todo`, `fixme`); **no `mailto:`** unless a public email was verified; only verified social hosts present.
- **Structured data**: JSON-LD parses; type/name/phone/address correct; `openingHoursSpecification` mathematically equals the imported `HOURS` module (no drift).
- **Assets**: every relative `src`/`href` resolves to an existing file; full favicon set exists.
- **A11y/structure**: exactly one h1; every img has alt ≥ 8 chars; ≥10 lazy images; `aria-label`/`aria-expanded` on nav; `target="_blank"` ⇒ `rel="noopener"`; iframe has a title; `<html lang>` and viewport present.

## Layer 2 — live browser (serve + Chrome tools)

Serve from the project dir on the user's machine (`python3 -m http.server <port>`), then:

1. Fresh load → zero console errors, zero network non-200s (load the page once with tracking on, then check; tracking starts at first call, so reload with a cache-busting query).
2. Status chip and hours table render with correct "today" + open/closed for the current moment.
3. Lightbox: open, arrow-key navigate, Esc closes.
4. Mobile nav at ≤720px: opens, links close it, hamburger animates.
5. Map iframe loads and the pin shows the right business (free data verification).
6. Mobile layout: if the window won't resize (occluded/automated), render the site in a 390px iframe injected into the page and screenshot that.

### Gotchas (cost real time — remember)

- **Occluded Chrome windows freeze rendering**: IntersectionObserver, smooth-scroll, and CSS transitions don't advance, so screenshots show stale/mid-animation frames and `scrollTo` appears to do nothing. Verify states via JS (`getComputedStyle`, classList, getBoundingClientRect), not pixels — and don't "fix" animation bugs that only exist while the window is hidden.
- The above-fold reveal fix (apply `.is-visible` immediately at init for in-viewport elements) exists because of this: never gate first-screen content on observer timing.
- Browser console/network tracking only records after the first tool call on that tab — always reload after enabling.
- `npx serve`/`http.server` ports linger; kill the old listener before rebinding.
