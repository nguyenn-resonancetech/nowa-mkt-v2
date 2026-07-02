# Nowa Graphics & Illustration

Rules for the pixel-art world, photography, and illustration. Status: **v1 —
codifies current asset practice**; the pixel-art palette audit (§2) and the
final pixel-icon direction (§5) are open items owed by the graphics team.

**Asset library today** (`pages/assets/`):
- `species/` — 12 pet sprites (200×200 source, RGBA): 7 base species + 5
  evolved forms (`-1`/`-2` suffix = form, e.g. `miko-1` = Scholar).
- `pixels/` — HUD/motif art: animated GIFs at 80px (`*_anim_80px.gif`),
  multi-scale stills suffixed `_x2`/`_x3`, exact-size pieces (`58x42`).
- `scenes/` — pixel scenes (288×288 sketches; `scene-care-loop` at 2048²).
- `avatars/` — advisor photos. `device/` — hardware renders. `showcase/` —
  offer illustrations. `compare/` — pixel category icons.

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
`tokens.css`. Needed: a pixel-art palette sheet — which token colors sprites
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

## 5. Icons (INTERIM — direction pending Daniel)

Two languages coexist (rule from COMPONENTS.md):
1. **Pixel icons** — pet world (`.licon` wells, HUD, sprites).
2. **Stroke icons** — utility/commerce: Feather-style, `stroke-width`
   1.8–2.6, round caps/joins, `currentColor`, 16–24px grid, inline SVG.
Never both in one component/canvas. The final pixel-icon style (and whether
a custom stroke set replaces Feather) is an open decision — don't invest in
new icon families until it lands.

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
