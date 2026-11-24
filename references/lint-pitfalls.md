## Lint pitfalls

These reflex hits cost a full rebuild when found late; design against them from the start.

- Add every colour, including ones added in a later rule, to the `:root` token block; a literal `oklch()` or hex in a rule fails the token check.
- Do not put `backdrop-filter` over a translucent surface; use a solid token surface and lift it by lightness.
- Give numeric display figures (stats, large readouts, prices) `font-variant-numeric: tabular-nums`, or the digits shift as they change.
- Commit an element to a hairline border or a soft shadow, not both; a bordered card with a wide shadow is flagged.
- A hero has one filled primary action; a second action is a text link, not a second filled button.
- A Reflex may be left in place only with a real reason written in the waivers line.
- Gradient text fails the gradient gate even in one brand hue: set display numerals and headings as solid accent or solid ink. Do not write `background-clip: text` at all.
- Copy must not contain an em dash or en dash (U+2014, U+2013). Use a comma, colon, full stop or parentheses in Thai and English copy alike.
- Do not hide content by default in CSS (`opacity: 0` on a reveal target). Scope the hidden state under a `.js` class the script adds on `<html>`, so the page stays readable with scripting off.
- Heading levels step one at a time (`h1`, `h2`, `h3`). Size a heading with CSS, never by picking a smaller or larger level.
- Every display head (`h1`, `h2`) carries `text-wrap: balance`, or a Thai headline wraps to an orphaned word.
- Numeric display figures and numeric selectors at display size get `font-variant-numeric: tabular-nums`, including non-counter numerals like a large `12`.
- A disabled control changes three things together: fill, ink and cursor. Its ink must still pass 4.5:1 on its fill, so opacity alone fails.
- Status pills (ok, wait, unknown, no) need text passing 4.5:1 on their tinted fill. Pick the token darker than the first instinct; the pale amber badge failed at 4.44:1.
- A box-shadow colour literal such as `rgba(...)` is a colour outside the token block. Lift it into a `--glow` or `--shadow` token.
- Pure `#fff` on a fill fails the tint gate (7a). Use a tinted paper token (for example `--paper: #f5f9ff`) for light text on accent fills.
- Text colour literals such as `rgba(255,255,255,.85)` inside a rule also fail the token check (48). Declare a `--on-acc-2`-style token for each translucent ink.
- When patching an existing stylesheet after a critique, add every new colour to the `:root` block in the same edit, then rerun sloplint. The first lint run after a patch block is where these errors show up.
