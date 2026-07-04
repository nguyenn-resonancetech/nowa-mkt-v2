# Nowa App UI

Concrete specs for the **parent app** surface. Builds on the adaptation
principles in `BRAND-RULES.md` (§App-UI) and the app register in `MOTION.md`.
**Living reference: `app-ui/new/*.html`** — 15 built screens (mission-control,
mission-edit, growth-insights, bedtime, data-privacy, safety-alerts, …). When
this doc and those screens disagree, flag it; don't silently fork.

---

## 0. The two prime directives

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
  | Executive Function | `#e2eef7` / `#2c5a7a` *(EF blue — INTERIM, not yet in tokens; promote or replace when the domain-color set is decided)* |
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

## 5. Sheets, modals, toasts (to build — specs)

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

## 6. States (to build — specs)

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
