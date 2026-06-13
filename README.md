# bizsite-studio

Find small businesses that need a website, research them deeply, and build, test, and launch a polished site — the complete workflow, packaged. Distilled from a real end-to-end build ([tryst-salon](https://github.com/djmorgan26/tryst-salon), live at [tryst-salon.vercel.app](https://tryst-salon.vercel.app)).

## Skills

Five skills, one clean linear workflow. They auto-trigger from natural language —
no separate slash commands (removed in 0.4.1 to avoid lookalike command/skill
duplicates). Invoke explicitly with `/<skill>` if you like.

| Skill | Purpose |
|-------|---------|
| `business-finder` | Prospect for businesses with no/bad websites by location, radius, category; ranked output |
| `business-research` | Fact gathering + verification rules + real-photo acquisition pipeline |
| `site-builder` | Style packs (distinct designs), static-site template, favicon/fonts, test suite, add-ons — plus the full one-pass build pipeline |
| `launch-and-domains` | GitHub, Vercel (main-only deploys), ranked domain table with buy links |
| `outreach` | Personable pitch emails: draft → user review → send via Gmail; follow-up rules; no fabricated claims about the business or the user |

## Requirements

Works in Claude Cowork and Claude Code. Expects these to be available on the machine: Chrome with the Claude extension (research + browser testing), `git` + authenticated `gh` CLI, Node/npm (`npx vercel`), Python 3 with Pillow (favicons, image optimization), and the Vercel MCP connector (domain price checks, deployment verification). Optional: Supabase MCP (see add-ons).

## Usage

Just ask in plain language — the right skill triggers automatically:

- "find hair salons near Alpharetta GA with no website" → `business-finder`
- "research Tryst Hair Salon & Boutique, Alpharetta GA" → `business-research`
- "build them a website" → `site-builder` (runs the full research → build → test → launch pass)
- "suggest domains for it" / "deploy it" → `launch-and-domains`

## Hard principles baked in

1. **Nothing fabricated.** Hours/phone verified across two sources; no invented emails, prices, reviews, or social links. Tests enforce it.
2. **Real photos only**, from the business's own public listings.
3. **Static-first.** No framework/build step unless an add-on justifies it. Easy to host anywhere.
4. **Tested before shown**: vitest suite + live browser console/network/interaction checks.
5. **Single production deploy per push to main** — preview builds skipped by config.

## Extending

Add capabilities as one markdown file each in `skills/site-builder/references/addons/` (format documented in that folder's README). Supabase and Google APIs guides included. When a new integration gets figured out on a project, write it back into an add-on so the next site gets it free.
