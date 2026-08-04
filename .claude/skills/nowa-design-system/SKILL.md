---
name: nowa-design-system
scope: product/nowa
version: 2.2.0
description: Apply NOWA's official design system to any Nowa visual or UI work so it carries the brand. Use whenever you build, restyle, or review anything for Nowa — app UI screens, the parent-app feature showcase, landing pages, marketing sections, banners, social/ad creative, emails, slides, icons, or any component (buttons, cards, navs, lists, modals, forms, badges). Use ESPECIALLY when converting existing app UI screens or mockups to the design system, or when someone says "make this on-brand / match Nowa / use our design system / our colors / our tokens". Trigger even if the user doesn't say "design system" — any Nowa-branded pixels are in scope. Supplies the tokens (colors, type, spacing, notch/shadow scales, motion), the component vocabulary (26 documented components + the Input form kit), the 114-icon pixel-line set (call-by-name), the mobile app-UI spec with 15 real reference screens, the LP-fluid vs app-4px-grid sizing law, the motion laws, the brand-mark rules, and the surface guides for landing pages, social/ads, graphics, and app UI.
allowed_tools:
  - Read
  - Write
  - Edit
  - Bash
owners:
  - Linhnguyen18388
  - GracefromRT
triggers:
  - /nowa-design-system
dependencies: []
---

# Nowa Design System

Nowa's visual language — **storybook warmth + pixel playfulness** — packaged
so any member (or Claude) produces on-brand Nowa pixels: warm Sunlit-cream
canvas, deep-ink night chapters, coral-only CTAs, stepped pixel corners, hard
offset shadows, Tiny5 reserved for the pet world.

## When to use

- Building or restyling ANY Nowa surface: landing pages, marketing sections,
  app UI screens, social posts, ads, banners, emails, slides, icons.
- Reviewing/auditing a design for brand compliance.
- Converting old mockups or app screens to the current system.
- Someone says "make this on-brand", "our colors", "match Nowa".

## Inputs

- The artifact to build/restyle/review (file, mockup, description).
- Target surface (landing page / social / graphic / app UI) — routes which
  reference applies, and which sizing regime governs (see below).

## Output

On-brand HTML/CSS (built on `assets/tokens.css`), a styled asset, or a
brand-compliance review — always grounded in the token set and the
non-negotiable brand rules.

## The five things people get wrong

1. **Coral `#ef493d` is the only action color.** One per view, never decorative.
2. **Tiny5 is pet-world only.** Onest headings, Noto Sans body.
3. **Two corner systems:** stepped pixel corners on drawn surfaces; soft radii
   only for photos, inputs and nav. Never round a pixel card.
4. **Hard offset shadows, never soft blur.**
5. **Two sizing regimes:** landing pages run fluid `clamp()` type; **app UI is
   strict 4px grid for everything** — spacing, padding, radius, font-size and
   computed line-height. Details in `prompt.md` and `references/APP-UI.md` §0.3.

## Detailed logic

Read **`prompt.md`** — the full instructions. Deep references in `references/`:
DESIGN · COMPONENTS · **APP-UI** (mobile spec) · MOTION · BRAND-RULES ·
**ICONS** (114-name pixel-line set) · GRAPHICS · BRAND-MARK · SOCIAL ·
AUDIT-2026-07-02 (decision log).

Assets in `assets/`: `tokens.css` / `tokens.json`, `gallery.html` (live
component library), `icons.svg` (114-icon sprite — call by name), `brand/`
(wordmarks), and **`app-ui/` — 15 self-contained parent-app screens that open
directly in a browser; start app design work from these.**

> Canonical editable source: `design-system/` + `design/tokens.css` in the
> `nowa-technologies/nowa-mkt-website` repo. Design decisions land there first,
> then re-sync into this skill folder and bump the version here.
