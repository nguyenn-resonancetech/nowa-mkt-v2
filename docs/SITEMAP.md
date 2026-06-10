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

## Section rhythm (storybook chapters)
Alternate warm-parchment (light) and deep-ink (dark) full-bleed sections down every
long page. Coral carries every CTA and accent. Hero imagery skews to children 6–8.

## Notes for the dev merge
Pages are built as clean semantic HTML against `design/tokens.css` so structure and
copy port directly into his framework. Treat these as content + layout specs, not
final production components.
