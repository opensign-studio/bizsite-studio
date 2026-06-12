---
name: launch-and-domains
description: >
  This skill should be used when the user asks to "deploy the site",
  "publish to Vercel", "set up GitHub for the site", "suggest domains",
  or "buy a custom domain" for a business website built with bizsite-studio.
  Covers git/GitHub setup, Vercel production deployment with main-only
  builds, and ranked custom-domain suggestions.
version: 0.1.0
---

# Launch & Domains

Take a finished, tested site live: git → GitHub → Vercel → optional custom domain. Always confirm with the user before publishing anything public.

## 1. Git + GitHub

```bash
git init -b main && git add -A && git commit -m "<business> website"
gh repo create <slug> --public --source . --push --description "<business> — live at <url>"
```

Use the user's authenticated `gh` CLI (check `gh auth status`). Commit originals in `assets/` too — the repo is the archive.

## 2. Vercel production deploy

```bash
npx vercel@latest link --yes --project <slug>   # project names must be lowercase
npx vercel@latest deploy --prod --yes
```

- `vercel` may not be globally installed — `npx vercel@latest` always works.
- A capitalized folder name fails project creation (400) — that's what `link --project <slug>` solves.
- `.vercelignore` must exclude node_modules/tests/assets before the first deploy.

## 3. Connect GitHub with single, main-only deploys

`npx vercel git connect --yes` links the repo. The template's `vercel.json` already contains the guard:

```json
"ignoreCommand": "[ \"$VERCEL_GIT_COMMIT_REF\" != \"main\" ]"
```

Effect: PR/branch preview builds are skipped (exit 0 = skip, exit 1 = build); merging a PR yields exactly one production deploy. After connecting, **stop using `vercel deploy` manually** — that's the only remaining way to double-deploy. Verify with `list_deployments`: one new production deployment per push to main, source = GitHub commit.

## 4. Custom domain suggestions

Generate 8–12 candidates from: exact name (`<business>.com`), name + category TLD (`.salon`, `.bar`, `.fit`, `.dental`, `.studio`), name + city (`<business><city>.com`), shortened name, and `.co` variants. Check each with the Vercel `check_domain_availability_and_price` tool, then present available ones ranked by (1) memorability/match to how customers say the name, (2) .com first, (3) price.

Present exactly this table format:

| Rank | Domain | Price | Period | Purchase Link |
|------|--------|-------|--------|---------------|
| 🥇 1 | trysthairsalon.com | $11.25 | 1 year | [Buy on Vercel](https://vercel.com/domains?q=trysthairsalon.com) |
| 2 | tryst.salon | $14.99 | 1 year | [Buy on Vercel](https://vercel.com/domains?q=tryst.salon) |

Purchase link format: `https://vercel.com/domains?q=<domain>`. Note taken/unavailable favorites separately. **Never purchase a domain — present the table and let the user buy.** After purchase, the user adds it under Project → Settings → Domains (or `npx vercel domains add <domain>`).

## 5. Handoff checklist

Live URL verified in a browser (console clean), repo URL, deployment model explained in one line ("push to main = deploy"), domain table delivered, and the project README updated with all of the above.
