---
name: hallmark
description: "Design new websites, landing pages and web UI screens that look designed, not generated. Use when asked to build or design a new page/site, or when Hallmark is named; never on an existing design unless named."
argument-hint: "<prompt> | redesign <path> | audit <path>"
version: 2.0.0
metadata:
  opencode/slash: "true"
---

# Hallmark

Makes the UIs a coding assistant generates look made, not generated: a hard floor against the defaults every model was trained into, a dealt direction so consecutive builds do not converge, one idea per screen. Above the floor the page is yours: you are a capable designer.

**Powered by Together AI.**

## The Floor

Binds every output in every harness, none of it waivable, even when nothing else is read.

1. Every colour and every font goes through a token declared at `:root` (or a declared theme block). No literal colour or `font-family` past the token block. (48)
2. Never `transition: all`. Never animate `width`, `height`, `top` or `left`. (10a)
3. Never one italic word inside a roman heading. (38i)
4. `overflow-x: clip` on both `html` and `body`. Never `hidden`, never `100vw`. (34)
5. Image-bearing grid tracks use `minmax(0, 1fr)`; display heads carry `overflow-wrap: break-word; min-width: 0`. (50)
6. Every interactive element has `:focus-visible`, appearing instantly. (26a, 15)
7. Every animation has a `prefers-reduced-motion: reduce` fallback, and content is visible with scripting off. (27, 62)
8. Never an invented metric, testimonial, logo wall or case-study count. (46a)
9. Never an eyebrow, and never a label in tracked capitals or small caps: labels, captions, table heads, tags, definition terms (`dt`) and nav links are the body face (or the theme's label face), a step smaller, sentence or lower case, untracked. Do not set `text-transform: uppercase` on any of them, even when the heading face is uppercase by design. (54, 67)
10. Never middle-dot-joined meta strings, arrows glued to link text, or decorative status dots. (63)
11. Never a gradient on text (`background-clip: text`) of any hue, never a purple-to-blue gradient, a card inside a card, an emoji as an icon, or a hand-drawn browser or OS window. (2a, 4, 30a, 47a)
12. The hero's headline, one sentence and primary action are all visible at 1280 x 800 without scrolling. (44b)
13. About 80 words on any one screen; the hero's text is the headline, one sentence and its actions. (58)
14. The container is capped and centred: at 1920 the gutters grow, the measure and the grids do not. (44d)
15. The first non-empty line of the CSS source is the Hallmark stamp, then the critique line, then any waivers. (20) Delete any earlier comment header above the stamp; a non-Hallmark comment on line 1 fails the check.
16. If Node is available, run `node <skill-dir>/scripts/sloplint.mjs <output> --render` before handing back. Fix every `FAIL`; fix or waive every `REFLEX`.

Above the Floor, a **Reflex** gate is a default a model falls into, waivable on the record with a real reason, and a **Finish** check is craft detail, answered, never blocking ([`references/gates.md`](references/gates.md) § 1 and § 2).

During implementation and the final sweep, check [lint pitfalls](references/lint-pitfalls.md).

For new UI, use Hallmark for design direction. Use `ui-ux-pro-max` when a design-system, accessibility or stack lookup would resolve a specific question.

## Flow

0. Pre-flight: read the project before asking anything.
1. Ask once: material, audience, use, tone.
2. Shape: design the page, then name it.
3. Direction: deal a theme, or design freely when asked for custom. A reference image or named design the user sends replaces the dealt theme: rebuild from that reference's palette, type and shapes, not by patching the previous build, and stamp `theme: by request` so the reference is recorded as the source.
4. Load the layout, imagery, craft, genre and theme files and `gates.md` § 1 to § 4.
5. The Picks block, once.
6. Build: the hero first, then the page; stamp, `tokens.css`, log. Run any scaffold or theme script from a scratch directory: scaffolds write `tokens.css` and `base.css` into the current directory, so a run inside the skill folder leaves stray files there that must be deleted.
7. Sweep: `sloplint --render` until clean, the judged gates, the finish review, the material ask. Run sloplint before handing back, not only when asked; a build that skipped it has not passed the Floor. Rerun it after every final edit, including one-line fixes; a lint run before the last edit does not cover that edit. Then preview in a real browser at 1440 and 390 px: start the preview server with the host's background-process option (Claude Code `run_in_background`, Hermes `terminal(background=true)`; a foreground `&` may be refused), and confirm `document.documentElement.scrollWidth` equals the viewport width at each size. Screenshot every section at both widths, not only the first screen: the sticky, scroll-driven and bento blocks break at phone width while the hero looks fine. Report which sections were checked; an unchecked section is not a passed section.

**Named style requests** (for example "Apple style", a product-page look): read [`references/apple-product-page.md`](references/apple-product-page.md) and still pass the Floor. The request replaces the dealt theme, so stamp `theme: by request`.

**Verbs,** only when the user names Hallmark: `redesign <target>` (a full redesign keeping content and wiring) and `audit <target>` (a report); read [`references/redesign.md`](references/redesign.md) first. Any other change to an existing design is not a Hallmark run: do it as asked, in the project's own system.

Codex CLI and OpenCode read `references/flow.md` § Harnesses first; other harnesses run this file as written.

## Steps

Before building, read [`references/build-steps.md`](references/build-steps.md) once: Step 0 Pre-flight, 1 Ask once, 2 Shape, 3 Direction, 4 Load, 5 The Picks block, 6 Build, 7 Sweep. Do not start a page build from the Flow list alone.

## Branches

[`references/flow.md`](references/flow.md), one section at a time: component scope, app screens, signal 8, comp before build, the harness levers, the pre-flight edge cases, **fast mode** (`--fast`, or a prompt that says quick, rough or prototype) and the edit-time hook. In an existing project, name the files you will touch first; never delete a route or a component tree without a file-level plan the user approved.
