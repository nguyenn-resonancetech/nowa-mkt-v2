# Figma Build Brief — Nowa Design System → Figma Library

**Purpose:** hand this to **Claude Desktop** (which has the *Claude in Figma* plugin
with `create_new_file` / `use_figma`) to build the Nowa DS as a real Figma library
with Variables + Components. This Claude Code session cannot run the write tools —
this brief is the ready-to-execute spec.

Canonical source of truth stays: `design/tokens.css` + `design-system/`.
Direction: **code → Figma**. Round-trip back (Figma → code) is done later with the
**Figma Dev Mode MCP** (`get_variable_defs` / `get_design_context`) + manual reconcile.

---

## 0. Setup (do once, in Claude Desktop)

1. Open **Claude Desktop** with the **Figma** connector authorized.
2. Open the **Figma desktop app**, create a new **Design** file: `Nowa DS`.
3. Ensure the *Claude in Figma* plugin (write / `use_figma`) is available.
4. Prompt: *"Load figma-use + figma-generate-library skills, then build the Nowa
   design system from `design-system/FIGMA-BUILD-BRIEF.md`."*

Build order (do not skip): **Variables → Base components → Composed components →
Sample assembly.** Bind every component property to a variable — never hardcode.

---

## 1. Variable collections

Create these Figma **variable collections**. Values are the canonical primitives
from `design/tokens.css`. Keep variable names matching the CSS custom-prop names
(minus `--`) so round-trip mapping is 1:1.

### Collection: `color` (mode: default)
| Variable | Hex |
|---|---|
| color-coral-flame | #ef493d |
| color-coral-glow | #f87a71 |
| color-coral-blush | #fececa |
| color-ember-deep | #b9271c |
| color-ember-darker | #7f241d |
| color-deep-ink | #161c24 |
| color-ink-charcoal | #212b36 |
| color-slate-mid | #454f5b |
| color-mist-body | #637381 |
| color-cloud-border | #c4cdd5 |
| color-chalk-surface | #dfe3e8 |
| color-warm-parchment | #fdf5dd |
| color-ghost-white | #f4f6f8 |
| color-pure-white | #ffffff |
| color-amber-signal | #ffc107 |
| color-leaf-success | #54d62c |
| color-sky-button | #6c9bd2 |
| color-sage-calm | #e2efdb |
| color-sage-border | #c9dec3 |
| color-sage-tint | #d3e7c9 |
| color-sage-ink | #1e3a2c |
| color-sage-muted | #4d6b58 |
| color-warm-sand | #fff3d6 |
| color-bright-paper | #faf8f0 |
| color-coral-mist | #fdecea |
| color-coral-mist-soft | #fff5f4 |
| color-pastel-coral | #f2a9a0 |
| color-pastel-amber | #f0cd83 |
| color-pastel-leaf | #9fd4a3 |
| color-pastel-sky | #a8cceb |
| color-tint-coral | #e59a90 |
| color-tint-amber | #dcb35b |
| color-tint-sky | #8fbfe0 |
| color-wordmark-blush | #f3e1db |

Semantic aliases (variables that point to the above): `surface-warm-parchment`→warm-parchment,
`surface-ghost-white`→ghost-white, `surface-chalk-surface`→chalk-surface,
`surface-pure-white`→pure-white, `surface-deep-ink`→deep-ink, `surface-ember-darker`→ember-darker,
`surface-sage-calm`→sage-calm, `surface-warm-sand`→warm-sand, `surface-bright-paper`→bright-paper.

### Collection: `type`
- Families: **Onest** (display/headings/UI labels), **Noto Sans** (body), **Tiny5** (pet-world ONLY).
- Sizes (px) / line-height: caption 12/1.333 · body-sm 14/1.429 · body 16/1.6 ·
  subheading 18/1.556 · heading-sm 20/1.4 · heading 24/1.333 · heading-lg 30/1.2 ·
  heading-xl 36/1.222 · display-alt 48/1.0 · display 64/1.25 (tight 1.08).
- Weights: 300/400/500/600/700/900. Display tracking −0.025em.
- Create Figma **text styles**: Display, H-XL, H-LG, H, H-SM, Subheading, Body,
  Body-SM, Caption, Pixel-HUD (Tiny5).

### Collection: `spacing` (number)
4, 8, 12, 16, 24, 32, 40, 48, 64, 96.

### Collection: `radius` (number) — soft, for PHOTOS/inputs/nav only
sm 4 · md 8 · lg 12 · xl 16 · 2xl 24 · 3xl 32 · cards 16 · cards-lg 24 · buttons 9999 · full 9999.

### Collection: `notch` (number) — stepped-corner scale (the signature)
dot 2 · 2xs 3 · xs 4 · sm6 6 · sm 8 · md 12. Rule: pick by element class —
chips/tags/buttons/tabs = sm 8 (even at 20–24px), cards/avatars/photos = md 12,
2xs/xs only for sub-20px micro elements. (⅛ of the short side is a sanity check
for large surfaces, not the selector — decided 2026-07-15.)

### Collection: `shadow` (effect styles — hard offset, ZERO blur)
| Style | X Y Blur Color |
|---|---|
| px-shadow-1 | 2 2 0 rgba(22,28,36,.10) |
| px-shadow | 3 3 0 rgba(22,28,36,.12) |
| px-shadow-dark | 3 3 0 rgba(0,0,0,.18) |
| px-shadow-3 | 4 4 0 rgba(22,28,36,.14) |
| px-shadow-dark-3 | 4 4 0 rgba(0,0,0,.28) |
| px-shadow-hover | 6 6 0 #fececa (coral-blush) |
| px-shadow-committed | 5 5 0 rgba(239,73,61,.32) |
| px-shadow-pop | 14 14 0 #fececa |

### Collection: `motion` (docs only — Figma has no easing var)
ease-expo cubic-bezier(.19,1,.22,1) · ease-out-strong cubic-bezier(.23,1,.32,1) ·
press 70ms steps(2) · hover-2 110ms · fast 150ms · base 300ms · reveal 700ms.

---

## 2. The signature shape — stepped corners in Figma

CSS uses `clip-path` polygon; Figma has no clip-path. Reproduce the notch with a
**vector/boolean shape** (or a component with the corner notches cut). Reference
polygons (from `gallery.html`):

- **step-8** (buttons/chips/icons, notch 8/4): 20-point polygon, outer step 8px, inner 4px.
- **step-12** (cards/avatars, notch 12/6): outer 12px, inner 6px.
- **step-12-in** (Tier-2 hover coral trace): inset variant at 4/10/16.

Build one **`Notch/8`** and **`Notch/12`** master vector; use as a mask/frame for
cards, buttons, chips. Pair every notched surface with a `shadow` effect style
(hard offset). **Never** use `border-radius` on a pixel surface.

`.pxcard` pattern = 1px border + fill drawn behind the notch. In Figma: a frame
with the notch shape, fill = `surface-pure-white` (or per-variant `--pxbg`), a 1px
stroke = `color-chalk-surface` (or per-variant `--pxborder`), + `px-shadow` effect.

---

## 3. Components to build (order + spec)

Reuse the vocabulary in `design-system/COMPONENTS.md` (full CSS per component) and
verify visuals against `design-system/gallery.html`. Build as Figma components with
**variants** for states. Bind fills/strokes/text to the variables above.

**Base (build first):**
1. **Button** `.btn` — coral-flame face, ember-deep side (hard offset), notch-8, Onest bold.
   Variants: default / hover (`-3px`, press) / on. + **Button-ghost** `.btn-ghost` (text + arrow, underline on hover).
2. **Tab** `.mtab` — notch-8; variants default / on (ink fill).
3. **Chip** — `.lvlchip` (Tiny5), `.beta-chip` (leaf), `.sample-chip` (amber), `.tchip`. Notch-6/8.
4. **Section label** — eyebrow number + heading (two systems: pixel vs onest).
5. **pxcard** — the core surface. Variants: static (plain) / clickable (Tier-2 coral-line hover) /
   committed (`.on`/`[open]` coral-mist fill + committed shadow). Light + dark (`--pxbg` ink) modes.

**Pixel HUD (pet-world, Tiny5 + steps motion):**
6. Care **meter** (8-bit cells), **egg** / egg-card, **equalizer** `.eq`, sound **bubble**, **Mario-block** fact icon (6 color variants: coral/red/green/blue/purple/amber; white icon, bevel via inner light/dark, no outer border, no dots — per current `preorder.html`).

**Composed / app-UI:**
7. `.appbar`, `.tabbar` (coral dot), `.row` list row, `.faq` accordion (details), `.device-frame` / phone showcase, `.dither` divider, named **bands** (sage / warm-sand / bright-paper), toggle (native rounded, coral "on" — NOT stepped).

**Rules to enforce while building:**
- One coral per view; coral = action only.
- Tiny5 only on HUD/pet. Onest headings, Noto body.
- Hover tiers 1–5 (see `prompt.md` / COMPONENTS.md §2b): only clickable → strong hover.
- Hard offset shadows only. Pixel art = integer scale, crisp.

---

## 4. Sample assembly (verify)

Recreate one section of `pages/index-permill-v2.html` (e.g. the **facts band** with the
6-color Mario-block icons, or the **compare table**) from the components to prove the
library composes correctly. Screenshot → compare to the live page.

---

## 5. Round-trip back to code (later)

After editing in Figma:
- **Tokens changed** → export via **Tokens Studio** plugin (2-way GitHub sync) OR read
  with Dev Mode MCP `get_variable_defs`, then update `design/tokens.css` + `tokens.json`.
- **Component changed** → Dev Mode MCP `get_design_context` on the node → reconcile into
  `design-system/COMPONENTS.md` + `gallery.html` (translate to token-based CSS, keep
  stepped-corner + hard-shadow; do not paste generic output verbatim).
- Then commit to `design-system/` and re-sync the bundled skill copies.
