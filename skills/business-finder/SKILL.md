---
name: business-finder
description: >
  This skill should be used when the user asks to "find small businesses",
  "find businesses without a website", "find clients", "prospect for web
  design clients", or wants a list of local businesses filtered by location,
  radius, category (salon, gym, restaurant, boutique, tech…), or website
  quality. Produces a ranked prospect list for the bizsite-studio workflow.
version: 0.1.0
---

# Business Finder

Find small businesses that would benefit from a new or better website, filtered by the user's criteria, and rank them as prospects.

## Parameters (all optional — ask only if everything is missing)

- **Location**: city/state/country, neighborhood, or "near me"; **radius** qualifier ("within 10 miles of Alpharetta GA").
- **Category**: hair/beauty, gym/fitness, restaurant/café, boutique/retail, dental/medical, trades, tech, etc. — or "any".
- **Website status**: `none` (no site at all), `bad` (outdated, not mobile-friendly, broken), or `any`.
- **Other**: minimum rating/review count (well-reviewed businesses make the best showcases), "longstanding", "family-owned".

## Search strategy

1. Sweep web searches combining category + location: `"<category>" <city> <state>`, `best <category> in <city>`, plus directory-targeted queries (`site:yelp.com`, `site:bestprosintown.com`, Nextdoor, Facebook pages, local "best of" lists).
2. For each candidate, capture: name, address/area, phone, rating + review count, and any website link the listings show.
3. **Determine website status** — the core signal:
   - No website field on listings + no domain in searches for `"<name>" <city>` → **none**.
   - A Facebook/Instagram page as their only web presence → **none** (counts as a prospect).
   - A domain exists → fetch it (browser tools if client-rendered). Mark **bad** if: not mobile-responsive, broken resources/SSL, years-stale content (old hours, dead links, copyright ≠ current era), builder placeholder pages, or no basic info (hours/phone) findable.
4. Verify each finalist is currently operating (recent reviews/posts within ~6 months; not "permanently closed").

## Ranking

Score prospects by: strong reputation but weak/no web presence (best gap = best client), review volume (proof the business is alive), photo availability on listings (research phase needs raw material), and category fit for a great-looking showcase (visual businesses: salons, restaurants, boutiques, gyms).

## Output

A ranked table: Rank · Business · Category · Location · Rating (count) · Website status (with one-phrase evidence) · Key links (listing, FB, current site if any). Below it, 1–2 sentence pitch angles for the top 3. Offer to start `/build-site` on any pick — the `business-research` skill takes over from there.

## Notes

- Don't contact businesses or scrape personal data; this is public-listing research only.
- Cache nothing as fact — statuses go stale; re-verify before pitching.
