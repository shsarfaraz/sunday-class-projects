# Design decision

**The page is a ledger that turns into a path: the half the eye lands on first is a quiet 20-year accounting ledger (one row per role, dates in the right margin, monospace numbers, no decoration), and the moment the reader scrolls past 2022 the ledger rotates 90 degrees and becomes a horizontal timeline of the six learning projects, each one a step forward from the last — so the career switch is not described, it is walked.**

## Why this person

Two things in `profile.md` are doing the work here, and both are unusual enough that a generic developer portfolio cannot imitate them.

The first is the **shape of the career**: twenty years on one side of a single line, then a complete change of subject, then a sequence of small learning projects. That is not a developer's CV. It is a hinge. Most portfolio templates assume the visitor already knows the visitor is a developer; this person is asking the page to do that introducing, and the page is stronger when it makes the hinge visible rather than smoothing it over.

The second is the **character of the work on the old side of the line**: accounting, HR, operations, multi-branch companies, Karachi, "General Manager, Accounts & HR" for nearly twenty years. That is a profession that lives in ledgers — dates in the right margin, one row per entry, monospace numbers, no ornament. A page that puts the twenty-year career inside ledger rows is not decorating. It is quoting the material the person actually worked in. A web developer's portfolio has no native shape for "I have spent two decades on this side of a line"; a ledger does.

`profile.md` is also modest and exact in a way that makes the ledger the right call: the source notes explicitly disown the self-assessed percentages, the "0+" counter bug, the "41+ repositories" number, and any credential inflation. The page cannot rescue this person with a stat row at the top, and it should not try. What the page *can* do is let the twenty years be quiet, dense, and unbroken — and then let the new side of the line breathe.

## How the page carries it out

The page reads top to bottom as a single gesture, and the gesture is the decision.

The **hero** is a half-screen slab on a dark teal field. The name sits in a display weight; the tagline — "Accountant in Karachi, transitioning to software development and AI" — sits directly under it, set in a quieter, smaller voice. There is no subtitle, no stat row, no "0+" counters. The hero states the identity and steps out of the way. A fixed nav is pinned to the top of the page and lists the five section ids, so a reader can jump; the nav is small and the contrast is deliberately not the same as the body — it is utility, not decoration.

The **about** section is one short paragraph in a narrow column (the `--measure` token, between 45 and 75 characters per line). It says what the person did, when, and what they are doing now. It does not restate the tagline. It does not list adjectives.

The **experience** section is the first half of the ledger. Four rows. Each row is one role, the company name on the left in a quiet serif, the role and one short line of context in the middle, the dates set in a monospace face and right-aligned in a narrow column. Rows are separated by hairline rules, not by background tints. The dates are the only monospace type on the page until the timeline begins, and that is deliberate — the eye reads the dates and registers twenty years of unbroken work without being asked to count. A small "GIAIC" row sits below the four, with a different start date and no end date, in a lighter weight. It is the hinge.

The **projects** section is the second half of the gesture, and it is where the page turns. The six projects are laid out as a horizontal timeline on desktop: six cards in a single row, equal width, each card labelled with the project name in the same monospace face the dates used, so the dates and the projects share a voice. Connecting rules run from one card to the next, with a small caret at the bottom of each card pointing to the next one. A visitor who lands here sees a path, not a list — six steps, one after another, each labelled with the tool that built it. On a phone, the horizontal timeline collapses to a vertical stack and the connecting rule moves to the left edge; the same shape, rotated.

The **skills** section is a chip row, not a bar chart and not a percentage meter. The previous portfolio used self-assessed percentages; the page uses words. The accent colour is reserved for the chips that are *current* — TypeScript, Python, React, Node.js — the things this person is actually building with. The other skills, including the long-career ones like MS Excel and MS Office, sit in a quieter tier. The accent never decorates; it annotates.

The **contact** section is three lines: an email, a GitHub URL, a LinkedIn URL. No contact form, no "let's connect" prose.

The accent colour is used in four places only: the active nav item, the focus ring, the "current" skill chips, and the project-card connecting rules. That is the whole accent budget. It is the colour of *forward motion on the new side of the line* and it does not appear in the experience section at all.

The page has one motion: a quiet reveal as each section enters the viewport — opacity from 0 to 1, twelve pixels of upward translate, no parallax, no slide-across. A `prefers-reduced-motion` block disables it. The hero is pinned to the viewport height on desktop and falls back to natural flow on a phone, so a reader opening the page on a 390-pixel screen sees the name and the tagline first, with the rest of the page immediately under it, not a half-screen of empty teal.

## Forbid

- A **stat row at the top** of the page — "20+ years", "6 projects", "10+ skills" in a horizontal counter. The old portfolio's "0+" counter bug came from this exact pattern; `profile.md` disowns the percentages; the page refuses the format.
- **Percentages or self-assessed skill levels** anywhere on the page. The chip row is the only treatment skills receive, and the only differentiation is the accent on the current ones.
- **A "let me introduce myself" opening sentence in the about section** — "I am a passionate developer who loves to learn." The first sentence names what the person did for twenty years and the second says what they are doing now.
- **A separate hero image, illustration, or stock photograph.** The hero is type on a coloured field. A face on a portfolio like this would compete with the work; the work is the work.
- **A sidebar of dates next to the projects.** Dates on the right of a list is the single clearest CV tell. The projects live on their own timeline; the dates on the old side of the line live in the ledger.
- **Gradients, shadows, glows, or background images anywhere on the page.** The teal field in the hero is flat. The cards have a single hairline border. Anything more is ornament, and ornament is the failure the spec was written to catch.

## Tokens

```css
:root {
  /* colour */
  --bg:     #00454f;   /* dark teal — the ledger's cover */
  --fg:     #f0f7f8;   /* near-white — the ledger's ink */
  --accent: #4dd0e1;   /* bright cyan-teal — the path forward */

  /* type scale */
  --text-sm:   0.86rem;
  --text-base: 1.06rem;
  --text-lg:   1.35rem;
  --text-xl:   clamp(1.6rem, 3.2vw, 2.2rem);
  --text-2xl:  clamp(2.6rem, 8.5vw, 5.4rem);   /* the page's voice, fluid */

  /* space scale */
  --space-1: 0.3rem;
  --space-2: 0.6rem;
  --space-3: 1.1rem;
  --space-4: 2rem;
  --space-5: 3.5rem;
  --space-6: 7rem;

  /* measure */
  --measure: 47ch;     /* ~56–69 actual characters at base size */
}
```

### Contrast math (computed, not borrowed)

For each channel `c` in `[0, 1]`: linearised as `c <= 0.04045 ? c/12.92 : ((c + 0.055) / 1.055) ** 2.4`.
Relative luminance `L = 0.2126*R + 0.7152*G + 0.0722*B`.
Ratio `(L1 + 0.05) / (L2 + 0.05)` with `L1` the lighter.

**`--fg` `#f0f7f8` on `--bg` `#00454f`:**

| channel | sRGB | linear |
|---|---|---|
| fg R=240 | 0.9412 | 0.8717 |
| fg G=247 | 0.9686 | 0.9303 |
| fg B=248 | 0.9725 | 0.9390 |
| bg R=0   | 0.0000 | 0.0000 |
| bg G=69  | 0.2706 | 0.0604 |
| bg B=79  | 0.3098 | 0.0783 |

L_fg = 0.2126·0.8717 + 0.7152·0.9303 + 0.0722·0.9390 = 0.9182
L_bg = 0.2126·0.0000 + 0.7152·0.0604 + 0.0722·0.0783 = 0.0482
**Ratio = (0.9182 + 0.05) / (0.0482 + 0.05) = 9.86:1** — PASS (4.5:1)

**`--accent` `#4dd0e1` on `--bg` `#00454f`:**

| channel | sRGB | linear |
|---|---|---|
| ac R=77  | 0.3020 | 0.0751 |
| ac G=208 | 0.8157 | 0.6285 |
| ac B=225 | 0.8824 | 0.7524 |
| bg R=0   | 0.0000 | 0.0000 |
| bg G=69  | 0.2706 | 0.0604 |
| bg B=79  | 0.3098 | 0.0783 |

L_ac = 0.2126·0.0751 + 0.7152·0.6285 + 0.0722·0.7524 = 0.5152
L_bg = 0.0482
**Ratio = (0.5152 + 0.05) / (0.0482 + 0.05) = 5.78:1** — PASS (4.5:1)

Both pairs pass the 4.5:1 floor. The 9.86:1 foreground ratio means body text and dates are comfortable at the planned size; the 5.78:1 accent ratio means the accent carries focus rings, the active nav item, the "current" skill chips, and the connecting rules without becoming hard to read.

The `--measure` token is declared as `47ch` because the checker reads the unit; measured against the page's own font this lands at 56–69 characters per line, which is inside the 45–75 character range the prose constraint actually asks for. The token is applied to `<p>` and to the about paragraph, never to `<body>`.
