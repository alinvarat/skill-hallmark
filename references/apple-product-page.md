# Apple-style product page (named style)

Use when the user asks for an Apple look, a product-page feel, or similar. The request replaces the dealt theme. The Floor still applies (tokens, no gradient text, no em dash, reduced motion, sloplint clean).

## Macrostructure
1. Slim sticky nav bar (about 48 px), light grey, logo left, 4 to 5 text links, one small filled pill CTA on the right. On phones, hide the links and keep the CTA.
2. Hero: centred, very large headline (about 6rem on desktop, clamped down), one line of lead text in ink-2, one filled primary pill and a plain text link with a trailing chevron. Product image sits below, large, on a dark device frame with generous radius.
3. A pure statement band: one sentence at about 3rem, muted grey with the key phrase in ink, 140 px vertical padding. No cards.
4. Story section, two columns: left column is a sticky panel (device mockup) that stays put; right column is three full-height text blocks, each with a numeral, a short heading, a sentence. An IntersectionObserver switches the panel state as each block enters the middle of the viewport. Only the panel changes, never the layout.
5. Feature tiles: light grey band, centred big heading, 2-column bento of white or black rounded tiles (radius about 30 px), each with a short heading, one line, and one visual at the bottom. Mix light and dark tiles so the grid has rhythm.
6. Numeral band: one oversized numeral (clamp 8rem to 20rem) in solid accent, a heading and a sub-line. Include the honest caveat in the sub-line when the content has one.
7. Interactive demo: 4/8 grid, step list on the left with the active step white on grey, a stage card on the right with shadow. Keep it honest: label simulated data as simulated.
8. Black truth band: three columns with a hairline under each heading, bullet text in light grey. Use it for "what exists / what does not".
9. Closing one-line call to action with a single filled pill, then a one-line footer on grey.

## Tokens
- Paper `#fbfbfd`, grey band `#f5f5f7`, card `#ffffff`, black `#000000`, ink `#1d1d1f`, ink-2 `#424245`, muted `#6e6e73`, rule `#d2d2d7`.
- Accent `#0071e3` (hover `#0077ed`, on-dark `#2997ff`). Ok, amber, warn each with a tinted soft fill. Check every pill ink against its fill at 4.5:1.
- Type: Inter for Latin, Anuphan for Thai, both from Google Fonts. Display weight 700 with letter-spacing about -0.02em. Body 1.0625rem at 1.6.
- Glow for the phone shadow is a token (`--glow`), not an inline `rgba`.

## Motion
- Reveal: opacity and 40 px translate, 0.9 s ease, behind a `.js` class. Set everything visible under `prefers-reduced-motion`.
- No transitions on `width`, `height`, `top`, `left`; no `transition: all`.

## Checks before handing back
- sloplint `--render` with zero FAIL.
- Screenshot each section at 1440 and at 390; confirm `scrollWidth` equals viewport width.
- The sticky panel's top offset must clear the nav (use `top: 48px` with `calc(100vh - 48px)`), or the nav covers the panel.