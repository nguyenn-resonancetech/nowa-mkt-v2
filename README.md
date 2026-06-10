# nowa-mkt-website

Marketing website for **Nowa** — the main site (nowaplanet.com), the blog/SEO
content engine, and ad landing pages. The message + conversion surface that ads
and social point to.

> **Not** the product/app site. App and device flows live in engineering repos.
> This repo is `@marketing`-owned and moves at marketing speed.

## Start here
1. [`CLAUDE.md`](CLAUDE.md) — operating brief + product facts + guardrails
2. [`docs/context/CUSTOMER.md`](docs/context/CUSTOMER.md) — who we're talking to
3. [`docs/context/BRAND-VOICE.md`](docs/context/BRAND-VOICE.md) — voice + hard rules
4. [`docs/SITEMAP.md`](docs/SITEMAP.md) — IA + page→segment→hook map
5. [`docs/CONTENT-PLAN.md`](docs/CONTENT-PLAN.md) — blog/SEO engine

## Layout
```
design/tokens.css     Nowa design system variables (single source for color/type)
docs/                 Strategy: customer, voice, sitemap, content plan
pages/                Page builds (HTML + tokens) — content/structure specs for the dev merge
pages/lp/             Ad landing pages
blog/                 Article drafts
```

## Current state
Content + structure phase. Pages are clean semantic HTML against `design/tokens.css`
so they port directly into the frontend dev's framework when he merges his
implementation in. `pages/index.html` is the first sample (homepage).

## Preview
Open any file in `pages/` directly in a browser, or run a static server:
```
python3 -m http.server 4400
```

## Source of truth
Customer model and all numbers come from the **Customer Intelligence Hub** in
`nowa-mkt-customer-research` (`research/intelligence/index.html`). `docs/context/`
is the distilled bridge.
