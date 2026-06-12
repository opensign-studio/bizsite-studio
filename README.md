# bizsite-studio

Find small businesses that need a website, research them deeply, and build, test, and launch a polished site — the complete workflow, packaged. Distilled from a real end-to-end build ([tryst-salon](https://github.com/djmorgan26/tryst-salon), live at [tryst-salon.vercel.app](https://tryst-salon.vercel.app)).

## Components

| Type | Name | Purpose |
|------|------|---------|
| Command | `/find-businesses` | Prospect for businesses with no/bad websites by location, radius, category |
| Command | `/build-site` | Full pipeline for one business: research → build → test → launch |
| Skill | `business-finder` | Prospecting strategy, website-status detection, ranked output |
| Skill | `business-research` | Fact gathering + verification rules + real-photo acquisition pipeline |
| Skill | `site-builder` | Design playbook, static-site template, favicon/fonts, test suite, add-ons |
| Skill | `launch-and-domains` | GitHub, Vercel (main-only deploys), ranked domain table with buy links |

## Requirements

Works in Claude Cowork and Claude Code. Expects these to be available on the machine: Chrome with the Claude extension (research + browser testing), `git` + authenticated `gh` CLI, Node/npm (`npx vercel`), Python 3 with Pillow (favicons, image optimization), and the Vercel MCP connector (domain price checks, deployment verification). Optional: Supabase MCP (see add-ons).

## Usage

- `/find-businesses hair salons near Alpharetta GA, no website`
- `/build-site Tryst Hair Salon & Boutique, Alpharetta GA`
- Or just ask: "research this business", "build them a website", "suggest domains for it".

## Hard principles baked in

1. **Nothing fabricated.** Hours/phone verified across two sources; no invented emails, prices, reviews, or social links. Tests enforce it.
2. **Real photos only**, from the business's own public listings.
3. **Static-first.** No framework/build step unless an add-on justifies it. Easy to host anywhere.
4. **Tested before shown**: vitest suite + live browser console/network/interaction checks.
5. **Single production deploy per push to main** — preview builds skipped by config.

## Extending

Add capabilities as one markdown file each in `skills/site-builder/references/addons/` (format documented in that folder's README). Supabase and Google APIs guides included. When a new integration gets figured out on a project, write it back into an add-on so the next site gets it free.
