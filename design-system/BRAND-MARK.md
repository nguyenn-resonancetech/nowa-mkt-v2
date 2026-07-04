# Nowa Brand Mark

The logo system: what exists, how it's used, and the rules. Status: **v1 —
codifies current practice**; master vector files and misuse sheet still owed
by the graphics team (flagged in §5).

---

## 1. The marks

| Asset | What it is | File |
|---|---|---|
| **App icon** | Coral Flame rounded square, white lowercase `nowa` wordmark | `pages/assets/brand/logo-app.png` (2729²), `logo-app-64.png` (64²) |
| **Horizontal lockup** | App-icon-style coral square (white horizontal bar motif) + "Nowa" wordmark in deep ink | `pages/assets/brand/logo-full.png` (99×40 — low-res, needs master) |
| **Live-text brand** | `logo-app` icon at 28×28 + "Nowa" set live in Onest 800, 22px, tracking -.02em, + coral `.bcell` | the nav pattern (`COMPONENTS.md §5`) |
| **Footer logotype** | Giant "Nowa**.**" — Onest 900, `clamp(90px,17vw,250px)`, tracking -.04em, parchment on ink, **coral period** | `.foot-word` |

## 2. The rules

1. **The coral period is the brand's punctuation.** "Nowa**.**" — the period is
   always `--color-coral-flame`. Use in the footer logotype and display
   lockups; never mid-sentence.
2. **The corner exception (decision 2026-07-02).** The app icon keeps its
   **rounded** corners — it is a platform artifact (iOS/Android icon grid,
   favicon) and follows platform convention. Everything else in the brand
   world uses stepped pixel corners. Do not create a stepped app icon, and do
   not round any other brand surface to match the icon. In web nav, the icon
   renders at 28×28 with `border-radius: 7px` (¼ of rendered size — keep this
   ratio at other sizes).
3. **Wordmark is Onest 800–900, ink (or parchment on dark).** Never coral,
   never Tiny5, never letterspaced apart. The icon's *internal* wordmark is
   white lowercase and lives only inside the coral square.
4. **The coral cell `.bcell`** (12px square, rotates 90° on hover, 300ms
   `--ease-expo`) is part of the live-text brand — it is the pixel-world
   counterpart to the app icon. Use icon **or** cell, not both at once…
   *(current nav shows icon + text; the cell appears in eyebrows/chapters —
   keep those roles separate).*
5. **One coral mark per view.** The logo counts toward the "one coral per
   view fights with none" rule when sizing hero layouts.

## 3. Usage by surface

| Surface | Mark | Min size |
|---|---|---|
| Web nav | live-text brand (icon 28 + Onest 800 text) | icon ≥24px |
| Footer | giant logotype + coral period | — |
| Favicon / app icon | `logo-app-64` / platform exports from master | 16px (favicon) |
| Social avatar | app icon | platform min |
| Social posts / ads | horizontal lockup (light bg) or parchment-text variant (ink bg) | icon ≥24px rendered; wordmark x-height ≥10px |
| Email header | horizontal lockup | width ≥96px |
| App UI | app icon only in About/splash; in-app brand is carried by tokens, not the logo | — |

**Clear space:** keep ≥ the icon's own width ×0.5 on all sides of any lockup
(interim rule until the master sheet defines exact metrics).

## 4. Backgrounds

- **On parchment / white / bright-paper:** full-color (coral icon + ink text). ✓
- **On ink:** coral icon holds; wordmark flips to `--color-warm-parchment`.
- **On coral:** never place the coral icon on coral. Use white wordmark only.
- **On sage / warm-sand:** full-color works; check the icon isn't fighting a
  nearby coral CTA (rule 5).
- **On photos:** only over calm, dark, or blurred regions; add the ink scrim
  treatment (as `.hero-tag` does) if contrast is marginal.

## 5. Owed by graphics (gaps)

- Master **SVG** of icon + lockup (logo-full.png is 99×40 raster — unusable
  for print/scale).
- On-dark lockup export (parchment wordmark version) as a file.
- Exact clear-space + minimum-size sheet, and a misuse page (stretched,
  recolored, stepped-corner icon, coral-on-coral, Tiny5 wordmark).
- Decision: does the white bar motif in `logo-full`'s icon stay, or does the
  lowercase `nowa` icon (app icon) become the only icon? Today two icon
  variants circulate.
