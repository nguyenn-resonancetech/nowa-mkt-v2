# Nowa Marketing Website — Roadmap & Source of Truth

This is the working plan for completing nowaplanet.com. Tackle phases in order;
within a phase, tasks are ordered by dependency. Check items off as they land.
Strategy context: `PRODUCT.md`, `docs/context/`. Design system: `docs/DESIGN-V2.md`.

Status legend: `[x]` done · `[~]` in progress / partial · `[ ]` open

---

## Proposed site structure

Grounded in the customer intelligence: one psychographic core in six modes, a
separate Nostalgia Bridge Dad track, organic search as the #1 acquisition channel,
and comparison-shopping interception. Each page exists because a segment needs it.

```
/                    Home — the whole promise in one scroll          (v2 built)
/how-it-works        Care Loop, missions, device, a day with Nowa
/the-world           Pets, species, library — the kid-delight deep dive
/parent-app          Control, boundaries, warm insights — the trust surface
/the-science         Advisors, three pillars, mechanism — the proof page
/safety              Walled AI, COPPA, privacy — own URL (trust + search)
/compare             Nowa vs Yoto / Tonies / Lovevery / tablets
/pre-order           Conversion: $99, what's in the box, Nowa+, shipping
/faq                 Full FAQ (home carries the top 8)
/about               Mission, team, the calm-tech story
/gift                Gift framing — Nostalgia Dad + gift-givers (pre-holiday)
/guides              Content hub — cold-register entry point
/guides/{article}    Problem-query articles (8 priority, then ongoing)
/lp/{campaign}       Paid landing pages, one per segment/angle
/privacy · /terms    Legal
```

| Page | Lead segment | Why it exists |
|---|---|---|
| Home | All (universal spine) | Communicate the promise; route everywhere |
| How it works | Routine Battler, Firefighter | Make the mechanism legible |
| The World | Kids over the parent's shoulder; Nostalgia Dad | "Will my kid love it?" answered at depth |
| Parent app | Social-Emotional Worrier, Method Practitioner | Control + insight objections die here |
| The Science | Method Practitioner | "Show me the receipts" |
| Safety | Worrier; also search ("is X safe for kids") | The walled-AI story earns its own URL |
| Compare | Community Curator, gift-givers | Win the consideration set; intercept comparison SERPs |
| Pre-order | All warm | Convert with reassurance, never urgency-shaming |
| FAQ | All | Objection clearing; FAQ schema for search |
| About | Curator, press | Vet-ability; the Era-4 story |
| Gift | Nostalgia Bridge Dad | Tamagotchi memory, spec + price clarity; no guilt register |
| Guides | Cold-register entry | The #1 acquisition channel for peer brands |
| /lp/* | Per campaign | One message, one CTA, inherits ad angle |

---

## Phase 0 — Design system foundation

Turn the v2 one-off into a reusable system so every new page is assembly, not
invention. **Everything else depends on this.**

- [ ] Extract shared CSS from `pages/index-v2.html` into `design/system.css`
      (pxcard + ring layer, pxslot, buttons, chapter markers, dither, graph,
      marquee, sparkles, meter, pull-quotes, reveal system, players, FAQ,
      device-frame, footer) — keep `design/tokens.css` values-only
- [ ] Extract shared JS into `design/system.js` (reveal IO, drift marquees with
      auto-duplication, chapter rail, audio player, egg hatch, marquee padding,
      reduced-motion guards)
- [ ] Create `pages/_template.html` — head/meta block, marquee, nav, footer,
      chapter scaffold; every new page starts from it
- [ ] Refactor `index-v2.html` to consume system.css/system.js; verify no visual
      regression (Chrome side-by-side screenshots)
- [ ] Write `DESIGN.md` at repo root (Stitch format) so AI collaborators and the
      graphic team share one visual contract — tokens, components, motion rules,
      pixel-language rules (pixels illustrate / type stays warm / coral = action)
- [ ] Document component usage in `docs/DESIGN-V2.md` (one example per component)
- [ ] Decide v1 (`pages/index.html`) fate: keep as archive or delete after team review

## Phase 1 — Asset & approval integration (unblocks "real" everything)

- [ ] Graphic team delivers per `docs/PIXEL-ASSET-BRIEF.md`; swap in place:
  - [ ] HERO-DEVICE-LOOP (pixel re-render of hero-01)
  - [ ] 3 mission loops · egg-hatch sequence (optional)
  - [ ] 4 care-loop icons · 3 tab icons · 3 compare icons · 4 world icons
- [ ] Advisor quotes: collect one approved quote per advisor (Denham, McClelland,
      Kurtz, Mou); replace SAMPLE-chipped drafts; remove chips
- [ ] Beta reviews: replace the 5 drafted samples with real beta-program quotes
      (3 from LP repo data are sourced; confirm provenance with team)
- [ ] Photography: confirm visual_18/20 usage rights; shoot/source hero-adjacent
      lifestyle imagery skewed to ages 6–8 per brand rule
- [ ] Confirm product facts with team: one pet per device vs. multiple over time
      (copy currently deliberately ambiguous); Nowa+ pricing for pre-order page
- [ ] Re-export compressed videos (mission-04 was crushed to 1.2MB; review quality)

## Phase 2 — Core pages (build order = conversion impact)

Each page follows the same loop: structure outline → copy draft (warm register,
guardrails checked) → build from `_template.html` → desktop+mobile verify →
team review. Per-page details:

- [ ] **/pre-order** — the money page
  - [ ] What's in the box (device, cable, starter content; confirm with team)
  - [ ] Nowa+ explainer (what's free vs. subscription — from faq/parent-app facts)
  - [ ] Price/shipping/cancel-anytime reassurance block; ships-Sept-2026 timeline
  - [ ] Reservation form or checkout integration decision (Stripe? waitlist tool?)
        — needs a team decision before build
  - [ ] FAQ subset (shipping, cancellation, warranty)
- [ ] **/how-it-works** — deep mechanism
  - [ ] Care Loop expanded (the 4 steps with mission videos inline)
  - [ ] "A day with Nowa" timeline (morning → school → evening → bedtime)
  - [ ] Device section expanded (blueprint, buttons, what's NOT in it)
  - [ ] Missions catalogue preview (habit/EQ/EF examples by age band)
- [ ] **/parent-app** — the trust surface
  - [ ] Use the 4 parent-app UI mockups + how-nowa-works-03 video (already inventoried)
  - [ ] Mission Control / Growth insights / Expert guidance / Safe-by-design
        sections (copy base exists in LP repo parent-app.json — rewrite post-pivot)
  - [ ] Nowa+ free-vs-paid table
- [ ] **/the-science** — the receipts
  - [ ] Advisor full profiles (credentials, external links from advisory.json)
  - [ ] Three pillars with the actual frameworks (Denham SEC, McClelland HTKS/EF,
        Kurtz PCIT) — "built with", never "clinically proven"
  - [ ] How development is woven into missions (age-banding explainer)
- [ ] **/the-world** — kid-delight deep dive
  - [ ] Species gallery (all 12 sprites, backstories from team if they exist)
  - [ ] Library showcase expanded (more playable samples, unlock mechanic)
  - [ ] Egg/hatch story; variety-not-collection framing throughout
- [ ] **/safety** — own URL
  - [ ] Walled AI explainer (nothing to say, everything to feel)
  - [ ] COPPA + ASTM F963 statements (legal review required)
  - [ ] Data practices in plain language; parent-control summary
- [ ] **/compare** — expanded showdown
  - [ ] Honest per-competitor pages-worth of detail (Yoto, Tonies, Lovevery, tablets)
  - [ ] Comparison table (screen-free / alive / develops / bond / price)
  - [ ] Target comparison search queries (SEO titles/meta)
- [ ] **/faq** — full version (homepage 8 + shipping, warranty, battery, wifi,
      languages, sibling profiles, what-if-it-breaks; FAQPage schema)
- [ ] **/about** — mission, team, Era-4/calm-tech story, press kit link
- [ ] **/gift** — Nostalgia Dad register (nostalgia visuals, spec + price clarity,
      gift box/wrap info; NO guilt-repair register) — build by October for holidays
- [ ] **/privacy + /terms** — adapt from LP repo's existing pages; legal review

## Phase 3 — Content engine (/guides)

- [ ] Guides hub page (cold-register titles, segment filtering, warm design)
- [ ] Article template page (structure per CONTENT-PLAN.md: her words → why →
      try tonight → where Nowa fits → built-with proof; Article schema; soft CTA)
- [ ] Write + ship the 8 priority articles (see docs/CONTENT-PLAN.md table;
      target: all live by mid-July 2026)
  - [ ] 1 — Stop yelling (Healing Parent)
  - [ ] 2 — Morning routine battle (Routine Battler)
  - [ ] 3 — Calm an angry child (Firefighter)
  - [ ] 4 — Bedtime battles at 5 (Routine Battler)
  - [ ] 5 — Deeply feeling child (idea, not trademark)
  - [ ] 6 — Screen-time alternatives at 6 (Battler/Curator)
  - [ ] 7 — Social skills practice at home (Worrier)
  - [ ] 8 — Picky eater battles (Routine Battler)
- [ ] Internal linking pass (guides ↔ science ↔ how-it-works ↔ pre-order)
- [ ] Ongoing cadence plan from the Pareto-80 keyword list (audience report)

## Phase 4 — Campaign landing pages (/lp)

- [ ] LP template: one message, one CTA, no nav escape hatches, inherits ad angle
- [ ] Launch set (one per proven angle):
  - [ ] Healing Parent — "a second regulated nervous system in the room"
  - [ ] Routine Battler — "the morning routine, minus the referee"
  - [ ] Method Practitioner — "built with the scientists" (receipts-forward)
  - [ ] Nostalgia Bridge Dad — Tamagotchi-memory creative, spec + price
- [ ] UTM/conversion tracking conventions documented per LP

## Phase 5 — Production merge (with Huy)

- [ ] Handoff session: walk DESIGN.md + system.css/js + this roadmap
- [ ] Map our sections → his Nuxt component/data-file architecture (copy lives in
      data files; confirm which components are new builds)
- [ ] Port design tokens into his Tailwind v4 theme (reconcile with the pixel-art
      README era — our tokens win per team decision)
- [ ] Fix pre-pivot copy in his repo (conversational-AI FAQ answers, "friend who
      remembers" framing, waitlist→pre-order) — flagged in ASSET-INVENTORY.md
- [ ] Move media to proper hosting (S3/CDN with cache headers; videos out of git)
- [ ] Analytics: GA4 + ad pixels + conversion events (pre-order click, audio play,
      egg hatch, scroll depth) — define the event schema together
- [ ] SEO tech: per-page meta/OG images, sitemap.xml, robots, canonical,
      structured data (Product, FAQPage, Article)
- [ ] Performance budget: LCP < 2.5s on 4G (hero video poster strategy, lazy
      loading below fold, font subsetting)

## Phase 6 — Launch readiness

- [ ] Accessibility audit (WCAG 2.1 AA: keyboard nav, screen reader pass on
      interactive bits — tabs, egg, players, FAQ; contrast re-check after asset swap)
- [ ] Cross-browser/device QA (Safari iOS especially: video autoplay, clip-path,
      color-mix fallbacks)
- [ ] Copy guardrail audit of every page (built-with not clinically-proven, no
      chatbot framing, no collect-them-all, no urgency-shaming, no DFK trademark)
- [ ] Legal review: COPPA/ASTM claims, testimonial compliance (FTC), privacy policy
- [ ] Pre-order flow end-to-end test (payment, confirmation email, cancellation)
- [ ] 404 page (pixel pet, obviously), redirects, uptime monitoring
- [ ] Launch checklist dry run + go/no-go with team

---

## Already done (for the record)

- [x] Message architecture: missions, world, library, balance rules (SITEMAP.md)
- [x] v2 homepage sample: full pixel design system, device-led hero, motion,
      playable library, reviews, FAQ (`pages/index-v2.html`, PR #1)
- [x] units.gr reverse-engineering + migration decisions (DESIGN-V2.md)
- [x] Creative asset inventory incl. pre-pivot do-not-use flags (ASSET-INVENTORY.md)
- [x] Pixel asset brief for the graphic team (PIXEL-ASSET-BRIEF.md)
- [x] Strategic context for collaborators (PRODUCT.md)
