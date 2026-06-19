# Nowa Components

Every component mined from `pages/index-permill.html` (the most complete source).
Each entry: what it is, the classes/anatomy, variants/states, and the load-bearing
CSS. The shared stepped-corner `clip-path` is abbreviated as `‹STEP n›` where `n`
is the notch size (8 or 12px) — the full polygon is in **§0**. Render them live in
[`gallery.html`](gallery.html).

> **App-UI guidance** is called out in each section where the web component needs
> adaptation for screens (nav bars, tab bars, lists, etc.).

---

## §0. The stepped-corner primitive (`clip-path`)

> **GOTCHA (read this — it recurs):** when a button/card draws its fill via a
> `::before` overlay (the pixel-border trick below) and lifts content with
> `.el > * { z-index: 1 }`, that selector only lifts *element* children. A **bare
> text node** label (e.g. `<button>Save</button>`) stays at z-index 0 and is
> hidden behind the `::before`. **Always wrap button label text in a `<span>`**:
> `<button><span>Save</span></button>`. Symptom: button shows its icon/arrow but
> the text is invisible.

The signature shape. A notched octagon-ish polygon. Two sizes used across the system:

**Small notch (8px)** — buttons, tabs, chips, 44px icons:
```
clip-path: polygon(0 8px,4px 8px,4px 4px,8px 4px,8px 0,calc(100% - 8px) 0,calc(100% - 8px) 4px,calc(100% - 4px) 4px,calc(100% - 4px) 8px,100% 8px,100% calc(100% - 8px),calc(100% - 4px) calc(100% - 8px),calc(100% - 4px) calc(100% - 4px),calc(100% - 8px) calc(100% - 4px),calc(100% - 8px) 100%,8px 100%,8px calc(100% - 4px),4px calc(100% - 4px),4px calc(100% - 8px),0 calc(100% - 8px));
```

**Medium notch (12px)** — cards, avatars, photos:
```
clip-path: polygon(0 12px,6px 12px,6px 6px,12px 6px,12px 0,calc(100% - 12px) 0,calc(100% - 12px) 6px,calc(100% - 6px) 6px,calc(100% - 6px) 12px,100% 12px,100% calc(100% - 12px),calc(100% - 6px) calc(100% - 12px),calc(100% - 6px) calc(100% - 6px),calc(100% - 12px) calc(100% - 6px),calc(100% - 12px) 100%,12px 100%,12px calc(100% - 6px),6px calc(100% - 6px),6px calc(100% - 12px),0 calc(100% - 12px));
```

---

## §1. Buttons

### Primary pixel button `.btn`
3D extruded pixel button: coral top face over an ember side, stepped corners,
chunky `steps(2)` press. The depth is a `--side` variable animated on hover/active.

- **States:** hover lifts (`translateY(-3px)`, taller side), active presses
  (`translateY(4px)`, shorter side). Hover gated to fine pointers.
- **Contains:** label (Onest 700) + optional `.arr` arrow that nudges on hover.
- **Variants:** `.btn` in nav is smaller (`padding:11px 22px; font-size:14px`).

```css
.btn{--side:6px;--btn-top:var(--color-coral-flame);--btn-side:var(--color-ember-deep);
  display:inline-flex;align-items:center;gap:10px;
  background:linear-gradient(var(--btn-top),var(--btn-top)) no-repeat 0 0/100% calc(100% - var(--side)),var(--btn-side);
  color:#fff;font-family:var(--font-onest);font-weight:700;font-size:var(--text-body);
  padding:16px 30px 22px;border:0;cursor:pointer;clip-path:‹STEP 8›;
  transition:transform 70ms steps(2)}
.btn:active{--side:2px;transform:translateY(4px)}
@media(hover:hover) and (pointer:fine){
  .btn:hover{--side:9px;transform:translateY(-3px)}
  .btn:hover .arr{transform:translateX(3px)}
}
```

### Ghost button `.btn-ghost`
Text + underline-on-hover. Onest 700, coral underline.
```css
.btn-ghost{display:inline-flex;align-items:center;gap:8px;font-family:var(--font-onest);
  font-weight:700;color:var(--color-deep-ink);padding:16px 6px;
  border-bottom:2px solid transparent;transition:border-color 200ms var(--ease-out-strong)}
.btn-ghost:hover{border-bottom-color:var(--color-coral-flame)}
```

> **App UI:** `.btn` is the primary CTA. For dense app screens, the same shape at
> the small notch works for toolbar/segmented actions (see `.mtab`).

---

## §2. Pixel card `.pxcard` (foundation surface)

The universal card: stepped corners + 1px border drawn as a layered background,
plus a hard offset shadow via `drop-shadow` on the host. Applied to steps, mission
panels, library cards, advisor cards, FAQ, compare columns, reviews.

- **Theming vars:** `--pxbg` (fill), `--pxborder` (border color).
- **Dark variant:** `.dark .pxcard` uses ink fill + translucent white border +
  darker shadow.
- **Hover & interaction:** governed by the tiered affordance system — **see §2b.**
  In short: a static `.pxcard` lifts only; a *clickable* `.pxcard`
  (`<a>`/`<button>`/`<details>`/`[role="button"]`) gets the coral-line lift; a
  *committed* card (`.on` / `[open]`) takes a coral fill. Never give a static
  `.pxcard` a "clickable" hover.

```css
.pxcard{border-radius:0!important;position:relative;background:transparent!important;border:0!important;
  --pxbg:var(--surface-pure-white);--pxborder:var(--color-chalk-surface)}
.pxcard::before{content:"";position:absolute;inset:0;
  background:linear-gradient(var(--pxbg),var(--pxbg)) 1px 1px/calc(100% - 2px) calc(100% - 2px) no-repeat,var(--pxborder);
  clip-path:‹STEP 12›;z-index:0}
.pxcard>*{position:relative;z-index:1}
/* offset shadow */
.step.pxcard,.lib.pxcard,.faq.pxcard,/* … */{filter:drop-shadow(var(--px-shadow))}
.dark .pxcard{ /* via overrides */ filter:drop-shadow(var(--px-shadow-dark))}
```
> Containers holding `.pxcard`s need `padding-right/bottom:10px` so the offset
> shadow isn't clipped.

---

## §2b. Hover & interaction system (the affordance law)

**The rule that lets this scale: _hover strength follows interactivity._** A
surface reacts to the pointer only in proportion to what it does. When everything
lifts and glows, nothing reads as clickable — so the page feels noisy and every
new component drifts. Wire interactivity with **real semantics** (`<a>`,
`<button>`, `<details>`, `[role="button"]`) and the correct tier applies
**automatically**; never bolt a "clickable" hover onto a static `<div>`.

### The five tiers

| Tier | What | Hover treatment | Lift | Speed |
|---|---|---|---|---|
| **1 — Primary controls** | `.btn`, `.pbtn`, `.mtab`, `.pf-arrow`, `.pf-dot` | extruded press — side-face grows, stays coral | `-3px` (btn) | `70ms steps(2)` |
| **2 — Clickable cards** | a `.pxcard` that is `<a>/<button>/<details>/[role="button"]` (today: `.faq`, `.egg-card`, `.papp-feat`) | **4px coral line traced all around** (incl. stepped corners) + coral-blush offset shadow | `-5px` | `110ms` |
| **3 — Links** | nav links, `.btn-ghost`, footer/trust links, `.rail` | coral color / coral underline (no lift) | — | `150–200ms` |
| **4 — Static cards** | a `.pxcard` that is a plain `<div>/<figure>` (`.step`, `.seg`, `.adv`, `.lib`, `.fun`, `.cmp .col`, `.revcard`, `.mpanel`, `.talk-demo`, `.pullq`, `.day-rhythm`) | **clear lift only — no coral line** | `-3px` | `150ms` |
| **5 — Pet delight** | `.sp` species sprites, `.foot-pets` | playful lift + scale (whimsy, *not* affordance) | `-7/-8px` + scale | reveal-default |

### Committed state — hover invites, the click commits
When a Tier-2 card becomes **selected / active / open** (`.papp-feat.on`,
`.faq[open]`, and any future toggled card), drop the coral line and switch to a
**coral-tinted fill + settled lift**:
`--pxbg:#fdecea` (light coral) · `--pxborder:var(--color-coral-blush)` (soft edge,
**not** the flame line) · `transform:translateY(-3px)` · coral-tinted offset
shadow. Suppress the hover ring with `::after{display:none}` and restore the base
`::before` fill. End-to-end: **rest → hover (snappy lift + coral line) → commit
(coral fill, settled, no line).**

### The coral outline must be corner-accurate
The Tier-2 line wraps the **whole stepped silhouette, corners included.** A simple
inset *rectangle* leaves the corner staircase filled with card color (looks
broken), so use **two stepped polygons**: `::before` floods the outer `‹STEP 12›`
shape with `--pxborder` (coral); a hover `::after` clipped to an **inner** polygon
punches the fill back in, leaving a uniform 4px ring. The inner polygon is `‹STEP
12›` **inset 4px** — every `0→4px`, `6px→10px`, `12px→16px` (and each `100% - n`
mirrored to `100% - (n+4)`). `width:auto;height:auto` on the `::after` is
**required** so a card with a pre-existing `::after` (e.g. `.step`'s connector
arrow) can't shrink it.

```css
@media(hover:hover) and (pointer:fine){
  /* speed — snappy, and it must OUTRANK the 600–700ms .reveal entrance transition;
     keep an opacity entry or the scroll-in fade dies */
  .pxcard,.reveal.in.pxcard,.reveal-group.in>.pxcard{
    transition:transform 150ms var(--ease-out-strong),filter 150ms var(--ease-out-strong),opacity 400ms var(--ease-expo)}
  .reveal-group.in>:is(a,button,details,[role="button"]).pxcard,
  .reveal.in:is(a,button,details,[role="button"]).pxcard,
  :is(a,button,details,[role="button"]).pxcard{
    transition:transform 110ms var(--ease-out-strong),filter 110ms var(--ease-out-strong),opacity 400ms var(--ease-expo)}

  /* Tier 4 — static: lift only */
  .reveal.in.pxcard:hover,.reveal-group.in>.pxcard:hover,.pxcard:hover{transform:translateY(-3px)}

  /* Tier 2 — clickable: lift + coral ring (sides AND corners) */
  a.pxcard:hover,button.pxcard:hover,details.pxcard:hover,.pxcard[role="button"]:hover{
    --pxborder:var(--color-coral-flame);filter:drop-shadow(6px 6px 0 var(--color-coral-blush))}
  a.pxcard:hover::before,button.pxcard:hover::before,details.pxcard:hover::before,.pxcard[role="button"]:hover::before{
    background:var(--pxborder)}
  a.pxcard:hover::after,button.pxcard:hover::after,details.pxcard:hover::after,.pxcard[role="button"]:hover::after{
    content:"";position:absolute;inset:0;width:auto;height:auto;z-index:0;background:var(--pxbg);
    clip-path:polygon(/* ‹STEP 12› inset 4px → 4/10/16 … */)}
  .reveal.in :is(a,button,details,[role="button"]).pxcard:hover,
  .reveal-group.in>:is(a,button,details,[role="button"]).pxcard:hover,
  :is(a,button,details,[role="button"]).pxcard:hover{transform:translateY(-5px)}
}
/* committed state (selected / open) */
.papp-feat.on,.faq.pxcard[open]{
  --pxbg:#fdecea;--pxborder:var(--color-coral-blush);transform:translateY(-3px);
  filter:drop-shadow(5px 5px 0 rgba(239,73,61,.32))}
.papp-feat.on::after,.faq.pxcard[open]::after{display:none}
@media(prefers-reduced-motion:reduce){.pxcard:hover{transform:none!important}}
```

### Maintainer notes — specificity traps (don't trip on these)
1. **Reveal transitions own timing.** Scroll-in elements carry
   `.js .reveal-group>*{transition:…600ms}` / `.js .reveal{…700ms}` (specificity
   `0,2,0`). A faster card transition **must** outrank that with a reveal-aware
   selector (above) or hover silently runs at 600ms. Always keep an `opacity`
   entry in the override so the entrance fade survives.
2. **Reveal pins transform.** `.js .reveal.in{transform:none}` and
   `.reveal-group.in>*{transform:none}` (`0,3,0`) cancel a plain
   `.pxcard:hover{transform}` lift. The lift/commit selectors are written
   reveal-aware (`:is(...)` inflates specificity) so they win.
3. **Dark `--pxbg` needs a double class.** Set it via `.x.pxcard`
   (e.g. `.day-rhythm.pxcard{--pxbg:var(--color-ink-charcoal)}`) — the generic
   `.pxcard{--pxbg:white}` is declared later and otherwise wins.
4. **Label text + `::before`/`::after` overlays:** keep the §0 GOTCHA — wrap
   button label text in a `<span>` so `.pxcard>*{z-index:1}` lifts it above the
   pseudo-element layers.

### Adding a new card (the workflow that keeps us consistent)
- **Static info card** → plain `<div class="pxcard">`. It gets the Tier-4 lift for
  free. Done.
- **Clickable card** → make it a real `<a>`/`<button>`/`<details>` or add
  `role="button"`. It gets the Tier-2 coral-line lift **automatically** — add
  nothing.
- **Toggleable/selected card** → add `.on` when active (or use `[open]` for
  `<details>`). It gets the committed coral-fill state.
- Never style a static `<div>` to *look* clickable, and never hard-code a
  one-off hover — extend a tier instead.

---

## §3. Chips & tags (Tiny5)

Small pixel-font labels. All use `--font-pixel`, ~10–11px, letter-spacing `.06em`.

| Class | Bg | Text | Use |
|---|---|---|---|
| `.lvlchip` | chalk | slate | "LVL 3" level/status pill |
| `.beta-chip` | leaf-success | ink | "BETA" reviewer tag |
| `.sample-chip` | amber-signal | ink | "SAMPLE" placeholder marker |
| `.hero-tag` | translucent ink | coral | "LVL · CARED FOR" over media |

```css
.lvlchip{font-family:var(--font-pixel);font-size:10px;letter-spacing:.06em;
  background:var(--color-chalk-surface);color:var(--color-slate-mid);padding:1px 5px}
.beta-chip{ /* same shape */ background:var(--color-leaf-success);color:var(--color-deep-ink);font-size:11px}
```
> **App UI:** these are ready-made for level/XP badges, status pills, and
> notification counts in the pet HUD.

---

## §4. Chapter marker `.chapter`
The storybook cadence: a coral pixel cell + Tiny5 number + Onest label. One per
section.
```css
.chapter{display:inline-flex;align-items:center;gap:10px;font-family:var(--font-onest);
  font-weight:700;font-size:var(--text-body-sm);margin-bottom:var(--spacing-24)}
.chapter .cell{width:14px;height:14px;background:var(--color-coral-flame)}
.chapter .cnum{font-family:var(--font-pixel);font-size:18px;color:var(--color-coral-flame)}
.dark .chapter .cnum,.dark .chapter .cell{color:var(--band-accent);background:var(--band-accent)}
```

---

## §5. Navigation `nav`
Sticky, blurred parchment bar. Brand wordmark (Onest 800) with a coral `.bcell`
that rotates on hover; links (Onest 600 slate) + a primary `.btn`.
```css
nav{position:sticky;top:0;z-index:var(--z-nav);backdrop-filter:blur(12px);
  background:color-mix(in srgb,var(--color-warm-parchment) 85%,transparent);
  border-bottom:1px solid rgba(22,28,36,.07)}
.brand{font-family:var(--font-onest);font-weight:800;font-size:22px;display:flex;align-items:center;gap:8px}
.brand .bcell{width:12px;height:12px;background:var(--color-coral-flame);transition:transform 300ms var(--ease-expo)}
.brand:hover .bcell{transform:rotate(90deg)}
```
> **App UI:** the blurred translucent bar + coral cell brand = top app bar. The
> rotating cell is a good loading/active affordance. For a **bottom tab bar**,
> reuse `.mtab` shapes (§7) as tab items with the coral active state.

---

## §6. Chapter rail `.rail`
Fixed left vertical progress nav (hidden < 1280px). Cells light coral + label
slides in on active. `.on-dark` variant for ink sections.
```css
.rail{position:fixed;left:18px;top:50%;transform:translateY(-50%);z-index:var(--z-rail);
  display:flex;flex-direction:column;gap:8px}
.rail .rcell{width:12px;height:12px;background:var(--color-cloud-border);transition:.25s var(--ease-out-strong)}
.rail a.active .rcell{background:var(--color-coral-flame);transform:scale(1.25)}
```

---

## §7. Tabs `.mtabs` / `.mtab`
Pixel tabs (mission switcher). Same extruded treatment as `.btn` at a small notch;
active tab `.on` goes ink with white text and presses in.
```css
.mtab{--side:4px;--tab-top:var(--surface-pure-white);--tab-side:var(--color-cloud-border);
  font-family:var(--font-onest);font-weight:700;font-size:var(--text-body-sm);
  padding:11px 20px 15px;clip-path:‹STEP 8›;
  background:linear-gradient(var(--tab-top),var(--tab-top)) no-repeat 0 0/100% calc(100% - var(--side)),var(--tab-side);
  color:var(--color-slate-mid);transition:color 150ms ease,transform 70ms steps(2)}
.mtab.on{--side:2px;--tab-top:var(--color-deep-ink);--tab-side:var(--color-ink-charcoal);
  transform:translateY(2px);color:#fff}
```
> **App UI:** this *is* the segmented control / tab bar. `.on` = active route.

---

## §8. Content panels & card families
All built on `.pxcard`. Shared pattern: white fill, Onest heading, slate body,
optional Tiny5 number/icon.

- **`.step`** — numbered care-loop card; Tiny5 `.n`, coral pixel arrow `::after`
  marching between steps. Grid of 4 → 2 → 1.
- **`.mpanel`** — two-column mission panel (copy + `.mission-art` media), crossfades
  via `.mfade`/`.mfade.out`.
- **`.lib`** — library card; `.licon` stepped pixel icon. Static `<div>` → Tier-4
  lift only (see §2b); it is *not* clickable, so no coral line.
- **`.seg`** — segment card (plain).
- **`.adv`** — advisor card; stepped avatar (`‹STEP 12›`), name (Onest 800), role
  (ember), credentials list.
- **`.fun`** — dark feature card (ink fill).
- **`.faq`** — `<details>` accordion → Tier-2 clickable card: coral-line lift on
  hover, coral fill when `[open]` (see §2b). Tiny5 `.fplus` rotates 45° when open.
- **`.pullq`** — advisor pull-quote (stepped avatar + Onest quote).
- **`.revcard`** — review card on a horizontal `.rev-track` marquee; Tiny5 quote
  mark, `.beta-chip`.

```css
.step .n{font-family:var(--font-pixel);font-size:26px;color:var(--color-coral-flame)}
.faq .fplus{font-family:var(--font-pixel);font-size:20px;color:var(--color-coral-flame);
  transition:transform 200ms var(--ease-out-strong)}
.faq[open] .fplus{transform:rotate(45deg)}
```

---

## §9. Media & device

- **`.device-frame`** — pixel device shell: 3px ink border, inner 2px charcoal
  frame around video, `.df-buttons` row of round buttons (`.db.y` amber,
  `.db.r` coral, `.db.b` blue). The "handheld" frame for app/feature demos.
- **`.stage-inner`** — hero v3 standout media card: 3px ink border, ink bg,
  bold `14px 14px 0` coral-blush offset shadow, 1:1 aspect.
- **`.blueprint`** — ghost-white product photo well.
- **`.mission-art`** — parchment media well with pixel grid + centered sprite.
- **photos `.ph`** — stepped `‹STEP 12›` corners + `3px 3px 0` shadow, slight rotate.

```css
.device-frame{background:var(--surface-pure-white);border:3px solid var(--color-deep-ink);padding:10px 10px 0}
.device-frame video{width:100%;border:2px solid var(--color-ink-charcoal);background:var(--color-deep-ink)}
.stage-inner{aspect-ratio:1/1;border:3px solid var(--color-deep-ink);background:var(--color-deep-ink);
  box-shadow:var(--px-shadow-pop)}
```
> **App UI:** `.device-frame` is the natural shell for in-app screen mockups /
> "watch it work" demos in the showcase.

---

## §10. Pixel HUD elements (Tiny5 world)

- **`.meter`** — 8-bit care meter: Tiny5 label + row of `.mc` cells; `.mc.full`
  coral, animate-fill on load. The signature pet-status widget.
- **`.egg` / `.egg-card`** — stepped-silhouette pixel egg; shake + hatch + confetti
  interaction. Blind-box species reveal.
- **`.eq`** — equalizer bars (pet sound visual), coral-glow, staggered bounce.
- **`.bubble`** — pet-sound speech bubble in Tiny5 amber on ink.
- **`.spark`** — `+`-shaped twinkle (amber/coral), `twinkle` keyframe.
- **`.lb-line`** — marching-pixel dashed line (care loop), `march` keyframe.
- **`.pbtn`** — pixel play button (audio tracks); presses with hard shadow.

```css
.meter .mc{width:14px;height:14px;background:var(--color-chalk-surface)}
.meter .mc.full{background:var(--color-coral-flame)}
.meter .mlabel{font-family:var(--font-pixel);font-size:16px;letter-spacing:.08em}
.eq i{width:7px;background:var(--color-coral-glow);animation:eq 1.1s ease-in-out infinite}
```
> **App UI:** these are the highest-value carryovers — the care meter, egg/hatch,
> equalizer, and sound bubble are literally pet-app UI. Reuse directly.

---

## §11. Section dressing

- **`.marquee`** — ink ticker strip; `.marquee-track` scrolls 36s linear, coral
  `.dot` separators. (Product-fact ribbon.)
- **`.dither`** — checkerboard transition strip between light/dark bands
  (`.dither.rev` flips direction). 12px checks.
- **`.graph` / `.graph-dark`** — graph-paper background utilities (28px grid).
- **`.foot-word`** — giant Onest 900 "Nowa." footer logotype with coral period;
  `.foot-pets` species peeking.
- **`.pxslot`** — dashed placeholder slot for the graphics team (Tiny5 label +
  note). Not for production.
- **`.readbar`** — fixed top scroll-progress bar, coral.

```css
.dither{height:24px;background-color:var(--dith-dark);
  background-image:linear-gradient(45deg,var(--dith-light) 25%,transparent 25% 75%,var(--dith-light) 75%),
                   linear-gradient(45deg,var(--dith-light) 25%,transparent 25% 75%,var(--dith-light) 75%);
  background-position:0 0,6px 6px;background-size:12px 12px}
```

---

## Component → app-UI map (quick reference)

| Web component | App-UI role |
|---|---|
| `.btn` / `.btn-ghost` | primary / secondary actions |
| `.mtab` | tab bar items, segmented controls |
| `nav` (blur + coral cell) | top app bar |
| `.pxcard` | list rows, content cards, sheets |
| `.lvlchip` / `.beta-chip` | XP/level badges, status pills, counts |
| `.meter` | pet care/health/XP bar |
| `.egg` / `.egg-card` | hatch / unlock flow |
| `.eq` / `.bubble` | pet-sound feedback |
| `.device-frame` | in-showcase screen mockup |
| `.faq` (`<details>`) | settings accordions, expandable rows |
| `.dither` / `.graph` | screen section dividers, backgrounds |
