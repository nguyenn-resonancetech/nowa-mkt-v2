# Nowa Brand Mark

The logo system: what exists, how it's used, and the rules. Status: **v2 —
2026-07-04 designer drop adds the drawn wordmark SVGs, which are now the
primary web marks**; icon master vector and misuse sheet still owed by the
graphics team (flagged in §5).

---

## 1. The marks

| Asset | What it is | File |
|---|---|---|
| **Wordmark (coral)** | Drawn lowercase `nowa` wordmark, chunky rounded letterforms, Coral Flame `#EF493D` fill. THE web mark on light surfaces. | `pages/assets/brand/nowa-wordmark.svg` (426×96 vector) |
| **Wordmark (blush)** | Same drawn shape, pastel blush `#F3E1DB` fill (`--color-wordmark-blush`). THE mark on ink surfaces. | `pages/assets/brand/nowa-wordmark-pastel.svg` (426×96 vector) |
| **App icon** | Coral Flame rounded square, white lowercase `nowa` wordmark | `pages/assets/brand/logo-app.png` (2729²), `logo-app-64.png` (64²) |
| **Horizontal lockup** | App-icon-style coral square (white horizontal bar motif) + "Nowa" wordmark in deep ink | `pages/assets/brand/logo-full.png` (99×40 — low-res, needs master) — LEGACY, prefer the wordmark SVGs |
| **Live-text brand** | `logo-app` icon at 28×28 + "Nowa" set live in Onest 800, 22px — SUPERSEDED in web nav by the coral wordmark (2026-07-04); still valid where the SVG can't ship (plain-text email, third-party profiles) | the old nav pattern (`COMPONENTS.md §5`) |
| **Footer logotype (typeset)** | Giant "Nowa**.**" — Onest 900, coral period — SUPERSEDED in page footers by the blush wordmark SVG; keep for typeset display lockups where the drawn mark is unavailable | `.foot-word` (text fallback) |

## 2. The rules

1. **The drawn wordmark is the web mark (decision 2026-07-04).** Nav header =
   coral wordmark on light (renders at 107×24 in nav, ~24px x-height min);
   footer = giant blush wordmark on ink (`clamp(240px,55vw,680px)` wide).
   One drawn shape, two fills — never restyle, stretch, or recolor beyond
   the two sanctioned fills.
2. **Coral wordmark counts as the view's coral.** It participates in the
   "one coral per view" rule — that's why the nav keeps the pre-order `.btn`
   as the only other coral element (CTA wins; the mark is small).
3. **The corner exception (decision 2026-07-02).** The app icon keeps its
   **rounded** corners — it is a platform artifact (iOS/Android icon grid,
   favicon) and follows platform convention. Everything else in the brand
   world uses stepped pixel corners. Do not create a stepped app icon. The
   favicon stays `logo-app-64.png`.
4. **Typeset wordmark rule (fallback contexts only).** Where the SVG can't
   ship, set "Nowa" in Onest 800–900, ink on light / parchment on ink, never
   Tiny5, never letterspaced apart. The coral period ("Nowa**.**") belongs to
   this typeset logotype; the drawn wordmark carries no period.
5. **The coral cell `.bcell`** (12px square, rotates 90° on hover, 300ms
   `--ease-expo`) remains the pixel-world brand cadence in eyebrows/chapters —
   keep that role separate from the logo.

## 3. Usage by surface

| Surface | Mark | Min size |
|---|---|---|
| Web nav | coral wordmark SVG (107×24 current) | height ≥20px |
| Footer | giant blush wordmark SVG on ink | — |
| Favicon / app icon | `logo-app-64` / platform exports from master | 16px (favicon) |
| Social avatar | app icon | platform min |
| Social posts / ads | coral wordmark (light bg) or blush wordmark (ink bg); app icon only as avatar/stamp | wordmark height ≥18px rendered |
| Email header | coral wordmark SVG (fallback: horizontal lockup) | width ≥96px |
| App UI | app icon only in About/splash; in-app brand is carried by tokens, not the logo | — |

**Clear space:** keep ≥ the wordmark's `o`-width on all sides (interim rule
until the master sheet defines exact metrics).

## 4. Backgrounds

- **On parchment / white / bright-paper:** coral wordmark. ✓
- **On ink / charcoal:** blush wordmark (never the coral one — too vibrating on ink).
- **On coral / ember:** neither fill works; use white typeset fallback (rule 4) until a white wordmark export exists (§5).
- **On sage / warm-sand:** coral wordmark works; check it isn't fighting a nearby coral CTA (rule 2).
- **On photos:** only over calm, dark, or blurred regions; blush wordmark + ink scrim treatment (as `.hero-tag` does) if contrast is marginal.

## 5. Owed by graphics (gaps)

- ~~On-dark lockup export~~ ✓ delivered 2026-07-04 (`nowa-wordmark-pastel.svg`).
- **White wordmark export** for coral/ember surfaces (rule 4 fallback today).
- Master **SVG** of the app icon + lockup (logo-full.png is 99×40 raster).
- Exact clear-space + minimum-size sheet, and a misuse page (stretched,
  recolored, stepped-corner icon, coral-on-coral, Tiny5 wordmark).
- Decision: does the white bar motif in `logo-full`'s icon stay, or does the
  lowercase `nowa` icon (app icon) become the only icon? Today two icon
  variants circulate.
