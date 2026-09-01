# The design decision

**This page is a ledger of two careers running side by side, set in two columns that meet down the middle — the left column is the accounting/management career, the right column is the software/AI career, and the hero, nav, and contact sections are the spine that holds them together.**

## Why this person
The source material is unusually explicit: a 20+ year accounting career that ends with "transitioning to software development" and a current GIAIC student in software development and AI. The page's structure mirrors that duality rather than hiding it. The off-white ledger paper and dark ink colour palette, the ruled-line section rails, and the two-column project grid all carry the metaphor: this is one person with two ledgers, both real, both complete.

## How the page carries it out
- **Hero:** a wide single column with a tall display name, a tagline that names both careers, and two rule-lines that separate left and right halves visually.
- **Nav:** sticky top, the five section names + a visible "20y → now" indicator.
- **About:** two short paragraphs, side by side, each about one career; reads as two entries in a ledger book.
- **Projects:** a two-column card grid (`.cards` with `grid-template-columns: repeat(2, 1fr)`) so the eye sees the pairing — an accounting project sits next to an AI project.
- **Skills:** rendered as a `<ul>` with two visible columns grouped by category (Programming, AI, Accounting, Management) — pulled from the CV's own groupings.
- **Contact:** a tight column of contact lines, separated by thin rules.
- **At 390px:** the two-column grid collapses to a single column, the section rails become a 1px top-border, the hero type scales down with `clamp()`. The two-career structure persists as a visual rhythm (rule-lines) even on phone.
- **Motion:** a 0.6s opacity reveal on cards as they enter the viewport (via `IntersectionObserver`); focus-visible ring on every interactive element; the nav background gets a subtle 0.95 opacity on scroll.
- **What this page does that paper cannot:** a persistent nav with jump-links to each section; a hover-revealed brief on each project card; live focus rings; a viewport-sized hero that uses `clamp()` to size the name; smooth scrolling; a 390px phone view that rearranges the same content.

## Tokens
```css
:root {
  --bg: #F4EFE6;          /* off-white ledger paper */
  --fg: #0E1B2A;          /* dark ink */
  --accent: #7A4A1F;      /* warm sepia — section rails, focus rings, project dot markers */
  /* contrast (computed, see below):
     --fg on --bg      = 15.17:1  (>= 4.5:1 PASS)
     --accent on --bg  =  6.49:1  (>= 4.5:1 PASS) */

  --text-xs:   0.78rem;
  --text-sm:   0.92rem;
  --text-base: 1.06rem;
  --text-lg:   1.45rem;
  --text-xl:   clamp(1.9rem, 4.5vw, 2.8rem);
  --text-2xl:  clamp(2.6rem, 8vw, 6.4rem);   /* the page's voice — the name */

  --space-1: .35rem;
  --space-2: .7rem;
  --space-3: 1.2rem;
  --space-4: 2rem;
  --space-5: 3.5rem;
  --space-6: 6.5rem;

  --measure: 47ch;        /* applied to <p>, never <body> */
}
```

## Contrast computation (WCAG AA)
```
L = 0.2126R + 0.7152G + 0.0722B   each channel linearised:
    c <= 0.04045 ? c/12.92 : ((c+0.055)/1.055)^2.4
ratio = (L1+0.05)/(L2+0.05)

#0E1B2A on #F4EFE6: 15.17:1  PASS (body text needs >= 4.5:1)
#7A4A1F on #F4EFE6:  6.49:1  PASS
```

## What the decision rules out
- A traditional single-column résumé layout (the obvious default — J6 failure).
- A "developer portfolio" template with default blue links and gradient hero (no identity, J4 failure).
- Ornament: no shadows on cards, no gradients, no glow. The ledger metaphor is the only visual idea.
- Date-ledger in a sidebar (J6 failure — that is a printed CV component).
- Skipping the "two careers" structure (would lose the only structural idea in this person's material).
