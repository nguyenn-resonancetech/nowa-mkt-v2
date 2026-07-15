# Nowa Icons — pixel-line set (Nucleo)

The utility/commerce icon language (GRAPHICS.md §5). 108 most-used icons from
the Nucleo pixel set, synced 2026-07-15 from the designer drop
(`nucleo_pixel_svg_v1.2.1`) and mirrored in Figma (**Nowa Design System v2 →
page "Icon"**, components named `icon/<name>`).

**Call an icon by its name — the name IS the filename** (Nucleo's file name
minus the `24px_` prefix). Same names in code and Figma, so round-trip is 1:1.

## Where

| What | Path |
|---|---|
| Individual SVGs (currentColor) | `pages/assets/icons/<name>.svg` |
| Sprite (all 108 as `<symbol id="<name>">`) | `pages/assets/icons/icons.svg` |
| Figma masters | file `9x2Eryg0EbeixCwSZduiml`, page **Icon**, `icon/<name>` |

## How to use

**Sprite reference (preferred on pages — one request, cache-friendly):**
```html
<svg class="pl-icon" width="24" height="24" aria-hidden="true">
  <use href="assets/icons/icons.svg#magnifier"></use>
</svg>
```

**Inline (when you need to style sub-paths or avoid the extra fetch):** paste
the file's `<svg>` content directly; it inherits `currentColor` from CSS.

```css
/* color comes from the text color of the surface */
.pl-icon { color: var(--color-slate-mid); }
.dark .pl-icon { color: var(--color-cloud-border); }
.cmp-them .pl-icon { color: var(--color-tint-coral); } /* or tint-amber / tint-sky */
```

Rules (unchanged from GRAPHICS.md §5):
- 24px grid, `stroke-width: 2`, **square caps** — never round.
- Scale proportionally only (24 → 18/20/36/48); stroke scales with it.
- Coral = actions only. Competitor/neutral tints on white = `--color-tint-*`.
- Pixel ART = pet world; pixel LINE = utility. Never both in one component.
- `<img src>` does NOT inherit currentColor — use sprite `<use>` or inline SVG
  (old `assets/pixels/*.svg` `<img>`+invert-filter usage is the legacy pattern).

## The 108 names

**UI & navigation:** house · magnifier · gear · menu · dots · sliders · toggle ·
check · xmark · plus · minus · arrow-up · arrow-down · arrow-left · arrow-right ·
chevron-up · chevron-down · chevron-left · chevron-right · expand · external-link ·
circle-info · circle-question · triangle-warning · ban

**People & communication:** user · users-2 · circle-user · heart-2 · star · bell ·
envelope · message · paper-plane-2 · phone · face-smile · thumbs-up

**Time:** calendar · clock · watch · hourglass · stopwatch

**Media & sound:** camera · photo · image · film · media-play · media-pause ·
music-note · volume · microphone · headphones-2

**Files & editing:** download · export · share-up-right · link · copy · clipboard ·
trash · pencil · pen · eraser · brush · folder · file · filter · sort-arrows ·
grid-layout · list-todo · print

**Security & account:** lock · lock-open · key · shield · eye · eye-slash ·
circle-logout

**Commerce:** cart-shopping · credit-card · wallet · money · percentage · receipt ·
tag · gift · truck · bag · calculator · chart · chart-line · repeat · rotate

**Places & things:** globe · map-pin · compass · bookmark · monitor · laptop ·
wifi · battery · code · square-terminal · rocket · lightbulb · book ·
graduation-cap · moon · door

Nucleo aliases to know: `magnifier` = search · `xmark` = close · `heart-2` = heart ·
`media-play/pause` = play/pause · `paper-plane-2` = send · `export` = upload ·
`cart-shopping` = cart · `circle-logout` = sign-out.

## Adding / regenerating

1. Pick the icon in the licensed Nucleo download (`nucleo_pixel_svg_v1.2.1/outline/…/24px_<name>.svg`).
2. Copy to `pages/assets/icons/<name>.svg`, replacing `stroke="#000|black"` and
   `fill="#000|black"` with `currentColor`.
3. Append a `<symbol id="<name>" viewBox="0 0 24 24">…</symbol>` with the same
   inner content to `icons.svg`.
4. Add the matching `icon/<name>` component to the Figma **Icon** page (import
   SVG, bind strokes/fills to `color-deep-ink`).
5. Add the name to the list above.

License: Nucleo is a paid licensed set (see `nucleo-copyright-notice.html` in
the download). Ship only in Nowa properties; don't redistribute the raw set.
