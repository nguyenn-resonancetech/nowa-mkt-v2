# Sitemap & Message Architecture

Every page maps to a job and a segment. The site's emotional throughline is the
universal spine (guilt → repair → calm → unprompted regulation); each page leads
with the hook for the segment most likely to land on it.

## Information architecture

```
/                      Home — the whole promise in one scroll
/how-it-works          The Care Loop, the non-verbal pet, a day with Nowa
/the-science           4 advisors, the 3 pillars, "built with" — the proof page
/compare               Nowa vs Yoto vs Tonies vs Lovevery (intercepts comparison search)
/pre-order             Conversion page — $99, ships Sept 2026, what's in the box
/blog                  SEO content hub (problem-query articles)
/blog/{article}        Individual articles
/lp/{campaign}         Ad landing pages (one per segment/angle; share design system)
/about                 Mission, team, the Era-4 / calm-tech story
/faq                   Safety, COPPA, age range, subscription, shipping
```

## Page → job → segment → lead hook

| Page | Primary job | Lead segment | Hook |
|---|---|---|---|
| Home | Communicate the whole promise; route to pre-order | All (spine) | "Your child's first friend who helps them grow." |
| How it works | Make the Care Loop + non-verbal pet legible | Routine Battler, Firefighter | "It doesn't talk to your kid — it needs your kid." |
| The Science | Earn trust via mechanism + advisors | Method Practitioner | "Built with the scientists who wrote the science." |
| Compare | Win the consideration set | Community Curator, Gift-Giver | "Screen-free like Yoto. Developmental like Lovevery. But alive." |
| Pre-order | Convert | All warm | "Reserve yours — ships September 2026." |
| Blog | Earn search traffic on problem queries | Cold-register entry | Problem-first titles (see CONTENT-PLAN) |
| /lp/* | Convert paid traffic by segment | Per campaign | Inherits ad angle; one message, one CTA |

## Homepage content balance (parent-outcome vs kid-delight)
The hero and close are 100% the parent's (spine register). Mid-page, the site must
answer her second objection — "will my kid actually love it?" — with the fun proof:
the reward engine (blind egg, a pet that grows through care, the species world) and
the Library (screen-free audio: story, song, podcast, soundscapes). Roughly **60/40
parent-outcome to kid-delight** by page area. Rules:

- **All learning runs through missions**, synced to real-world actions (brush teeth,
  bedtime, calm-down, focus tasks). Fun sections appear *downstream* of the missions
  story and exist to explain *why the mechanism works* ("children follow through on
  things they care about") or what the device does between missions.
- **Variety, never accumulation.** The species world is "who might you meet," not
  "collect them all." No gacha/FOMO framing — this audience is allergic to it.
- The Library is framed as **screen-free audio** (enters the Yoto/Toniebox
  consideration set) and pre-builds the Nowa+ value story.
- Kid-fun sections double as the Nostalgia Bridge Dad surface (pixel pets, mystery
  egg = Tamagotchi memory) without switching the page's register.
- **Pre-pivot cleanup:** the product pivoted from human-voice responses to
  animation/action/pet-sound responses. Any ported copy implying the pet converses
  ("responds with warmth," "not generic scripts") must be rewritten to non-verbal
  framing before it ships.
- **Advisor quotes:** advisor sections carry full credentials (from the LP repo's
  advisory data) plus quote slots. Quotes must be real and approved by each advisor —
  never drafted on their behalf. Placeholders stay clearly marked until then.

## Section rhythm (storybook chapters)
Alternate warm-parchment (light) and deep-ink (dark) full-bleed sections down every
long page. Coral carries every CTA and accent. Hero imagery skews to children 6–8.

## Notes for the dev merge
Pages are built as clean semantic HTML against `design/tokens.css` so structure and
copy port directly into his framework. Treat these as content + layout specs, not
final production components.
