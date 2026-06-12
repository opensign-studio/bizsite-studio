---
name: business-research
description: >
  This skill should be used when the user asks to "research a business",
  "look up a company", "find a business's hours/reviews/photos", or as the
  first phase of building a website for a small business. It covers finding
  and verifying business facts from public listings and acquiring the
  business's real photos.
version: 0.1.0
---

# Business Research

Gather every verifiable fact about one small business, plus its real photos, so a website can be built without inventing anything.

## What to collect

Name (exact, including suffixes like "& Boutique"), street address, phone, full weekly hours, founding year, owner name, rating + review count, 3–5 quotable customer reviews, list of services actually offered, amenities (walk-ins, parking, accessibility, Wi-Fi, payment types), social media links, price positioning ("reasonable prices", "$$"), and 8–12 usable photos.

## Source playbook (in order of usefulness)

1. **Web search** the business name + city + address. Note every listing site in the results.
2. **BestProsInTown** (`bestprosintown.com/<state>/<city>/<slug>`) — the best single source. Mirrors the Google Business Profile: hours table, amenity "Tips", full review texts, and a `/photos/` page with ALL Google photos. Pages are client-rendered, so use browser tools (get_page_text), not plain fetch.
3. **Fresha / booking platforms** — services list, hours cross-check.
4. **BBB profile** — founding date, owner name, legal business name.
5. **Facebook page** — recommendation %, posts, photos. Verify the page city matches before trusting it.
6. **Google Maps embed** (later, on the site) independently confirms address, name, and rating — a free verification step.

## Verification rules (hard requirements)

- **Hours**: trust only when two independent sources agree. Listings drift; pick the two most recently updated.
- **Phone/address**: must match across sources character-for-character before publishing.
- **Social links**: many same-named businesses exist in other cities. Only link profiles whose location is confirmed. When in doubt, omit.
- **Email**: if no public email exists, the site gets no email — use phone CTAs. Never guess `info@...`.
- **Reviews**: quote real public reviews, lightly trimmed; attribute generically ("Google review") unless the reviewer's name is clearly public. Never compose reviews.
- **Rating**: use the figure from the live listing (the maps embed will display it too — they must not contradict).
- Record every fact's source URL; the site's README should cite them.

## Photos

Read `references/photo-acquisition.md` before touching photos — it documents the exact extraction pipeline, the failure modes (download throttling, hotlink protection, CORS), and the working fallbacks. Summary: extract the full image URL list from the listing's photo page via browser JS, review them as a labeled contact sheet, then download the selected originals with `curl -sSL` + a browser User-Agent on the user's machine.

**Selecting photos**: prefer (1) exterior/storefront with signage, (2) the most distinctive interior shot (becomes the hero), (3) styling/work areas, (4) product or retail displays, (5) one example of actual work output. Skip: clip-art, holiday graphics, COVID signage, blurry shots, anything with non-consenting identifiable customers, and anything visibly outdated relative to newer photos of the same area.

## Output of this phase

A fact sheet (name, address, phone, hours table, founding year, rating, services, amenities, socials, review quotes — each with source) and a folder of selected original photos. Hand both to the `site-builder` skill.
