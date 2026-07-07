# Pixel Asset Brief — for the graphic team

Every slot below is visible on `pages/index-v2.html` as a dashed box labeled in
pixel type (`PX-GFX` / `PX-ICON`). Deliver assets, we swap the files — paths and
layout don't change.

**Shared specs:** PNG with transparency (or MP4/WebM for loops). Author on an
8px grid. Palette: Coral Flame `#ef493d`, Coral Glow `#f87a71`, Coral Blush
`#fececa`, Amber `#ffc107`, Leaf `#54d62c`, Deep Ink `#161c24`, Warm Parchment
`#edeae2`. Coral is reserved for action/emphasis. Sprites style-match the
existing species set (Brim, Nori, etc.).

## Video loops (temp assets currently playing in place)

| Slot | Where | Spec | Temporarily using |
|---|---|---|---|
| HERO-DEVICE-LOOP | Hero, full-bleed band | 1920×1080, seamless loop, ≤8s, device reveal, pixel style | `hero-01.mp4` (3D clouds) |
| MISSION-LOOP-HABIT | Missions tab 1, inside drawn device frame | 16:9, loop, "brush teeth" mission | `the-mission-engine-02.mp4` |
| MISSION-LOOP-EQ | Missions tab 2 | 16:9, loop, emotional-regulation mission | `the-mission-engine-04.mp4` (compressed) |
| MISSION-LOOP-EF | Missions tab 3 | 16:9, loop, focus/memory mission | `the-mission-engine-03.mp4` |
| EGG-HATCH (optional upgrade) | The World, egg card | Sprite-sheet or loop, egg shake → crack → hatch | CSS pixel egg + sprite pop |

## Pixel icons

| Slot | Where | Size | Subject |
|---|---|---|---|
| CARE-ICON-1 | Care Loop step 01 | 96×96 | Pet with emotion bubble (sound waves, "?") |
| CARE-ICON-2 | Care Loop step 02 | 96×96 | Watering can / feeding hand |
| CARE-ICON-3 | Care Loop step 03 | 96×96 | Small sprite → big sprite, evolution sparkle |
| CARE-ICON-4 | Care Loop step 04 | 96×96 | Pixel kid with star badge |
| TAB-ICON-1..3 | Mission tabs | 16×16 | Toothbrush · Heart · Brain/puzzle |
| CMP-ICON-1 | Compare col 1 | 96×96 | Cassette/audio player |
| CMP-ICON-2 | Compare col 2 | 96×96 | Building blocks |
| CMP-ICON-3 | Compare col 3 | 96×96 | Tablet with warning sparkle |
| LIB-NOWPLAYING (optional) | Library, beside active track | 32×32, 2-frame | Pet bobbing with a music note |
| FUN-ICON-1 | World, "A friend that knows them" | 96×96 | Pet with heart bubble |
| FUN-ICON-2 | World, "Grown through care" | 96×96 | Watering can + sprouting creature |
| FUN-ICON-3 | World, "Its own quirks and story" | 96×96 | Open storybook with sparkle |
| FUN-ICON-4 | World, "From the first crack" | 96×96 | Cracked egg with glow |

Note: the four World cards sit on tinted dark surfaces (coral/amber/leaf/blush
mixed into ink) — icons should read on dark.

2-frame idle animations welcome on the 96×96 icons (we animate with
`steps(2)` CSS — see the Brim bob in the Compare section for the feel).

## Already final (no work needed)
Species sprites, pixel scene illustrations (visual_10–13), device blueprint
(visual_14), advisor headshots, logo set.
