---
description: Research a small business and build + launch its website
argument-hint: [business name and city, or a maps/listing URL]
---

Build a complete website for the business identified by: $ARGUMENTS

Run the full bizsite-studio workflow in one continuous pass, using the plugin's skills in order:

1. **Research** — use the `business-research` skill to gather and verify every fact (hours, phone, address, founding year, rating, reviews, services, amenities, socials) and to acquire the business's real photos. Do not proceed with unverified or fabricated info.
2. **Build** — use the `site-builder` skill to derive a design system from the business's own branding, scaffold the static site, generate the favicon set, self-host fonts, and write the test suite.
3. **Test** — run the unit tests and the live browser checks described in `site-builder`. Fix everything before showing the user.
4. **Launch (ask first)** — present the finished local site, then offer the `launch-and-domains` skill: GitHub repo, Vercel deployment (main-only), and a ranked custom-domain table.

Rules:
- Create the project in a folder named after the business (kebab-case) inside the user's working folder, unless the user specifies otherwise.
- Track progress with the task list. Do not stop midway to ask questions that research or sensible defaults can answer.
- Never invent contact info, prices, reviews, or social links. If something can't be verified, leave it out and tell the user.
- If any add-on capability is requested (database, booking, Google APIs…), check `site-builder`'s `references/addons/` directory for an integration guide before improvising.
