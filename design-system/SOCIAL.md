# Nowa Social & Ad Design

How the design system leaves the website: social posts, paid ads, thumbnails,
covers. Words are governed by the `nowa-content-writing` skill (segment
routing, cold-register ad language, the anti-chatbot line family, the de-AI
lint) — this doc governs the **pixels**. Status: **v1 — rules are derived
from the system, not yet battle-tested in a real campaign; validate on the
first ad batch and amend.**

---

## 1. Canvases

| Format | Ratio / px | Use |
|---|---|---|
| Square | 1:1 · 1080×1080 | IG/FB feed, carousel cards |
| Portrait | 4:5 · 1080×1350 | IG/FB feed (preferred — more real estate) |
| Story/Reel | 9:16 · 1080×1920 | Stories, Reels, TikTok |
| Landscape | 16:9 · 1200×675 | X/Twitter, link cards, YouTube thumb |
| Cover | per platform | FB/YT banners |

**Safe areas:** keep all text + logo inside the center ~80% (9:16: respect
~250px top / ~310px bottom for platform UI). Nothing essential in corners.

## 2. The recipe (default composition)

One post = **one band + one subject + one line (+ one chip)**.

1. **Pick a band as the canvas** — the same named bands as the site:
   - *Sunlit cream day* — default; product, routines, warmth
   - *Deep ink night* — pet-world, species reveals, "doesn't talk" lines
   - *Sage calm* — safety/guarantee/trust messages
   - *Warm sand* — offer/pre-order messages
   Cream/bright canvases carry the **graph-paper grid** at low contrast
   (scale `--grid-cell` proportionally: ~2.6% of canvas width ≈ 28px@1080).
2. **One subject** — a sprite, the device, or one photo. Sprites render
   crisp (`image-rendering: pixelated`, integer scale multiples only —
   see GRAPHICS.md). One decisive subject beats a collage.
3. **One line** — Onest 800–900, tracking -.02 to -.025em,
   `text-wrap: balance` equivalent (manual break). The "Less X. More Y."
   lockup is the house hero shape.
4. **Optionally one chip** — a Tiny5 tag (`LVL 3`, `CARED FOR ♥`) or a
   stepped tag chip ("PRE-ORDER $99"). One, not three.

**Dither strip** (12px checks, scaled) is the sanctioned way to split a
canvas into two bands (e.g. day top / ink bottom on a 4:5).

## 3. Type floors (small-screen legibility)

- Headline: Onest 800–900, ≥ 64px @1080 (≈6% of width). 1–2 lines max.
- Support line: Onest 600 / Noto Sans, ≥ 36px @1080. One line.
- **Tiny5: display-accent only, ≥ 28px @1080, never the message itself.**
  At thumbnail scale pixel fonts die first — if the post must work as a
  ~200px thumb, the headline alone has to carry it.
- No body copy on the image. The caption is the body (content skill owns it).
- All-caps only for chips/tags ≤4 words.

## 4. Color & CTA rules (unchanged from the system, restated for ads)

- **Coral = the action.** One coral element per canvas: the CTA chip/button
  *or* the key word, never both. Coral is never a background wash.
- Text on cream: deep-ink headlines, slate-mid support. On ink: parchment/
  white + coral-glow accents. On sage: sage-ink/sage-muted only. On sand:
  deep ink. (Same contrast floors as the site: ≥4.5:1 body, ≥3:1 display.)
- CTA in ads renders as the **stepped stamp** (`.show-card-stamp`
  construction: white-on-coral, 4px notch, uppercase Onest 900) or the
  extruded button face for larger placements. Verb + object ("Reserve yours",
  "Hear it purr") — never "Learn more" if we can help it.
- **No urgency theater.** No countdowns, no "selling fast" (content-skill
  hard rule). The honest-scarcity register ("500 reservations, that's it")
  is the only scarcity allowed.

## 5. Logo on social

Per `BRAND-MARK.md`: horizontal lockup on light bands, parchment-wordmark
variant on ink; app icon alone only as avatar/profile. Bottom-left or
bottom-right inside safe area; icon ≥40px @1080; clear space = ½ icon width.
On the ink band the "Nowa**.**" logotype with coral period may serve as the
sign-off instead of the lockup.

## 6. Format notes

- **Carousel** — treat each card as one `.pxcard` idea; the swipe is the
  scroll. Card 1 = hook (hero line), middle = one point each (a mission, a
  stat callout, a species), last = offer + CTA stamp. Reuse the site's
  section rhythm: alternate day/ink cards, bridge with a dither edge.
- **Story/Reel end-card** — warm-sand band, `.po-tally` composition
  (struck value → big coral price → save badge) adapts 1:1.
- **Stat posts** — the `.mstat` block (big coral stat, plain-language
  finding, italic source) is the receipts pattern; always keep the source
  line, even at 24px. Never a stat without its citation.
- **Species/pet posts** — ink band + crisp sprite + Tiny5 name tag
  (`MIKO · SCHOLAR`) + eq bars or sound bubble as dressing. This is the
  loudest brand-ownership format we have; use it.
- **Motion (video/reels)** — the site's motion laws apply: stepped/chunky
  for pet life, smooth expo-out for text/UI; marching-pixel lines as
  transitions; no bounce/elastic; captions burned in (sound-off default).

## 7. Don'ts

- No gradient text, no glassmorphism, no soft drop shadows — hard pixel
  offsets only.
- No rounding stepped elements to "soften" them for social.
- No coral background floods; no more than one coral element.
- No pixel-font paragraphs; no headline below the type floors.
- No "AI companion" lead, no chatbot framing, never "no AI" (content skill
  hard rules; the ad-grade anti-chatbot lines live in its swipe file).
- Don't mix pixel icons and stroke icons in one canvas (interim icon rule).
