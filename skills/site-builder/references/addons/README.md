# Add-ons

Optional capabilities layered onto the static template. One markdown file per capability, loaded only when relevant.

## How to use an add-on

When the user requests a capability (database, forms, booking, maps API, analytics, CMS…), read the matching file here and follow it. If none matches, design the integration, then **write a new add-on file documenting it** so the next site gets it for free.

## Add-on file format (keep this structure)

```markdown
# <Capability name>

## When to use
One paragraph: the user signals and use cases that justify this add-on.
The default answer is still "the static template needs nothing" — add-ons
must earn their complexity.

## Prerequisites
Accounts, MCP connectors, CLIs, API keys (and where they go: env vars,
never committed).

## Setup
Numbered, copy-pasteable steps.

## Template integration points
Exactly which files change (index.html sections, js/ modules, vercel.json)
and what new files appear. Keep js/hours.js-style separation: pure logic
modules + thin DOM glue, each testable.

## Tests
What to add to the vitest suite and the browser checklist.

## Gotchas
Anything that cost time once.
```

## Current add-ons

| File | Capability |
|------|-----------|
| `supabase.md` | Database, auth, storage, edge functions (contact forms, booking requests, galleries) |
| `google-apis.md` | Google Maps/Places APIs beyond the free keyless embed |

Planned (write when first needed): `contact-forms.md` (serverless email), `booking.md`, `analytics.md`, `cms.md`.
