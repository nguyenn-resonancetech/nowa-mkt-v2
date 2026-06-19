# Nowa Brand & Design Rules

Read before designing anything Nowa — web, app, or graphic. These are the
non-negotiables that keep work on-brand. Visual rules first, then the copy
guardrails (carried from `CLAUDE.md`).

---

## Visual non-negotiables

1. **Coral Flame `#ef493d` is the only action color.** CTAs, active/selected
   states, key accents, chapter cells. Never use coral as decoration or fill a
   large area with it (except a hover "pop"). One coral per view fights with none.

2. **Tiny5 (pixel font) is pet-world only.** Pet sounds, care meters, level/XP
   tags, chapter numbers, species names, durations, "NOWA" stamps. **Never** body
   copy, paragraphs, or general UI labels. Onest does headings/labels; Noto Sans
   does body. Mixing Tiny5 into UI chrome breaks the spell.

3. **Storybook chapter rhythm.** Alternate warm parchment "day" sections and deep
   ink "night" sections. Don't run three of the same in a row. The pre-order
   moment is a calm warm-sand band (`#fff3d6`); the pet "World" chapter and footer
   stay ink in every theme.

4. **Pixel motif = the signature, used with restraint.** Graph paper, stepped
   corners, hard offset shadows, dither transitions, sparkles. Let parchment and
   negative space carry the page — pixels punctuate, they don't wallpaper.

5. **Two corner systems, on purpose.** Stepped pixel corners for drawn surfaces
   (cards, buttons, avatars, chips); soft radii for photos and text inputs. Don't
   round a pixel card or step a photograph's frame inconsistently.

6. **Hard shadows, not soft.** Offset `3px 3px 0` (or `14px 14px 0` coral-blush on
   the hero stage). Avoid blurred Material-style elevation — it's off-brand.

7. **Motion is expo-out and reduced-motion safe.** Entrances translate + fade
   (never `scale(0)`). Pixel presses use chunky `steps(2)`. Hover effects only on
   fine pointers. Always provide a `prefers-reduced-motion` instant fallback.

8. **Canvas is Sunlit cream `#fdf5dd` (paper3).** The `mint`/`sky` full-repaint
   cartridges are not the chosen direction — don't reintroduce them.

9. **Pixel art renders crisp.** `image-rendering: pixelated` on sprites/scenes;
   advisor/product photos render normally (`image-rendering: auto`).

10. **Hover strength follows interactivity.** A surface reacts to the pointer only
    in proportion to what it does — clickable things get a clear, coral
    affordance; static content stays quiet. Never make a non-interactive element
    *look* clickable. Use real semantics (`<a>`/`<button>`/`<details>`/
    `[role="button"]`) so the right tier applies automatically, and the committed
    state (selected/open) reads differently from hover. The full tiered spec lives
    in `COMPONENTS.md → §2b` — extend a tier, don't invent a one-off hover.

---

## Product facts (keep current — as of June 2026)

- **$99** device, **pre-order** now, **ships September 2026**. Optional Nowa+ subscription.
- Ages **3–10** platform claim; pull strongest at **6–9** — skew imagery to 6–8.
- Launch is **DTC** (not Kickstarter — legacy references are wrong).
- The pet **does not speak human language** — sounds, emotion, animation only.
  Never imply chatbot conversation. Don't lead with "AI companion."

---

## Copy guardrails

- Say **"built with" / "shaped by"** the advisors — **never "clinically proven."**
- Advisors: Dr. Susanne Denham (EQ), Dr. Megan McClelland (EF),
  Dr. Steven Kurtz (PCIT), Dr. David Mou (business/GTM).
- Magical pet, **not** a chatbot toy. No surveillance / behavior-control /
  obedience framing.
- Do **not** use the phrase **"empathy-based dependency."**
- "DFK" / "deeply feeling kid" is Good Inside's trademark — echo the *idea*
  (a child wired deeply), don't lift the phrase.
- Ground every claim in customer intelligence or a confirmed product fact.

---

## App-UI adaptation notes

When taking this system from marketing pages to **app screens**:

- **Brand the identity layer, native the control layer.** The pixel/stepped
  treatment expresses *what this is* — reserve it for identity & hero moments:
  the canvas, cards, headers, primary CTAs, the pet HUD, level chips. For the
  *operating controls* — toggles/switches, steppers, checkboxes, sliders — use
  familiar **native (iOS/Android) patterns**: a rounded switch, a standard
  stepper. Parents already know how they work, they're more accessible, and the
  dev gets them almost free from the platform. Keep **coral as the "on"/active
  color** so native controls still feel like Nowa. Don't pixel-ify a 30px switch —
  it adds friction for near-zero brand gain. (Mobile screens are small; spend the
  brand budget where it's seen, not on micro-controls.)
- **Keep dark "night" surfaces sparing in-app.** The parchment/ink storybook
  rhythm is great on long marketing pages, but a big dark slab on a small utility
  screen reads heavy/negative and eats vertical space. Prefer light, warm cards
  (white or a soft coral-blush tint) for app content; reserve full ink surfaces
  for genuine pet-world moments (the pet HUD, a hatch screen), not settings.
- **Carry over:** the full token set, the pixel HUD elements (meter, egg, eq,
  sound bubble, level chips — these are *already* pet-app UI), `.pxcard` surfaces,
  `.btn`/`.mtab` actions, the coral-only-CTA rule, parchment/ink surfaces.
- **Build new (the marketing system lacks these):** bottom tab bar, list rows,
  navigation headers with back/title, modals/sheets, form fields & toggles,
  empty/loading/error states, toasts. Build them *on the existing tokens and the
  stepped-corner + hard-shadow language* — don't import a generic UI kit.
- **Don't** force marketing-page components (marquee, chapter rail, giant
  footer logotype, scroll reveals) into app screens. They're page furniture.
