# Google APIs (Maps, Places)

## When to use
Only when the free keyless pieces aren't enough. The template already uses, with **no API key**: the Maps iframe embed (`?q=<query>&output=embed`) and the directions/search deep links. Reach for real APIs when the user needs: styled/branded maps (Maps JavaScript API), live reviews/photos/hours pulled programmatically (Places API), multi-location store locators, or geocoding.

## Prerequisites
- Google Cloud project with billing (both APIs have free monthly credit).
- API key restricted by HTTP referrer to the production domain(s) + localhost — an unrestricted key in client JS is the #1 mistake.

## Setup
1. Enable "Maps JavaScript API" and/or "Places API (New)" in the Cloud console.
2. Create a browser API key; add referrer restrictions immediately.
3. Places: find the business `place_id` once (Place ID Finder) and hard-code it.

## Template integration points
- New `js/maps.js` module; loader script appended only when the map section scrolls near viewport (IntersectionObserver) to protect page speed.
- Replace the iframe in the Visit section with a `<div id="map">` — keep the 380px-tall full-width band rule.
- Places-powered reviews: render into the existing review-card components; keep the static curated quotes as fallback when the API call fails.
- Key lives in a `<meta>` or const; it's referrer-restricted, so client exposure is acceptable.

## Tests
- Unit: place-details response parser; fallback path renders static reviews on API error.
- Browser: map loads with no console errors; network shows 200 from maps.googleapis.com; page still renders fully with the API blocked.

## Gotchas
- Places hours format differs from the template's `HOURS` minutes model — convert at the boundary, keep `js/hours.js` as the single source of truth for the status chip.
- Programmatic Google photos require attribution; the embed and the research-phase photo pipeline don't.
