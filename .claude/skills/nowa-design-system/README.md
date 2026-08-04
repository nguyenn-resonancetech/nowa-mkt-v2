# `/nowa-design-system` skill

Nowa's official design system, packaged as a skill. Any member doing Nowa
visual work in Claude — landing pages, social/ad creative, app UI, slides,
banners, icons — gets the tokens, components, motion rules, and brand
guardrails applied automatically.

---

## When to use

| Situation | Use this skill? |
|---|---|
| Build/restyle a Nowa landing page or marketing section | ✅ Yes |
| Design a social post / ad / banner for Nowa | ✅ Yes |
| Build or convert parent-app UI screens | ✅ Yes |
| Build a form (input, textarea, radio, checkbox, slider) | ✅ Yes |
| Need a UI icon by name | ✅ Yes — 114-icon pixel-line set is bundled |
| Review a design for brand compliance ("is this on-brand?") | ✅ Yes |
| Anything showing Nowa-branded pixels, even if "design system" isn't said | ✅ Yes |
| Writing/rewriting Nowa copy (words, not pixels) | ❌ Use `nowa-content-writing` |
| Non-Nowa products (Pawcast etc.) | ❌ Their own design skills |

## What's inside

```
nowa-design-system/
├── SKILL.md          frontmatter + overview (this skill's contract)
├── prompt.md         the full instructions Claude follows
├── references/
│   ├── DESIGN.md         complete token + system reference
│   ├── COMPONENTS.md     26 documented components with real CSS (§12+ = Permill v3)
│   ├── APP-UI.md         parent-app spec (app bar, tab bar, rows, controls,
│   │                     sheets, states, a11y floors, the 4px grid rule)
│   ├── MOTION.md         motion laws, duration bands, signature moves
│   ├── ICONS.md          the 114-name pixel-line icon set + usage
│   ├── BRAND-RULES.md    the non-negotiables + copy guardrails
│   ├── GRAPHICS.md       pixel art, photography, icons, infographics
│   ├── BRAND-MARK.md     logo system + usage rules
│   ├── SOCIAL.md         social/ad canvases, band recipes, type floors
│   └── AUDIT-2026-07-02.md  extraction audit + decision log
└── assets/
    ├── tokens.css        the CSS variables (single source for authoring)
    ├── tokens.json       tooling mirror (W3C-ish design tokens)
    ├── gallery.html      live component library (open in a browser)
    ├── icons.svg         114-icon sprite — <use href="…#gear">
    ├── brand/ pixels/    wordmark SVGs + pet gif the gallery embeds
    └── app-ui/           15 self-contained parent-app sample screens
                          (+ their images; open any .html in a browser)
```

## The 10-second version of the brand

- Canvas: **Sunlit cream `#fdf5dd`**, graph-paper grid, deep-ink "night" bands.
- **Coral `#ef493d` is the only action color.** One per view.
- **Stepped pixel corners + hard offset shadows** on drawn surfaces; soft radii
  only for photos/inputs/nav.
- **Tiny5 pixel font = pet world only.** Onest headings, Noto Sans body.
- **Icons:** pixel art = pet world · pixel-line (Nucleo, 114 named) = utility.
  Never both in one component.
- **Sizing:** landing pages fluid (`clamp`), app UI strict 4px grid.
- Motion: chunky `steps()` for pet life, smooth expo-out for UI; nothing over
  300ms in UI; reduced-motion always handled.

## Versioning & source of truth

The canonical, editable source is `design-system/` + `design/tokens.css` in
[`nowa-technologies/nowa-mkt-website`](https://github.com/nowa-technologies/nowa-mkt-website).
Changes land there first (PR'd with the site work), then get re-synced into
this skill folder and version-bumped here. Don't edit this copy directly for
design decisions — propose them in the website repo.

v2.2.0 (2026-07-15): **pixel-line icon set** — 114 named Nucleo icons shipped
as `assets/icons.svg` + per-icon SVGs in the website repo, callable by name
(`ICONS.md`); the legacy `<img>`+invert pattern is migrated off. **Input form
kit** (text field, text area, radio, checkbox, Ranger slider) specced from the
Figma masters, with a new semantic `--color-error` token. **Sizing law
decided** — LP stays fluid `clamp()`, app UI goes strict 4px grid for
everything incl. font-size and computed line-height (`APP-UI.md` §0
directive 3; the 15 bundled screens predate it and migrate on touch). Skill
re-synced to all 10 canonical references.

v2.1.0 (2026-07-15): re-sync to the 2026-07-04 designer drop (wordmark SVGs
as the web marks → BRAND-MARK v2, pastel `.fun` cards + `.licon` pixel icons
in COMPONENTS, icon direction decided in GRAPHICS, July product facts in
BRAND-RULES) and **bundle 15 self-contained app-UI sample screens** under
`assets/app-ui/` so app design work can start from real, rendering references.
Adds the AUDIT-2026-07-02 decision log.

v2.0.0 (2026-07-02): full extraction from Permill LP v3 — tokens v2 (sage/
sand/bright-paper bands, notch + shadow scales), COMPONENTS §12–§26, new
MOTION / BRAND-MARK / APP-UI / SOCIAL / GRAPHICS references.

## Owners

Daniel (@Linhnguyen18388) — design direction · Grace (@GracefromRT) — repo
