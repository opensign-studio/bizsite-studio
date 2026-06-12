---
name: outreach
description: >
  This skill should be used when the user asks to "reach out to a business",
  "draft an outreach email", "send the pitch", "contact the owner", or wants
  to follow up after building a site with bizsite-studio. Covers personable
  pitch emails with the live site link, the draft-review-send workflow, and
  follow-up sequencing.
version: 0.1.0
---

# Outreach

Turn a finished site into a conversation with the business owner — personable, professional, zero-pressure. The pitch is "I already built this for you, come look," never "buy my services."

## Hard rules

1. **Draft first, always.** Show the user the full draft (recipient, subject, body) in chat and ask explicitly whether to send. Never send without a clear per-email "yes" — even if a previous email was approved. The user may explicitly delegate sending for a batch; only then send without re-asking, and report each send.
2. **Real recipients only.** Use a published business email (their site, listings, BBB) — never guess `info@`. If no public email exists, say so and offer the alternatives: Facebook page message, the business's contact form, a phone call script, or walking in (often best for neighborhood businesses).
3. **Truth only — about the business AND about the user.** Every claim about the business must match the verified fact sheet. Every personal claim about the user ("I'm a customer", "I live nearby", "I drive past your shop") must be confirmed by the user BEFORE drafting — never assume a relationship to make the email warmer. Ask one question up front: "What's your actual connection to this business, if any?" and write only that. A fabricated personal detail is worse than a colder email: the owner will ask about it in person. The site link must be live; click it before drafting.
4. One follow-up maximum without a reply, ~5–7 days later, shorter and lighter than the first. Never a third unsolicited email.

## Voice (what makes it land)

- Open with the user's **real, confirmed connection** — customer, neighbor, or simply "I'm a local developer and your reviews caught my eye." All three work; only one of them is true for any given business, and the user decides which. Personal-connection lines are `[ASK USER]` slots in the templates, never auto-filled.
- Compliment something **specific and earned from the research** (their 119 five-star reviews, the hand-painted 1932 sign, the stylist customers rave about) — public facts need no confirmation.
- The hook: **the site already exists and is theirs to look at** — one link, front and center.
- Zero pressure: "nothing's required of you; I built it because I think you deserve it."
- One CTA only: a quick call, or "I'll swing by." Don't stack asks.
- Pricing: do NOT put prices in the first email. If the user wants pricing included, use the user's own numbers — never invent rates.
- Sign with the user's real name and email. Short. No corporate boilerplate, no "synergy," no exclamation-point pileups.

Read `references/templates.md` for the three templates (first touch, follow-up, handoff/maintenance) and per-business personalization slots.

## Mechanics (verified working)

1. **Draft**: create with the Gmail connector's `create_draft` (it cannot send — drafts only).
2. **Review**: paste the draft in chat; ask "ready to send?"
3. **Send** (after explicit yes): the Gmail connector has no send tool — send through the browser:
   - Navigate Chrome to `https://mail.google.com/mail/u/0/#drafts`, click the draft row (it opens as a **minimized compose bar at bottom-right** — click the bar to expand), then press **Cmd+Return**.
   - Confirm the "Message sent" toast appeared (or Drafts count decremented) before reporting success.
4. **Track**: update the pipeline artifact stage to "Contacted" and note the date; schedule the one follow-up reminder if the user wants (scheduled-task tool).

## After they reply

Offer the user three lanes and draft accordingly: (a) meet/call to walk through the site, (b) straight handoff — transfer the GitHub repo + Vercel project (or deploy under their accounts) and point their domain, (c) maintenance arrangement — user keeps the repo, owner pays a recurring fee for hosting/updates; put the user's real terms in writing, nothing invented.
