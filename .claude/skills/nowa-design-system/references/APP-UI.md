# Nowa App UI

Concrete specs for the **parent app** surface. Builds on the adaptation
principles in `BRAND-RULES.md` (§App-UI) and the app register in `MOTION.md`.
**Living reference: `app-ui/new/*.html`** — 15 built screens (mission-control,
mission-edit, growth-insights, bedtime, data-privacy, safety-alerts, …). When
this doc and those screens disagree, flag it; don't silently fork.

---

## 0. The three prime directives

1. **Brand the identity layer, go native on the control layer.**
   Stepped-pixel treatment for what expresses *what Nowa is*: canvas, cards,
   headers, primary CTAs, pet HUD, level chips. Familiar native patterns for
   *operating controls*: switches, steppers, sliders, checkboxes — with
   **coral as the "on" color** so they still feel Nowa. Never pixel-ify a
   30px toggle.
2. **The frequency test governs motion.** App chrome is seen 100×/day → no
   animation on tab switches, toggles snap in 200ms, never animate
   keyboard/system actions. Spend delight only on pet-world moments (hatch,
   level-up, mission complete). Full bands in `MOTION.md`.
3. **Everything sits on the 4px grid** *(app-only rule, decided 2026-07-15).*
   Marketing pages run fluid `clamp()` type and cannot hold a type grid;
   `app-ui/new/` contains **zero `clamp()`** — every value is fixed px. So the
   app can carry a real grid, and it does: **spacing, padding, margin, gap,
   radius, icon/control sizes, font-size and computed line-height are all
   multiples of 4.**

   | Axis | Allowed values |
   |---|---|
   | Font size | `12 · 16 · 20 · 24 · 28 · 32` (36 · 40 for rare hero numerals) |
   | Line-height | any ratio whose **computed px is ÷4** — 16/24 = 1.5, 20/28 = 1.4, 12/16 = 1.333 |
   | Spacing / padding / gap / margin | the `--spacing-*` ladder (4 → 96) |
   | Radius | `--radius-*` (4 · 8 · 12 · 16 · 24 · 32) |
   | Control / icon / touch size | 16 · 20 · 24 · 40 · 44 · 48 |

   **Narrow exceptions** — proportional or hairline scales, not layout:
   the notch scale `--px-step-*` (2 · 3 · 4 · 6 · 8 · 12 — sized as ⅛ of the
   element's short side), border/stroke widths (1 · 2 · 3 · 4, including the
   Nucleo icon stroke of 2 on a 24px grid), and hard-shadow offsets
   (2 · 3 · 4 · 5 · 6 · 14).

   Side effect worth keeping: the smallest app type becomes **12px**, retiring
   today's 10/11px labels — a straight accessibility win.

   ⚠️ **The 15 screens in `app-ui/new/` predate this rule and do not comply
   yet.** Audit at time of writing: 101 off-grid `font-size` declarations
   (10 · 11 · 13 · 14 · 15 · 17 · 18 · 19 · 21 · 22 · 23 · 26 · 30 · 42px) plus
   off-grid padding/gap/margin (6 · 10 · 14 · 15 · 22 · 26px). **Migrate on
   touch — do not rewrite all 15 in one pass.** Common swaps: 10/11 → 12 ·
   13/14/15 → 16 (12 if tertiary) · 17/18/19 → 20 · 21/22/23 → 24 · 26 → 24 or
   28 · 30 → 32 · 42 → 40; icon wells and back/add buttons 38 → 40.

## 1. Screen anatomy (from mission-control.html)

```
.phone (393×852 showroom shell — dev only)
 ├─ .appbar   sticky top bar
 ├─ .scroll   content, padding 0 18px 110px
 ├─ .addcta   floating primary CTA (bottom, above tabbar)
 └─ .tabbar   bottom tab bar
```

- **App bar `.appbar`** — sticky, `backdrop-filter: blur(12px)`,
  `color-mix(parchment 84%, transparent)` bg, 1px ink-alpha bottom border.
  Left: stepped back button (38px, `--px-step-sm`, white, px-shadow).
  Center/flex: Onest 800 21px title. Right: coral extruded add button
  (38px, the `.btn` construction at icon size).
- **Bottom tab bar `.tabbar`** — blur + `color-mix(parchment 92%)`, top ink
  border; tabs = 24px stroke icon + Onest 700 10px label; active =
  **coral icon/label + 14×3px coral dot underline**; inactive = mist-body.
  4–5 tabs max (Today · Pet · Growth · Controls).
- **Content canvas** — Sunlit cream. No graph-paper grid by default in-app
  (small screens; the grid is page furniture). White pxcards carry content.

## 2. List rows & groups

- **Row** — the `.pxcard` construction at row scale: `--px-step-md` clip,
  white fill, chalk 1px drawn border, `--px-shadow`, `14px 16px` padding,
  flex: `[.ic 38px stepped icon well] [.rmeta title+sub] [control] [.chev]`.
  Title Onest 700 15px; sub-row = Tiny5 time (12px) + domain chip.
  Rows stack at 12px gap; container gets `padding-right: 8px` so shadows
  don't clip.
- **Group label `.glabel`** — the in-app eyebrow: 10px coral cell + Onest 700
  11px uppercase, tracking .12em, mist-body. (Same family as `.geyebrow`;
  in-app it's allowed per group because lists genuinely need group headers.)
- **Domain chips `.tchip`** — Onest 700 10px, stepped sm clip:
  | Domain | bg / text |
  |---|---|
  | Habit & Routine | chalk / slate-mid |
  | Executive Function | `--color-info-surface` / `--color-info-ink` *(the old "EF blue INTERIM" — promoted to tokens 2026-07-15)* |
  | Emotional Regulation | coral-mist / ember-deep |
  Nowa+ locked chips carry the tiny padlock glyph (`currentColor`, opacity .7).

## 3. Controls (native layer)

- **Toggle** — 46×28 native-style switch: pill track, white round knob,
  `box-shadow 0 1px 3px`, 200ms `--ease-out-strong`; **on = coral track**.
  `aria-pressed` drives state. This is the canon toggle — never stepped.
- **Steppers / sliders / pickers** — platform defaults, coral accent color.
- **Text inputs** — soft radius (`--radius-inputs` 8px), never stepped
  (per the two-corner rule).
- **Checkbox/radio** — native or minimal custom; coral checked state.

## 4. Buttons

- **Primary `.addcta` pattern** — full-width coral extruded pixel button
  (same construction as `.btn`, `--side: 6px`), floats above the tab bar
  (`bottom: 78px`), press = `translateY(4px)` + side collapse, 70ms steps(2).
  One per screen max.
- **Secondary** — `.btn-ghost` (coral underline on press) or a white stepped
  button (backbtn construction with a label).
- **Destructive** — ember-deep fill, same construction; always paired with a
  confirm. Never optimistic (MOTION.md perceived-performance rules).

## 5. Sheets, modals, toasts (sheet BUILT — see §11.11)

- **Sheet** — slides from bottom, `translateY(100%)` → 0, 300–400ms
  `--ease-out-strong` (drawer curve ok), exit ~75% of enter; scrim =
  `rgba(22,28,36,.45)` fading in; `--z-overlay`/`--z-modal`. Surface: white
  pxcard treatment with the TOP corners stepped (bottom edges square against
  the screen edge). Drag-to-dismiss with velocity threshold (flick > 0.11
  dismisses regardless of distance); friction past the top boundary.
- **Modal (rare; confirms only)** — center, `scale(.96)+opacity` → 1, 200ms;
  `transform-origin: center`. Never `scale(0)`.
- **Toast** — enters `translateY(100%)`+fade above the tab bar, 250ms in /
  ~180ms out; **transitions, not keyframes** (rapid-fire interruptible);
  `--z-toast`. Coral only if the toast is an action confirmation.
- **Popover/menu** — `transform-origin` at the trigger; 150–200ms;
  first tooltip delayed, adjacent tooltips instant.

## 6. States (empty BUILT — see §11.4)

- **Empty** — a pet-world moment, not a gray void: small sprite or egg +
  one warm Onest line + one primary action. (See `mission-empty.html`,
  `activity-empty.html`, `growth-early.html` for the built pattern.)
- **Loading** — skeleton pxcards (chalk fill, no shimmer sweep — a gentle
  opacity pulse ≤1.2s), fade out on content; spinners only for sub-second
  waits; fast-spinning if used.
- **Error** — plain-language line + retry button; never blame the child or
  the parent ("Couldn't sync missions. Try again." — content skill register).
  No red walls: ember-deep text accent, white card.
- **Success / celebration** — reserve confetti/stepped delight for pet-world
  wins (mission complete, hatch); settings saves get a quiet toast at most.

## 7. Dark surfaces in-app

Sparing (BRAND-RULES): light/warm cards for settings and content; full ink
reserved for genuine pet-world moments (pet HUD, hatch screen, bedtime mode).
Bedtime mode may run an ink surface — see `bedtime.html`.

## 8. Accessibility & platform floors

- Touch targets ≥44×44 (back/add buttons are 38px visual inside a ≥44px
  hit area — pad the hit area, not the art).
- Contrast: body ≥4.5:1, large text ≥3:1; mist-body only for tertiary lines
  ≥13px; Tiny5 never below 12px rendered and never for essential-only info.
- Real semantics: toggles are `<button aria-pressed>`, rows that navigate are
  `<a>`/`<button>` (the §2b tier rules apply in-app too).
- `prefers-reduced-motion`: two-tier (MOTION.md) — keep state-change fades,
  drop movement.
- Hover states only behind `(hover:hover) and (pointer:fine)` — the app is
  touch-first; rely on `:active` press states instead.

## 9. Embed mode (showroom plumbing — dev only)

Every screen self-detects iframing (`window.self !== window.top` →
`html.embed`) and strips showroom chrome: transparent bg, no shadow/radius,
scrollbars hidden, fixed 770px height for the marketing `.pf-phone` frame at
`scale(.76336)`. Keep this block in every new screen; it's what lets the
marketing page showcase real screens from `file://` with no cross-document
scripting.

## 10. Carry-over map (quick)

| Need | Use | From |
|---|---|---|
| top bar | `.appbar` | mission-control.html |
| tab bar | `.tabbar` (coral dot active) | mission-control.html |
| list row | `.row` (pxcard-at-row-scale) | mission-control.html |
| group header | `.glabel` | mission-control.html |
| toggle | native-style `.toggle`, coral on | mission-control.html |
| primary CTA | `.addcta` extruded coral | mission-control.html |
| level/XP badge | `.lvlchip` / `.tchip` | COMPONENTS.md §3 |
| care meter / egg / eq / bubble | direct reuse | COMPONENTS.md §10 |
| expandable row | `.faq` grid-rows pattern | COMPONENTS.md §21 |
| screen mockup in marketing | `.pf-phone` + embed mode | COMPONENTS.md §18, §9 above |

---

## 11. App component catalogue (extracted 2026-07-15)

Mined from the 15 screens in `app-ui/new/`. **Every value below is normalised
to the 4px grid** (§0 directive 3) — where a screen currently ships an off-grid
number the "was" is noted, and the screen migrates on touch. Figma masters:
**Nowa Design System v2 → page "App UI"**.

All of these use the existing pixel language: `--px-step-sm` (8) notch for
controls/chips, `--px-step-md` (12) for cards, hard offset `--px-shadow`,
tokens for every colour. Status colours come from the token set added
2026-07-15 (`--color-success-*`, `--color-info-*`, `--color-warning-*`,
`--color-error*`).

### 11.1 Icon Button `.iconbtn`
Unifies today's `.backbtn` (8 screens), `.iconbtn` (2) and `.addbtn` (2) — one
construction, three variants.
- **40×40** *(was 38)*, notch-8, icon 20px pixel-line, centred. Hit area padded
  to ≥44 without growing the art (§8).
- `Neutral` — `--surface-pure-white` face + `--px-shadow`. Back, overflow, filter.
- `Primary` — coral extruded (the `.btn` construction at icon size, `--side: 4px`),
  white glyph. **One per screen** (it is the `.addcta` at bar scale).
- `Ghost` — transparent, ink glyph, no shadow. Dense toolbars only.
- Press `translateY(2px)` + side collapse, `70ms steps(2)`.

### 11.2 Segmented control `.seg`
Container `display:flex; gap:8` *(was 6)* wrapping app-size `.mtab`s.
- `.mtab` app size: Onest 700 **12/16**, padding **8px 16px 12px** *(was 7/14/9)*,
  notch-8, `--side: 4px`. Marketing keeps the 14px size (COMPONENTS.md §7).
- Active `.on` = ink face, white text, pressed 4px *(was 2)*.

### 11.3 Media row `.track`
Compact row for content lists (library tracks, stories, podcasts).
- `gap:12`, `padding:12px 0`, 1px `--color-chalk-surface` top border.
- Thumb `.pic` **36×36** *(was 34)*, notch-8, `--color-coral-blush` fill,
  icon 16px *(was 15)* in `--color-ember-deep`.
- Title Onest 600 **16/24** *(was 15)*, meta Noto 12/16 `--color-mist-body`.
- Differs from `.row` (§2): no pxcard shell, no chevron — it is a list item
  inside a card, not a standalone card.

### 11.4 Empty state `.empty`
**Built in 3 screens** (`activity-empty`, `mission-empty`, `growth-early`) — this
supersedes the "to build" note in §6.
- Centred column, `padding: 0 36px 40px`, `gap:8` *(was 6)*.
- `.illus` **160×160** *(was 160×150)*: notch-12 pad filled with a 45° hatch
  (`rgba(22,28,36,.045)` 8px stripes) over white, pixel sprite **88px** *(was 90)*
  centred, `image-rendering:pixelated`. Margin-bottom **16** *(was 18)*.
- Eyebrow `.ek` Tiny5 **12/16**, `.06em`, `--color-coral-flame`.
- Headline Onest 800 **24/32** *(was 22)*, max 17ch. Body Noto 14/20 slate.
- Exactly one primary action below. Never a grey void (§6).

### 11.5 Stepper `.stepper`
Native-layer ± control (§3). Today two sizes ship (44 in `controls-home`, 46 in
`bedtime`) — **unify at 44**.
- Buttons `.st` **44×44**, transparent, Onest 800 **24**, ink. Press
  `translateY(2px)`, `70ms steps(2)`. Disabled at bounds = `--color-cloud-border`.
- `gap:12` *(was 10/16)*. Value display Onest 800 **32/40**, tabular.
- Used by the bedtime time-setter (`.timeset`) and any numeric control.

### 11.6 Status badge `.badge`
Small state pill. Replaces the hardcoded hexes in `data-privacy` / `activity`.
- Onest 700 **12/16** *(was 10–11)*, padding **4px 8px** *(was 3/8 and 5/10)*,
  notch-8, optional 8×8 square dot.
- `Success` — `--color-success-surface` / `--color-success-ink`
- `Info` — `--color-info-surface` / `--color-info-ink`
- `Warning` — `--color-warning-surface` / `--color-deep-ink`
- `Neutral` — `--color-chalk-surface` / `--color-slate-mid`
- Distinct from `.lvlchip` / `.tchip`: those are pet-world (Tiny5) and domain
  labels; this one is system state and uses Onest.

### 11.7 Alert card `.alert`
Attention card for safety/permission notices.
- Notch-12 pxcard, fill `--color-warning-surface`, 1px `--color-warning-border`,
  `--px-shadow`. Padding **20** *(was 18/22)*.
- Left accent bar **4px** *(was 5)* in `--color-amber-signal`, inset 16 top/bottom
  *(was 14)*.
- Header: badge well **32×32** *(was 30)* notch-8 amber + Onest 700 16/24 title.
  Body Noto 14/20 slate. Actions right-aligned below.
- Swap the surface/border/bar triple for the error or info set to re-skin;
  **never coral** — coral is action only.

### 11.8 Insight card `.insight`
Icon + text callout ("you're on a 5-day streak").
- Notch-12 pxcard white, `--px-shadow`, padding **20** *(was 18/16)*, `gap:16`
  *(was 14)*.
- Icon well `.ic` **40×40** *(was 42)*, notch-8, tinted surface, 20px glyph.
- Title Onest 700 16/24, body Noto 14/20 slate.

### 11.9 Lock row `.lockrow`
Nowa+ gated content line at the foot of a card.
- `gap:12` *(was 10)*, `padding:12px 0 4px` *(was 0 2)*, 1px chalk top border,
  Noto **12/16** `--color-slate-mid`, padlock glyph at 70% opacity.
- Trailing unlock button **28×28** *(was 26)*, notch-8, parchment fill.

### 11.10 Heat grid `.heat-grid` + Legend `.legend`
Weekly habit data-viz.
- Grid `96px repeat(3, 1fr)`, `gap:8`. Column heads Onest 700 14/20 slate;
  row heads Noto 500 14/20 ink.
- `.cellbar` height **28** *(was 26)*, notch-8 clip. Done =
  `--color-leaf-success`, missed = `--color-chalk-surface`, partial = 50% tint.
- Legend: `gap:16`, margin-top **16** *(was 14)*, dot **12×12** *(was 13)*,
  label Onest 600 14/20 ink, hint Noto 14/20 mist.
- Charts follow GRAPHICS.md §6: hard edges, no gradients, coral only for THE
  data point.

### 11.11 Bottom sheet `.sheet`
**Built in `mission-edit`** — supersedes the "to build" note in §5.
- ⚠️ **The built version diverges from the §5 spec**: it uses
  `border-radius: 24px 24px 0 0`. **The spec wins — top corners are notch-12
  stepped, bottom edges square** against the screen edge. Migrate on touch.
- Padding **12px 20px 28px** *(was 10)*, max-height 92%, white surface.
- Drag handle **44×4** *(was 44×5)*, full radius, `--color-cloud-border`,
  margin **8px auto 16px** *(was 6/14)*.
- Backdrop `rgba(22,28,36,.55)` fading in; sheet enters `translateY(100%)`→0 in
  300–400ms `--ease-out-strong`, exit ~75%. Drag-to-dismiss per §5.
- Header `.shead`: title Onest 800 20/28 + close Icon Button (§11.1 Ghost).
