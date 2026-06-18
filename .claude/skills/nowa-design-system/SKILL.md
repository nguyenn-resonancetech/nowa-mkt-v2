---
name: nowa-design-system
description: >-
  Nowa's official design system — apply it to any Nowa visual or UI work so it
  carries the brand. Use this skill whenever you build, restyle, or review
  anything for Nowa: app UI screens, the parent-app feature showcase, landing
  pages, marketing sections, banners, social/ad creative, emails, slides, icons,
  or any component (buttons, cards, navs, lists, modals, forms, badges). Use it
  ESPECIALLY when converting existing app UI screens or mockups to the new
  design system, or when someone says "make this on-brand / match Nowa / use our
  design system / our colors / our tokens." Trigger even if the user doesn't say
  "design system" — any Nowa-branded pixels are in scope. It supplies the tokens
  (colors, type, spacing, radius, motion), the component vocabulary, and the
  non-negotiable brand rules (coral-only CTA, Tiny5 pet-world-only, stepped
  pixel corners, hard offset shadows, Sunlit cream #fdf5dd canvas).
---

# Nowa Design System

Nowa is a $99 screen-free emotional-companion device for kids 6–9 (platform 3–10),
pre-ordering now, shipping Sept 2026. The visual language is **storybook warmth +
pixel playfulness**: a warm paper canvas, deep-ink "night" chapters, and a retro
8-bit pixel motif (graph paper, stepped corners, Tiny5 font) reserved for the pet
world. This skill makes new work look like it belongs.

## How to use this skill

1. **Always start from the tokens.** Link or inline `assets/tokens.css` and build
   with the CSS variables — never hardcode hex values that have a token. The
   canvas is **Sunlit cream `#fdf5dd`**.
2. **Reuse the component vocabulary** before inventing new components. The full
   catalog with real CSS is in `references/COMPONENTS.md`.
3. **Obey the brand rules** in `references/BRAND-RULES.md` — they're the difference
   between on-brand and off-brand. The most-violated ones are in the cheat sheet
   below.
4. **For app UI specifically:** carry over tokens + the pixel HUD elements
   (care meter, egg, equalizer, sound bubble, level chips — these are *already*
   pet-app UI), `.pxcard` surfaces, and `.btn`/`.mtab` actions. Build the screen
   chrome the marketing system lacks (tab bar, list rows, nav header, modals,
   forms, empty/loading/error states) **on these same tokens and the
   stepped-corner + hard-shadow language** — do not import a generic UI kit.
   **But brand the identity layer, go native on the control layer:** use the
   pixel/stepped treatment for cards, headers, CTAs, the pet HUD, and level chips;
   use familiar **native patterns** (rounded iOS-style switches, standard
   steppers/sliders) for small operating controls — keep coral as the "on" color
   so they still feel Nowa. Don't pixel-ify a 30px toggle. And keep big dark
   "night" surfaces sparing in-app (heavy on small screens) — prefer light/warm
   cards for settings; reserve full ink for real pet-world moments.
5. **Verify** against the live component library `assets/gallery.html` and, when
   the change is visible, render it in the browser preview.

> Full references (read when you need detail): `references/DESIGN.md` (complete
> token + system reference), `references/COMPONENTS.md` (every component + CSS),
> `references/BRAND-RULES.md` (all guardrails + copy rules). The canonical,
> editable source lives in the repo at `design-system/`; if tokens change there,
> re-sync this skill's bundled copies.

## Brand rules cheat sheet (the ones people break)

These are non-negotiable. Why they matter is in `references/BRAND-RULES.md`.

- **Coral Flame `#ef493d` is the ONLY action color.** CTAs, active/selected
  states, key accents. Never decorative, never a large fill. One coral per view.
- **Tiny5 (pixel font) is pet-world ONLY** — pet sounds, care meters, level/XP
  tags, numbers, species names. Never body copy or general UI chrome. Onest does
  headings/labels; Noto Sans does body.
- **Two corner systems, on purpose:** stepped pixel corners (notched `clip-path`)
  for drawn surfaces — cards, buttons, avatars, chips; soft radii only for photos
  and text inputs. Don't round a pixel card; don't step a photo inconsistently.
- **Hard offset shadows, not soft blur:** `3px 3px 0` (or `14px 14px 0`
  coral-blush on the hero stage). No Material-style elevation.
- **Storybook rhythm:** alternate warm-parchment "day" and deep-ink "night"
  sections; don't stack three of the same.
- **Motion:** expo-out entrances (`translateY + opacity`, never `scale(0)`);
  pixel presses use chunky `steps(2)`; hover only on fine pointers; always a
  `prefers-reduced-motion` instant fallback.
- **Pixel art renders crisp** (`image-rendering: pixelated`); photos render normal.

## Token quick reference

Full set in `assets/tokens.css`. The load-bearing ones:

| Token | Value | Use |
|---|---|---|
| `--color-coral-flame` | `#ef493d` | the only action color |
| `--color-coral-glow` | `#f87a71` | coral on dark / hover |
| `--color-coral-blush` | `#fececa` | pixel offset shadow |
| `--color-ember-deep` | `#b9271c` | button side face |
| `--color-deep-ink` | `#161c24` | text / night canvas |
| `--color-slate-mid` | `#454f5b` | secondary text |
| `--color-warm-parchment` | `#fdf5dd` | CANVAS (Sunlit cream) |
| `--color-pure-white` | `#ffffff` | card faces |
| `--color-amber-signal` | `#ffc107` | signal / sample chip |
| `--color-leaf-success` | `#54d62c` | success / beta chip |
| `--font-onest` | Onest | display, headings, UI labels |
| `--font-noto-sans` | Noto Sans | body |
| `--font-pixel` | Tiny5 | pet-world only |
| `--grid-cell` / `--grid-line` | 28px / `rgba(22,28,36,.08)` | graph paper |
| `--px-shadow` | `3px 3px 0 rgba(22,28,36,.12)` | pixel drop shadow |
| `--ease-expo` | `cubic-bezier(0.19,1,0.22,1)` | reveals |
| `--ease-out-strong` | `cubic-bezier(0.23,1,0.32,1)` | UI transitions |

## The signature shape (stepped corners)

Drawn surfaces use a notched `clip-path` polygon instead of `border-radius`, paired
with a hard offset shadow. Two notch sizes — small (8px) for buttons/chips/icons,
medium (12px) for cards/avatars. The exact polygons and the `.pxcard` pattern that
draws a 1px border + fill behind them are in `references/COMPONENTS.md §0–§2`.

## Component → app-UI map

When taking the system to app screens, reach for these first:

| Need | Use |
|---|---|
| primary / secondary action | `.btn` / `.btn-ghost` |
| tab bar, segmented control | `.mtab` (active = ink) |
| top app bar | `nav` (blur + rotating coral cell) |
| list row, content card, sheet | `.pxcard` |
| level / XP badge, status pill | `.lvlchip` / `.beta-chip` |
| pet care/health/XP bar | `.meter` (8-bit cells) |
| hatch / unlock flow | `.egg` / `.egg-card` |
| pet-sound feedback | `.eq` + `.bubble` |
| in-showcase screen mockup | `.device-frame` |
| settings accordion / expandable row | `.faq` (`<details>`) |
| section divider / background | `.dither` / `.graph` |

## Copy guardrails (when the work includes words)

- "built with" / "shaped by" advisors — **never** "clinically proven."
- Magical pet, not a chatbot toy; the pet doesn't speak human language.
- No surveillance / behavior-control / obedience framing.
- Don't use "empathy-based dependency"; don't lift "deeply feeling kid" verbatim.
- Full list in `references/BRAND-RULES.md`.
