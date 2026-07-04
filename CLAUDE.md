# CLAUDE.md — Nowa Marketing Website

Operating brief for Claude Code / AI collaborators working in this repo.

## What this repo is
The **Nowa marketing website**: the main site (nowaplanet.com), the blog/SEO
content engine, and the ad landing pages (`/lp`). It is the canonical
**message + conversion surface** — where ads and social send traffic, and where
pre-orders convert.

It is **not** the product/app site. App, parent-app flows, and the device
simulator live in the engineering repos. This repo moves at marketing speed and
is owned by `@marketing`.

## Read first (in order)
1. `docs/context/CUSTOMER.md` — who we're talking to (six segments, pain, language)
2. `docs/context/BRAND-VOICE.md` — voice rules and hard guardrails
3. `docs/SITEMAP.md` — information architecture + which segment each page serves
4. `docs/CONTENT-PLAN.md` — blog/SEO engine and the priority articles

The deepest source of truth for the customer is the **Customer Intelligence Hub**
in the `nowa-mkt-customer-research` repo (`research/intelligence/index.html`).
`docs/context/CUSTOMER.md` is the distilled bridge; open the Hub for detail.

## Product facts (as of July 2026 — keep current; the live LP pre-order section is the freshest truth)
- **$99 pre-order** (retail **$149**), **ships September 2026**. **DTC** launch
  (not Kickstarter — treat Kickstarter references in old docs as legacy).
- **Fully refundable** — cancel anytime before ship; **auto-refund if not shipped by Oct 31**.
- Limited to **500 reservations**; then price is $149 and the extras are gone. State the limit; never perform urgency.
- $99 reserves the **Day-One Bundle**: device + 6 months of Nowa+ + the Nowa Handbooks + Adventure Kit,
  plus pre-order extras (exclusive starter pet, badge, Nowa+ price locked 2 years). No "Founding Family" naming.
- The pet **does not speak human language** — sounds, emotion, and animation only.
  Never imply chatbot-style conversation. Don't lead with "AI companion."
- Ages **3–10** is the platform claim; purchase pull is strongest at **6–9** — skew hero imagery to 6–8.
- Full copy guardrails + facts detail: `design-system/BRAND-RULES.md`.

## Non-negotiable copy guardrails
- Say **"built with"** / **"shaped by"** the advisors — **never "clinically proven."**
- Advisors: Dr. Susanne Denham (EQ), Dr. Megan McClelland (EF), Dr. Steven Kurtz (PCIT), Dr. David Mou (business/GTM).
- Magical pet, not a chatbot toy. No surveillance / behavior-control / obedience framing.
- Do not use the phrase **"empathy-based dependency."**
- "DFK" / "deeply feeling kid" is Good Inside's term — echo the *idea* (a child wired deeply), don't lift the trademarked phrase into copy.

## Design system
Tokens in `design/tokens.css` (mirrored from the Nowa design system). Rules:
- Coral Flame `#ef493d` is the **only** CTA / action color.
- Onest for display/headings; Noto Sans for body; Tiny5 (pixel) only inside pet UI.
- "Storybook chapter" rhythm: alternate warm-parchment light sections and deep-ink dark sections.
- Buttons are full pill radius; cards 16px. Let parchment + negative space do the work.

## How we work here
- Content and structure first; the frontend dev merges his implementation in later.
  Build pages as clean semantic HTML against the design tokens so they port easily.
- Name pages for what they are. Keep durable strategy in `docs/` as Markdown.
- Ground every claim in the customer intelligence or a confirmed product fact — don't invent.
