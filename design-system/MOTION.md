# Nowa Motion System

How Nowa moves. Extracted from `pages/index-permill-v2.html` (Permill v3) and
hardened with design-engineering practice (Emil Kowalski's animation framework,
impeccable's motion register). Tokens live in `tokens.css`; component-specific
CSS lives in `COMPONENTS.md`.

---

## The two laws

1. **Stepped is alive, smooth is chrome.**
   Pet-world and organic motion runs on `steps()` timing — chunky, 8-bit,
   deliberate: pixel press `steps(2)`, pet bob `steps(2)`, confetti `steps(5)`,
   `+1 FRIEND!` `steps(6)`, egg tease `steps(2)`, marching pixel lines.
   UI chrome (reveals, hovers, crossfades, carousels) runs on smooth expo-out
   curves (`--ease-expo`, `--ease-out-strong`).
   *This split is what makes the page feel coherent. Never give chrome a
   stepped wobble; never give the pet a silky tween.*

2. **The frequency test decides the budget.**
   How often will a user see this animation?
   | Seen | Budget |
   |---|---|
   | 100+×/day (app tab switch, toggle, keyboard action) | none. Ever. |
   | tens×/day (hovers, list nav) | minimal — ≤150ms, transform/opacity only |
   | occasional (modals, sheets, toasts) | standard bands below |
   | rare / first-run (hero, hatch, onboarding, celebration) | full delight |
   Landing pages live mostly in the bottom rows; app UI lives in the top rows.
   **Never animate keyboard-initiated actions.**

---

## Easing map

| Situation | Curve |
|---|---|
| enter / exit | `--ease-out-strong` (or `--ease-expo` for big entrances) |
| moving/morphing on screen | ease-in-out (add token if needed) |
| hover / color | `ease` or `--ease-out-strong` |
| constant motion (marquee, progress, march) | `linear` |
| pixel press / pet life | `steps(n)` |

Never `ease-in` on UI (feels sluggish exactly when the user is watching).
**No bounce, no elastic curves** — Nowa expresses "life" through `steps()`,
not spring overshoot.

## Duration bands

| Moment | Duration | Token |
|---|---|---|
| pixel press | 70ms `steps(2)` | `--duration-press` |
| Tier-2 clickable-card hover | 110ms | `--duration-hover-2` |
| Tier-4 static lift, color hovers | 150ms | `--duration-fast` |
| content crossfade out-phase (tab swap, label swap) | 220ms | `--duration-swap` |
| UI state (accordion, sheet) | 300ms | `--duration-base` |
| **UI ceiling** | **300ms** | — |
| section reveal (LP only) | 700ms | `--duration-reveal` |
| hero line reveal (LP only) | 900ms | `--duration-reveal-lg` |

**Exits run ~75% of their entrance.** Asymmetry rule: slow where the user is
deciding (hold-to-confirm), fast where the system responds (release, dismiss).

---

## Signature moves (the proprietary vocabulary)

- **Pixel press** — extruded side-face (`--side`) grows +3px on hover, collapses
  to 2px + `translateY` on `:active`, 70ms `steps(2)`. The "old console button."
- **Hover→commit grammar** — hover invites (lift + 4px coral ring traced around
  the stepped silhouette), click commits (coral-mist fill, settled -3px lift,
  ring off). Full spec + specificity traps: COMPONENTS.md §2b.
- **Marching pixels** — dashed repeating-gradient + `background-position` loop,
  700ms linear (`.lb-line`, `.gameloop .loop-rail`).
- **Scroll-reactive drift** — marquees driven by scroll velocity with friction:
  `v += dy*0.4; v *= 0.92; x += v*0.18 + idle`, direction-aware sprite flip
  (`walk-rev`). Species strip + review rows. Never freezes (idle drift term).
- **Word-stagger brighten** — quote words at opacity .18 → 1, 80ms/word, on
  50% visibility.
- **Hero choreography** — h1 lines masked (`translateY(110%)`→0, 900ms expo,
  70ms stagger), then lead/CTA/shipline fade-rise at 220/300/380ms. Gated by a
  `loaded` class with a **600ms safety timeout** — never let slow assets hold
  the hero hostage.
- **Stepped delight** — confetti/plusone/hatch on the egg; reserve for earned,
  rare moments (a hatch, a completed mission), never routine UI.

## Scroll reveals (LP register)

- IntersectionObserver, `rootMargin: 0 0 -80px 0`, threshold .05,
  **unobserve after firing**.
- `.js`-gated: no-JS (and headless/SEO) users see everything. Reveals enhance
  a visible default — never gate content on a class-triggered transition.
- Group children stagger 60ms; cap total stagger ≈ 500ms.
- Use **transitions, not keyframes** — interruptible, retargetable.
- **Budget rule (decision 2026-07-02):** uniform fade-on-scroll on every
  section is generic. Spend entrances on 3–4 earned moments per page
  (hero, spine words, gameloop ring, $99 tally); demote the rest to instant
  or opacity-only. *(Applies to new pages; retrofitting permill-v2 is a
  separate pass.)*

## App-UI register (for APP-UI.md work)

- Frequency test first — most app chrome gets **no** motion.
- Popovers/menus scale from their **trigger** (`transform-origin`), start at
  `scale(.96)` + opacity, never `scale(0)`. Modals stay center-origin.
- Tooltips: delay the first, open adjacent ones instantly (no animation).
- Toasts/sheets: transitions (interruptible), enter ease-out, exit 75%.
- Height changes: `grid-template-rows 0fr→1fr` (COMPONENTS.md §21), never
  `height`.
- Perceived performance: <80ms feels instant; optimistic UI for low-stakes
  actions (mission toggle), never for payment/deletion; skeletons fade out.

## Performance rules

- Hot paths animate **transform + opacity only**. Blur/clip-path/shadow are
  allowed as *bounded* premium materials (small areas, verified smooth).
- Don't drive per-child CSS variables during drag — set `transform` on the
  element (variable writes recalc every child).
- Predetermined motion = CSS/WAAPI (off main thread); dynamic/interruptible
  = JS. JS rAF animation drops frames under load.
- `will-change` only while animating, never page-wide.
- Hover effects gated: `@media (hover:hover) and (pointer:fine)`.
- Reveal-vs-hover specificity: snappy hover transitions must outrank the
  600–700ms `.reveal` entrance transition and keep an `opacity` entry
  (COMPONENTS.md §2b maintainer notes).

## Reduced motion — two tiers, not a nuke

Reduced motion means *fewer and gentler*, not zero:
- **Remove:** movement (translate/scale), marquees, drift, parallax, smooth
  scroll (Lenis off), autoplaying ambient video, stagger delays.
- **Keep:** opacity/color crossfades that aid comprehension (near-instant is
  fine), state changes, focus indicators.
Each component ships its reduced state (annc → static single item; mission
swap → instant text swap; egg → instant hatch).

## Dependencies

- **Lenis** smooth scroll (`lerp: 0.17, wheelMultiplier: 1.1`) is part of the
  LP register only. Skipped entirely under reduced motion. Never in app UI.
- Anchor clicks route through Lenis (`duration: 0.65, offset: -20`).

## Future signature (sanctioned direction)

Stepped **clip-path motion**: dither-style wipes, stepped-corner reveals,
hold-to-confirm fills that sweep a stepped silhouette. Makes the motion
language as proprietary as the corners. Prototype before adopting; keep it
bounded (perf) and rare (budget).
