# Supabase

## When to use
The site needs persistence or a backend: contact/booking request forms that store submissions, client galleries, testimonial moderation, simple auth. Skip for purely informational sites — phone CTAs beat forms for most local businesses.

## Prerequisites
- Supabase MCP connector or CLI, authorized.
- **Free-tier limit: 2 active projects per account.** Check `list_projects` first; if at the limit, ask the user to pause/retire one or upgrade — do not silently reuse an unrelated project for a client site.

## Setup
1. `create_project` (name = business slug; confirm the $0 cost via the confirm-cost flow).
2. Create tables with `apply_migration` (e.g., `contact_requests(id, created_at, name, phone, message, status)`), RLS ON.
3. RLS policy: anonymous INSERT only (no SELECT) for form tables.
4. Get URL + publishable key via `get_project_url` / `get_publishable_keys`. The publishable/anon key is safe to ship client-side; service keys never leave the server.

## Template integration points
- New `js/api.js`: thin fetch wrapper posting to the PostgREST endpoint with apikey headers. Pure request-building function (testable) + DOM glue in main.js.
- `index.html`: form section with honeypot field + client validation; success/failure states inline.
- Keys: inline the publishable key as a const in `js/api.js` (it is public by design) or, if a build step exists, env-inject.
- For notification emails on new submissions: Supabase Edge Function + a transactional email provider — document keys in the project README; set secrets via Supabase, never in the repo.

## Tests
- Unit: request-builder produces correct URL/headers/body; validation rejects empty/invalid input; honeypot short-circuits.
- Browser: submit a test row, verify 201 + UI success state, then delete the test row via `execute_sql`.

## Gotchas
- Storage objects aren't reachable via `execute_sql` — manage them via the storage API.
- Paused/inactive projects fail silently from the client — check project status when a form "stopped working".
