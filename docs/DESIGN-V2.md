# Design v2 — units.gr system migrated to Nowa tokens

Sample implementation: `pages/index-v2.html` (compare against `pages/index.html`).
Strategic context: `PRODUCT.md`. Tokens unchanged: `design/tokens.css`.

## What we reverse-engineered from units.gr

| Element | units.gr | Nowa v2 adaptation |
|---|---|---|
| Stack | GSAP 3.13 + ScrollTrigger (1 pinned scrub intro), Lenis, Swiper, Aeonik Pro | Vanilla CSS + IntersectionObserver + rAF (ports to any framework; Huy can swap in GSAP/Lenis 1:1) |
| Canvas | rgb(244,233,225) warm cream | `--surface-warm-parchment #edeae2` (already ours) |
| Type | Aeonik Pro, chunky black display | Onest 800/900, deep ink (not pure black) |
| Color blocks | 6 saturated colors at equal weight | Ink/white/parchment blocks; coral reserved for action; amber/leaf/blush only as pixel-cell accents |
| Easing | `cubic-bezier(0.19,1,0.22,1)` (expo-out), 0.2–0.7s | Same curve as `--ease-expo`; UI under 300ms, reveals 600–900ms |
| Pixel-grid illustrations | Colored cells on graph paper | `.graph` / `.graph-dark` utilities + scattered `stage-cell`s; real species sprites as imagery |
| Numbered side rail | 01–04 colored blocks | Chapter rail (storybook chapters = our named brand system) |
| Marquee ribbon | Amenities ticker | Product-fact ticker (screen-free · no ads · built with scientists · $99 · Sept 2026) |
| Giant footer logotype on grid | "units." + scattered pixels | "Nowa." + pixel cells + species peeking |
| Scroll-jacked cinematic intro | ~6000px pinned scrub before content | **Deliberately dropped** — hero is instant; one 900ms line-reveal choreography only |

## Motion rules applied (emil-design-eng)

- Entrances: expo-out, translateY + opacity, never `scale(0)`.
- Buttons: `scale(.97)` on `:active`, 160ms; arrow nudges on hover (hover-capable devices only).
- Reveals are transitions (interruptible), JS-gated via `html.js` so no-JS renders everything.
- Stagger 60ms inside groups; marquee linear; species strip is rAF-lerped scroll drift (no scroll-jack).
- Rare-moment delight allowed: egg-hatch interaction (click), spine quote word-brighten (once).
- Full `prefers-reduced-motion` fallback: no movement, instant states.

## Interactive moments in the sample

1. **Hero**: 3-line clip reveal, floating Brim sprite on graph paper, "LVL 3 · CARED FOR" Tiny5 tag.
2. **Spine quote**: words brighten in sequence on entry.
3. **Talk demo**: pet-sound bubble rotates (Tiny5), equalizer bars — shows "speaks in sound, not words."
4. **Mission tabs**: 3 mission types crossfade copy + sprite; each names its real-world sync.
5. **Egg hatch**: tap to hatch a random species — the blind-egg mechanic made tangible.
6. **Species strip**: scroll-linked sideways drift through all 12 sprites.
7. **Chapter rail**: fixed left, lights up per chapter (hidden under 1280px).

## For the dev merge

- All copy is the approved message architecture (see SITEMAP.md homepage balance rules).
- Sprites live at `pages/assets/` (pulled from nowaplanet-lp `app/assets/images/`); reference the originals in the production repo.
- Advisor quotes are placeholders pending sign-off — do not ship.
- Tiny5 appears only in pet-world moments (chapter numbers, pet sounds, LVL tag, species names) per the design rule.
