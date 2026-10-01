# Binding rules for every template

These come from repeated review feedback. They are not suggestions.

## Design

1. **Section headings must be unmistakably louder than body text.** Not just
   bigger — bolder weight AND a dark ground. Every section heading sits on a dark
   band or an inset dark plate with light type, so the page skeleton is visible
   while scrolling fast without reading a word.
2. **Dark grounds are calm and deep** — navy, charcoal, deep sage, near-black.
   Never a hot saturated accent as a full-bleed section band.
3. **Parallel items are visually identical.** Four benchmark cards, four
   segments, three layers: same box treatment, same icon treatment. Only the
   glyph and the text differ. **No rotation** either — cycling a palette through
   a peer set reads as highlighting just as much as singling one out.
   Where a style needs several colours, express them at a higher level (the
   section header, a chroma bar under the heading, a kicker badge) or on
   annotation elements outside the peer set.
4. **Variety belongs between component types**, not inside a peer set — a stat
   band vs a benchmark card vs a callout vs a layer row may all differ.
5. **Visual aid over prose.** Prose is the exception. Constraints become icon
   tiles, hierarchies become ranked bars, contradictions become paired meters,
   segment profiles carry attribute bars, frameworks become matrices. If a block
   is a wall of text, it has not been designed yet.
6. **Icons** are inline SVG using `currentColor`. Several treatments across the
   page (bare oversized mark, filled disc, keyline square, inline mark, numbered
   badge, ghost watermark) — but one treatment per peer set.
7. **One cream at most.** No more than one template may use a warm cream/beige ground. Every other
   template needs a genuinely different surface, and the set must include dark
   options. Do not replace one monotony with a set of identical pale neutrals.
8. **Difference means style/brand character** — typographic voice, proportion,
   density, composition, material feel — not saturation. The test: could each
   template plausibly be a different firm's house style?

## Technical

9. **Self-contained single HTML file.** No build step. Opens from disk.
10. **No Tailwind CDN, no icon CDN.** Only Google Fonts. Real CSS in one
    `<style>` block. (The old Tailwind play-CDN config broke silently whenever a
    brace was miscounted, killing every custom colour.)
11. **All design values are CSS custom properties on `:root`.** No hardcoded hex
    outside it — that is what makes a theme swappable.
12. **Content elasticity.** No fixed heights on anything holding generated text.
    Grids use `auto-fit` so 3, 4 or 5 items all look deliberate. Blocks size to
    their own content; never force two columns to equal height. A section must
    look right with one short paragraph and with five long ones.
13. **Responsive.** Works at 375px with no horizontal scroll and no text at the
    screen edge. A 4-column table cannot compress below ~450px — stack it into
    labelled rows via `data-label`, never add horizontal scroll. Watch for
    padding shorthands wiping out a container's side gutters.
14. **Contrast.** Body and headings ≥4.5:1 against their actual background;
    graphic elements like bar fills ≥3:1. Measure, do not assume — pale accents
    almost always need a darker variant for text and a lighter one on dark
    grounds.
15. **Scroll reveal, if used, must be failure-proof.** Nothing hidden by CSS
    alone; an element only goes transparent after JS measures it as below the
    fold, measured on `window.load` so `#anchor` deep links have already
    scrolled, plus a timeout that clears every hidden flag. JS blocked, deep
    link, or iframe embed must all render the full page. Omitting animation
    entirely is fine.
16. **Print stylesheet.** Hide fixed chrome, force animated elements visible,
    convert dark bands to white/black, avoid breaking a section across pages.
17. **Semantics.** One `<h1>`; `<h2>`/`<h3>` without skipping levels; real
    `<table>` for tabular data; `tabular-nums` on all figures;
    `prefers-reduced-motion` respected.
