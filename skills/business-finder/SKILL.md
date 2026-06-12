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

## The bar (strict by default)

Only two website statuses make the list — anything in between is NOT a prospect unless the user explicitly broadens the bar:

- **NONE**: no owned site at all. Listings only, Facebook/Instagram-only, a booking-platform page (Squire/Booksy/Fresha) as their sole presence, or an auto-generated directory page (`*.com-place.com`, yellowpages microsites) masquerading as a "website".
- **TRULY TERRIBLE**: 1990s/2000s-era construction (table layouts, .html page chains), broken hero images or dead resources, content frozen in time (COVID-era banners as the homepage lede, ancient copyright years), no https, or missing the absolute basics (hours, phone) entirely.

Explicitly excluded: mediocre-but-functional template sites (a dated Divi/Wix/Squarespace site with working info does not qualify), franchise locations on corporate sites, and anything that just has weak SEO.

## Where the gold is

The best hit-rate categories are old-school service businesses: **dry cleaners, shoe/boot repair, tailors & alterations, pet groomers, barbers, watch/jewelry repair, appliance/vacuum repair**, plus any business **established before ~2005** ("institution since 19xx" language). Modern boutiques, studios, and salons in trendy districts usually already have Shopify/Squarespace sites — sweep them, but expect to discard most. Neighborhood **district-association directories** (e.g. "<neighborhood> business directory") are excellent harvest lists: enumerate every non-restaurant member, then status-check each.

## Search strategy

1. Sweep web searches combining category + location: `"<category>" <city> <state>`, `best <category> in <city>`, plus directory-targeted queries (`site:yelp.com`, `site:bestprosintown.com`, Nextdoor, Facebook pages, local "best of" lists, district directories).
2. For each candidate, capture: name, address/area, phone, rating + review count, and any website link the listings show.
3. **Verify website status — never declare "none" from absence alone.** Businesses often own domains that listings don't link (e.g. a nail salon at `<name>salon.com` rather than `<name>.com`). Before marking NONE, run a dedicated search `"<name>" <city> website` including name-variant tokens (`"<nameconcatenated>"`), and check obvious domain permutations. A wrong "no website" claim kills credibility with the user — this verification is mandatory per finalist.
4. A domain exists → actually open it (browser tools if client-rendered; screenshot it) and grade against the TRULY TERRIBLE rubric above. Note the specific evidence ("homepage still leads with COVID curbside copy", "table-layout .html pages").
5. Verify each finalist is currently operating (recent reviews/posts within ~6 months; not "permanently closed"); flag ownership changes or review-quality dips as caveats.

## Ranking

Score prospects by: strong reputation but zero/terrible web presence (best gap = best client), review volume + photo availability on listings (the research phase needs raw material), proximity to the user, and dramatic before/after potential (an ancient site or beloved institution beats a generic gap).

## Estimated returns (only if asked)

If the user asks for revenue estimates, present them as **rough placeholders to calibrate with the user's own pricing — generic market ranges have proven off before**. Ask what the user actually charges (or intends to) and anchor to that; otherwise label every figure "unvalidated estimate". Recurring care-plan revenue is usually the more important line than the one-time build fee.

## Output

A ranked table: Rank · Business · Category · Location · Rating (count) · Website status (with one-phrase evidence) · Key links (listing, FB, current site if any). Below it, 1–2 sentence pitch angles for the top 3. Offer to start `/build-site` on any pick — the `business-research` skill takes over from there.

## Notes

- Don't contact businesses or scrape personal data; this is public-listing research only.
- Cache nothing as fact — statuses go stale; re-verify before pitching.
