# Nowa Design System — Reference

The visual language of the Nowa marketing site, extracted so it can be reused on
**app UI** and any follow-up graphic work. The mood: **storybook warmth meets
pixel playfulness** — warm paper canvas, deep-ink night chapters, and a retro
pixel/8-bit motif (graph paper, stepped corners, Tiny5 type) reserved for the
pet world.

- **Tokens:** [`tokens.css`](tokens.css) (authoring) · [`tokens.json`](tokens.json) (tooling)
- **Components:** [`COMPONENTS.md`](COMPONENTS.md)
- **Rules (read before designing):** [`BRAND-RULES.md`](BRAND-RULES.md)
- **Live library:** [`gallery.html`](gallery.html)
- **Source pages:** `pages/index-v2.html`, `pages/index-permill.html`
- **Locked variant:** canvas = **Sunlit cream `#fdf5dd`** (paper3), hero = **Stage** (option 1)

---

## 1. Color

### Brand & action
| Token | Hex | Use |
|---|---|---|
| `--color-coral-flame` | `#ef493d` | **The only action color.** CTAs, active states, key accents, chapter cells. |
| `--color-coral-glow` | `#f87a71` | Coral on dark surfaces; hover-lift fills. |
| `--color-coral-blush` | `#fececa` | Soft coral — pixel offset shadow on hero stage, egg spot. |
| `--color-ember-deep` | `#b9271c` | Button side/shadow face (the 3D pixel button). |
| `--color-ember-darker` | `#7f241d` | Brand dark accent surface. |

### Ink & text
| Token | Hex | Use |
|---|---|---|
| `--color-deep-ink` | `#161c24` | Primary text; dark "night" canvas. |
| `--color-ink-charcoal` | `#212b36` | Dark card faces, device frames. |
| `--color-slate-mid` | `#454f5b` | Secondary text / lead paragraphs. |
| `--color-mist-body` | `#637381` | Tertiary / fine print. |
| `--color-cloud-border` | `#c4cdd5` | Borders & muted text on dark. |

### Surfaces
| Token | Hex | Use |
|---|---|---|
| `--color-warm-parchment` | `#fdf5dd` | **Canvas (Sunlit cream).** |
| `--color-chalk-surface` | `#dfe3e8` | Alt band, inactive meter cells. |
| `--color-ghost-white` | `#f4f6f8` | Blueprint / subtle fill. |
| `--color-pure-white` | `#ffffff` | Card faces, modals. |

### Signal
| Token | Hex | Use |
|---|---|---|
| `--color-amber-signal` | `#ffc107` | Pixel sparkle, "sample" chip, device button. |
| `--color-leaf-success` | `#54d62c` | Beta chip, success. |

> **Theme note.** The canvas is `paper3` / Sunlit cream `#fdf5dd`. The `paper`
> family only re-tints the canvas + hero background; ink and coral are unchanged.
> The `mint` and `sky` "cartridges" re-ink the *entire* palette (different ink
> hues) — they are **not** the chosen direction and are excluded here.

---

## 2. Typography

Three families, each with a strict job:

| Family | Token | Role |
|---|---|---|
| **Onest** | `--font-onest` | Display, all headings, UI labels, button text, nav. Weights 700–900 for display, 600–700 for labels. |
| **Noto Sans** | `--font-noto-sans` | Body copy, paragraphs, list text. |
| **Tiny5** (pixel) | `--font-pixel` | **Pet-world only** — pet sounds, level/care tags, chapter numbers, species names, "NOWA" stamps, durations. Never body or general UI. |

> `Departure Mono` is loaded by the source pages but **unused**. Don't adopt it
> as body/UI; reserve only for terminal/HUD textures if ever needed.

### Scale
`12 · 14 · 16 (body) · 18 · 20 · 24 · 30 · 36 · 48 · 64`px — tokens
`--text-caption` … `--text-display`.

**Display headings** override line-height to `1.08` and letter-spacing `-0.025em`
(`--leading-display-tight`, `--tracking-display`), with `text-wrap: balance`.
Body uses `line-height: 1.6` and `text-wrap: pretty`. Leads cap at `60ch`.

Fluid display sizing in source: `clamp(38px, 6.2vw, 84px)` for hero H1.

---

## 3. Spacing & layout

4px base scale: `4 · 8 · 12 · 16 · 24 · 32 · 40 · 48 · 64 · 96`.
(`--spacing-40` was missing from the original tokens and is now included.)

| Token | Value |
|---|---|
| `--page-max-width` | 1152px |
| `--page-max-width-content` | 896px |
| `--page-max-width-narrow` | 768px |
| `--card-padding` | 24px |
| `--element-gap` | 16px |

Sections use fluid vertical rhythm: `padding: clamp(72px, 9vw, 128px) 0`.
Content centers in `.wrap` (max-width + 24px side padding).

---

## 4. Shape — two corner systems

This system deliberately runs **two** corner languages:

1. **Soft radii** — for photographs, inputs, nav, soft pills. Scale `4 → 9999px`
   via `--radius-*`. Buttons on the *web* marketing pages are full pills
   (`--radius-buttons`).
2. **Pixel stepped corners** — the signature. Drawn surfaces (cards, buttons in
   the pixel treatment, avatars, chips, icons) use a `clip-path` notched polygon
   instead of a radius, paired with a **hard offset drop shadow**
   (`--px-shadow`, `3px 3px 0`). Two notch sizes: `--px-step-sm` (8px) and
   `--px-step-md` (12px). See `COMPONENTS.md → Pixel card (.pxcard)`.

> For **app UI**, prefer the pixel stepped-corner treatment for primary surfaces
> (it's the brand signature) and reserve soft radii for photos and text inputs.

---

## 5. The pixel system (signature)

- **Graph paper** — the page background and `.graph` / `.graph-dark` utilities draw
  a 1px grid at `--grid-cell` (28px). Light uses `--grid-line`, ink uses
  `--grid-line-dark`. Background is offset `0 16px` to align with the header.
- **Stepped corners** — notched `clip-path` polygons (see Shape).
- **Hard offset shadows** — `3px 3px 0` instead of soft blur. On the hero stage,
  a bold `14px 14px 0` coral-blush offset.
- **Dither transitions** — `.dither` checkerboard strips bridge light↔dark bands.
- **Pixel sparkles** — `+`-shaped amber/coral twinkles.
- **Tiny5 accents** — care meters, level chips, pet sounds, chapter numbers.

---

## 6. Surfaces & the band system

Sections alternate **warm parchment (day)** and **deep ink (night)** — the
"storybook chapter" rhythm. Dark sections use `.dark` and read a set of band
tokens that can be re-inked per section:

| Band token | Default | Meaning |
|---|---|---|
| `--band` | `--surface-deep-ink` | section background |
| `--band-ink` | `--color-pure-white` | heading/foreground |
| `--band-muted` | `--color-chalk-surface` | body on dark |
| `--band-accent` | `--color-coral-glow` | accent on dark |
| `--band-note` | `--color-cloud-border` | fine print on dark |

The pre-order band is a calm warm-sand `#fff3d6` (trust moment); the World
chapter and footer stay ink in every theme.

---

## 7. Motion

| Token | Curve / value | Use |
|---|---|---|
| `--ease-expo` | `cubic-bezier(0.19,1,0.22,1)` | content reveals, hero line entrance |
| `--ease-out-strong` | `cubic-bezier(0.23,1,0.32,1)` | UI transitions, hovers |
| `--ease-default` | `cubic-bezier(.4,0,.2,1)` | generic |
| `--duration-fast` | 150ms | color/hover |
| `--duration-base` | 300ms | UI state |
| `--duration-reveal` | 700ms | content entrance |
| `--duration-reveal-lg` | 900ms | hero line reveal |

Rules (from `docs/DESIGN-V2.md`):
- Entrances: expo-out, `translateY + opacity` — never `scale(0)`.
- **Pixel-press feel** uses `steps(2)` timing (chunky, not smooth) — buttons,
  tabs, players translate down on `:active`.
- Hover effects gated to `(hover:hover) and (pointer:fine)` only.
- Stagger 60–70ms inside groups; reveals are interruptible transitions.
- Full `prefers-reduced-motion` fallback: instant states, no movement.
