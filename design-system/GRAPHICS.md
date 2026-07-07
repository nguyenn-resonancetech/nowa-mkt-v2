# Nowa Graphics & Illustration

Rules for the pixel-art world, photography, and illustration. Status: **v2 —
2026-07-04 designer drop lands the icon direction (§5, now decided)**; the
pixel-art palette audit (§2) remains open.

**Asset library today** (`pages/assets/`):
- `species/` — 12 pet sprites (200×200 source, RGBA): 7 base species + 5
  evolved forms (`-1`/`-2` suffix = form, e.g. `miko-1` = Scholar).
- `pixels/` — HUD/motif art. Two generations: legacy snake_case GIFs at 80px
  (`*_anim_80px.gif`, `_x2`/`_x3` stills) and the 2026-07 kebab-case set at
  80/96px (`pet-loved-80.gif`, `pixel-pet-96.gif`, `watering-can-96.gif`,
  `pet-evolution-{80,96}.gif`, `kid-star-{80,96}.gif`, `pet-reading-80.gif`)
  plus full-color library icons (`lib-story/song/podcast/soundfx.png`).
  New art follows the kebab-case `{subject}-{action}-{size}` naming.
- `scenes/` — pixel scenes (288×288 sketches; `scene-care-loop` at 2048²;
  `scene-care-permill.png` = current pull-quote art).
- `brand/` — logo system incl. the drawn wordmark SVGs (see BRAND-MARK.md).
- `avatars/` — advisor photos. `device/` — hardware renders. `showcase/` —
  offer illustrations (`whatyouget-1.png` = deal expand). `compare/` — pixel
  category icons (`cmp-*-permill.png` = 2026-07 full-color variants).

---

## 1. Pixel art — rendering laws

- **Always crisp:** `image-rendering: pixelated` (the `.px` utility). Photos
  and hardware renders stay `auto`. Never mix per-element.
- **Integer scale only.** A sprite renders at 1×, 2×, 3×… of its source
  pixel grid, never fractional (fractional = shimmering half-pixels). The
  `_x2`/`_x3` filename suffix marks pre-scaled exports; `clamp()` sizing on
  sprites (as the species strip does) is acceptable only because the source
  is high-res relative to display size — new HUD art should snap.
- **Naming convention:** `{subject}_{action}_{size|scale}.{png|gif}` —
  keep it (`miko_evolution_loop_80px.gif`, `egg_hatch_x2.png`).
- Animated pixel art = GIF loops at chunky frame rates (matches the
  `steps()` motion law); no smooth-tweened sprite motion.

## 2. Pixel palette (OPEN — owed by graphics)

Sprites currently carry their own palettes and do **not** all sample from
`design/tokens.css`. Needed: a pixel-art palette sheet — which token colors sprites
may use, plus the sanctioned skin/species ramps outside the UI palette.
Until then: new HUD/motif art (hearts, sparks, meters, eggs) uses token
colors only (coral family, amber, leaf, ink, parchment); species art is the
artists' domain.

## 3. Scenes & composition

The house scene formula (see `scene-care-loop`, mission-art wells):
**parchment ground + faint graph grid + one centered subject + sparse
`+`-sparkles.** Scenes sit inside `.mission-art` / `.blueprint` wells or
pxcard media slots — never full-bleed behind body text. Negative space is
part of the drawing; don't wallpaper.

## 4. Photography

- **Treatment:** stepped `--px-step-md` mask + `--px-shadow` + slight rotate
  (±2°) — the `.ph` / `.hard-photos` pattern. Advisor avatars: stepped mask,
  112px (72px mobile), `object-fit: cover`, `image-rendering: auto`.
- **Subjects:** real families, real mornings, warm light; kids 6–8 skew
  (BRAND-RULES). No stocky staged joy; the register is "calm, real, slightly
  imperfect."
- Photos never get pixel-art filters; the two worlds contrast on purpose
  (drawn pet world vs. real family world). That contrast IS the story.

## 5. Icons (DECIDED 2026-07-04 — pixel-line set)

Two languages coexist, both now pixel-flavored:
1. **Pixel art icons** — pet world: full-color sprites/GIFs (HUD, game loop,
   fun cards, `lib-*.png` / `cmp-*-permill.png` variants).
2. **Pixel-line icons** — utility/commerce: the Nucleo-based set from the
   2026-07 designer drop. Spec: 24px grid, `stroke-width: 2`,
   **`stroke-linecap="square"`** (the pixel tell — never round caps), no
   joins/curves where a right angle works, `fill:none`, colored via
   `currentColor`, inline SVG. Dotted/dashed detail is drawn as short 0.01
   paths (renders as square dots). Live examples: device-spec accordions,
   library chips, compare-table headers on the LP; specimen sheet =
   `design-system/designer-components.html`.
The old Feather-style round-cap icons are DEPRECATED — replace on touch.
On white, competitor/neutral icons may tint with `--color-tint-*`; coral
stays reserved for actions. Never mix the two languages in one component.

## 6. Infographics & data

- Template: ink or white pxcard + one drawn diagram + Tiny5 data tags +
  warm caption (`.day-rhythm` is the reference; COMPONENTS.md §15).
- Stats always render as the `.mstat` receipts block (big coral stat +
  finding + italic source). Never uncited numbers (BRAND-RULES).
- Charts (app Growth screens, blog): Onest labels, coral for THE data point,
  slate/chalk for context series, hard edges (no smoothed gradients), grid =
  graph-paper alpha lines. No 3D, no donut-for-decoration.

## 7. Placeholders & handoff

- `.pxslot` (dashed well + Tiny5 label + note) is the only sanctioned
  placeholder — it screams "not final" on purpose. Never ship it.
- `SAMPLE · PENDING APPROVAL` chips stay on any unapproved quote/asset until
  sign-off (amber `.sample-chip`).
- Graphics handoff into the repo: PNG/GIF into the `pages/assets/` folders
  above, following §1 naming; source files stay in the design drive, not
  the repo.
