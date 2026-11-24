# Hallmark build steps

Full Steps 0 to 7 for a Hallmark run. Read this whole file once before the first step of a page build; `SKILL.md` holds the Floor and the one-line flow.

### 0. Pre-flight

Signals, in order: `design.md` or `DESIGN.md` at the root (a locked system: it overrides everything below, and pages share it); `.hallmark/brand-spec.md` or a prompt naming a real brand (run [`references/brand-truth.md`](brand-truth.md); never theme a real brand from memory); the project's fonts, palette, spacing, motion libraries and framework (`package.json`, Tailwind config, `:root`, tokens, font links); **the product itself**: a URL, a running dev server, a project that starts with one command or an app on the machine, which the build captures with `scripts/capture.mjs` (`imagery.md` § 4); an Inspo MCP server (`mcp__inspo__*` tools: signal 8, `flow.md` § Signal 8; a `/hallmark` prompt, Hallmark named or a custom ask beats it); `TOGETHER_API_KEY` set (signal 9, the comp step).

Output one block (file:line citations, what is preserved, what is introduced), cached in `.hallmark/preflight.json` (`flow.md` § Pre-flight).

### 1. Ask once

One message, even on a five-word prompt:

> *Before I build, four things. 1. **Material**, the one that matters most: what can the page show? Screenshots or a screen recording (or point me at the app, its URL or its folder and I will run it and take them), your photos, real numbers (customers, uptime, prices), a quote with the name of who said it, logos you may use. Paste them or give paths; without photos I place stand-ins from Hallmark's photo library that your own replace later, and I never invent a number, a quote or a logo. 2. **Audience**: who uses this and what do they care about? 3. **Use**: the one action the page should drive. 4. **Tone**: pick an extreme (editorial, brutalist, soft, utilitarian, luxury, playful, technical, austere); "clean and modern" is not a tone. Plus the vibe in 4 to 8 words and an anchor colour if you have one. Or say **go ahead** and I will infer and tell you what I picked.*

Skipped fields are opt-outs: infer them, state the inferences in one line at the top of the reply, stamp them; no follow-up questions. Facts are never inferred: a number, a quote or a logo not given is absent; a picture not given is a stand-in in a slot. When the prompt answers all four, or no one can answer (a headless run, a batch), do not ask.

**Genre,** silently: *AI tool, generative, music, video, voice, dark, atmospheric* → **atmospheric**; *SaaS, enterprise, API, platform, developer tool, infra, B2B* → **modern-minimal**; *playful, fun, friendly, soft, kids, games, community* → **playful**; otherwise **editorial**, which holds most consumer and family prompts. Once a theme is dealt, its genre wins (genre file, stamp, `--genre`). When two non-default genres fire, add one either-or to the message, or on go ahead pick and say so.

**Scope.** A prompt naming one element (button, input, card, modal, nav, footer, tab strip, chip) or saying "just the X" is a component (`flow.md` § Component scope). A screen someone works in (a dashboard, an admin, settings, a tool) is an app screen (`flow.md` § App screens).

### 2. Shape

**Material first.** The inventory, one line: *real* (every concrete thing the prompt and the project supply: name, claim, numbers, places, dates, images), *pictures* (what the page shows and where each comes from: the user's, screenshots of the real product, the product built, the library), *absent* (every proof it will not have: logos, quotes, metrics nobody gave). The shape follows it: a page with pictures leads with them (`imagery.md` § 1); a page about words carries type and facts (Long Document, Letter, Index-First, Manifesto).

**The job.** Name what a visitor comes to do (subscribe, book, visit, attend, buy, try, sign up, hire, join, listen) and read that job in [`references/anatomy.md`](anatomy.md): where real sites in the category put the action, the sections they are built around (the menu, the lineup, the issues, the record), and how they end. The page is built from that anatomy, never from a default run of figures, steps and an email band (85).

Then design the page: its shape, how it opens, each section's content and composition, the nav, the footer, what carries the hero. Starting points: 21 shapes in [`references/macrostructures.md`](macrostructures.md) (load only the file you pick); compositions, navs and footers in `layout.md`.

**The draw.** On a theme build, once Step 3 has picked the theme, run `node <skill-dir>/scripts/theme.mjs draw --material photo|product|words --job <job> --theme <slug> [--log .hallmark/log.json]`. Clear of the log and the theme's picture, it deals a shape, the hero posture, the nav, the footer, the first section, where the action sits, two compositions to leave out and what the hero leads with. Take it unless the material refuses a pick, and name any swap in the Picks block: one prompt in one theme, built twice, makes two pages. **Mirror test:** would a neighbouring prompt in the same category get this exact combination? If yes, change one decision and say which.

**Signature.** The one thing a visitor would remember: the prompt's strongest real thing shown at its best (the photograph that is the place, the product doing its one job, a price set huge because it is the offer, a control to try). Make it in the theme's material (on a custom run, in its own look), show it on the first screen, name it in the Picks block and the stamp. A number drawn as marks is a device, not a signature (82).

Hold all of it; it is said once, at Step 5.

### 3. Direction

The first match wins.

1. **The user named a theme** → build it (stamp `theme: <name> (by request)`).
2. **The user asked for custom** ("custom", "derive it", "bespoke", "no theme", "a world of its own") → [`references/direction.md`](direction.md): the design is yours. It replaces the draw, the shapes, `layout.md`, the genre file and Step 6's composition and fold rules; the Floor, the gates and the sweep hold. Silence never takes this route.
3. **Everything else deals a theme:**

```
node <skill-dir>/scripts/theme.mjs deal --genre <genre> --prompt "<the prompt>" [--log .hallmark/log.json]
```

It deals three themes that fit the prompt and clear the log. Look at the three pictures, pick the one whose material can carry the prompt (motion, photographs, code), say which and why, and load only `references/themes/<slug>.md`. Re-deal only when asked (`--reroll 1`). No Node: pick from `references/themes/index.json` by hand and stamp `deal: manual`.

A theme is a material, not a plan: it never sets what the page contains or in what order. Where it and a shape, genre or craft file disagree on material, controls or motion, the theme wins; the Floor and the user's own words beat both.

### 4. Load

Exactly these, for a page build: [`references/layout.md`](layout.md) · [`references/anatomy.md`](anatomy.md), the job's part · [`references/imagery.md`](imagery.md) · [`references/craft.md`](craft.md) · `references/genres/<genre>.md` · `references/themes/<slug>.md` and its picture, already seen at the deal (a named theme: look at `<slug>.jpg` now). From the theme take its palette balance, type voice, surfaces and its Range (the sections it makes without a photograph), never its layout · [`references/gates.md`](gates.md) § 1 to § 4. A custom run loads `direction.md` instead of the layout, genre and theme files.

Only when needed, in `references/`: one macrostructure file · `microinteractions.md` for stateful UI · `interaction-and-states.md` for forms · `responsive.md` for an unusual layout · `texture.md` when the theme names texture · `scroll-choreography.md` for a scroll story · `dark-mode.md` for both modes · `data-viz.md` for charts · `fonts.md` on custom runs · `comp.md` on signal 9 (comps, generated stills) · `design-md.md` to lock the system.

`gates.md` § 5 waits for Step 7, § 6 for the reviews; loading more is the largest avoidable cost.

### 5. The Picks block

The run's only recital of its decisions, and the user's redirect window:

```markdown
**Hallmark · v2.0.0**

- **Shape** · Workbench, from draw 7f3a2c · genre modern-minimal · job: sign up, the action in the hero and beside the price
- **Theme** · Coral, dealt 2/3 (warm grey, one coral signal, General Sans, soft pills) · clears Cobalt on paper band
- **Chrome** · nav: edge-aligned, a wordmark and one action · footer: a mast, the wordmark over the links
- **Hero** · Stage: head on columns 1 to 5, the slot on 6 to 12 at 560px, centred
- **Signature** · the invoice list chasing a late payment, built live in the hero
- **Sections** · Hero (the invoice list) · Pinned (one late payment, chased in three panels) · Switcher (the client's view and yours) · Table (pricing) · Footer
- **Material** · real: the 2-minute setup, the CSV import, Lisbon · pictures: the invoice list built in the hero, library photos of a Lisbon studio (muted) · absent: logos, quotes, metrics
- **Sweep** · run after build
```

A custom run's rows are in `direction.md`. Then one quiet line, skipped in component scope or when `design.md` exists: *System portable? Say `lock the system` for a `design.md`.* On signal 9, `comp.md` runs here.

### 6. Build

- **Start from the scaffold.** `node <skill-dir>/scripts/theme.mjs scaffold <slug>` (with the deal's `--dealt`; `--custom` on a custom run) writes `tokens.css` (the theme's tokens and the shared scale) and `base.css` (what the Floor already decided) beside the project's stylesheet, and prints the stamp skeleton, the two imports and the slot script. Write only the page.
- **Read [`references/patterns.md`](patterns.md) once:** controls in all eight states, a slot, a missing fact, a form that posts nowhere yet, one reveal, figures that compare. Take their shape, never their copy.
- **Hero first.** Write the nav and the hero, nothing below them yet, run `node <skill-dir>/scripts/sloplint.mjs <file> --render --stage hero`, then the hero review in fresh context (`gates.md` § 6). Build the sections once the hero ships; photo credits and page-wide checks wait for the page.
- **One idea per screen, set big.** Hero: a headline of seven words or fewer (50 characters), one sentence of twelve words or fewer, one or two actions. Six to nine sections, hero and footer included (five on a thin prompt), 450 visible words at most, each a piece of the category's own content in a composition with mass (`layout.md` § 4 and § 5). The hero is the first screen and only the first screen, its posture taken from the job (`layout.md` § 6). Fullness comes from scale and pictures, never from more words (77 to 79).
- **Show, do not describe** (`imagery.md`). The page shows the real thing: the user's pictures, screenshots of the real product taken with `scripts/capture.mjs` whenever it can be reached, the product built at full fidelity only when it cannot, or library photographs (`node <skill-dir>/scripts/theme.mjs photos "<subject>" --theme <slug>`), big, in the theme's treatment, in slots the user's files replace, each library photo credited in the footer. Pictures take at most a third of the page below the hero, never two photograph-led sections in a row, and the theme's Range carries the rest (83). Never a stock-site URL, a drawn illustration (80), an empty wash (81), a row of counting marks (82) or an invented figure.
- **Page invariants** (F15): one primary button style, one container width, one column gap below the hero, one radius per nesting level, never more centred heading groups than left-aligned ones.
- **Type and motion** (`craft.md` § 1 and § 5). The theme's faces, two families at most (three with one outlier role); body 16px or more; heads one weight and one colour (38iii); labels never mono unless mono is the material (64). Eight states on every control; `transform` and `opacity` only; one reveal at most, none where the theme keeps still, visible by default.
- **Stamp.** Line 1 of CSS is the scaffold's stamp skeleton with every field filled, then the critique line (`gates.md` § 3), then any `waive` and `answered` lines, all within the first 40 lines.
- **Existing stylesheets are append-only:** the imports go right after the last `@import`, never below a rule or a `@tailwind` directive; reuse the project's token names ([`references/export-formats.md`](export-formats.md)).
- **Log.** `node <skill-dir>/scripts/theme.mjs log --entry '<json>'` puts the build atop `.hallmark/log.json` with the fields rotation reads (`shape`, `theme`, `axes`, `hero`, `nav`, `footer`, `imagery`, `photos`, `entry`, `fingerprint`, `sections`, `signature`, `waived`, `prompt`) and names any you left out.

### 7. Sweep

1. `node <skill-dir>/scripts/sloplint.mjs <files> --genre <genre> --render` (`--scope component` or `--scope app` where it applies; in a framework project, `--url http://localhost:<port>/<route>` with the dev server running). Fix every FAIL and re-run until clean. The render tier writes the screenshots; never drive a browser by hand.
2. Load [`references/gates.md`](gates.md) § 5 and walk the J and R/J gates. Confirm or dismiss every WARN. Fix every open Floor finding; fix or waive every Reflex one; answer every Finish one.
3. The finish review in fresh context (`gates.md` § 6; the reviewer reads its prompt, you never open `review-*.md`): act on its first word (`recapture`, `rebuild`, `fix`, `ship`) and score the fixes yourself.
4. Close with the material ask: every slot, its size and what belongs there, then the one piece of material that would most improve the page.
5. Update the Picks block: any row the build changed, and the last row with the outcome (`Floor 0 FAIL · Reflex 2 (1 waived: 47b) · finish-review: subagent, 3 resolved`). A fabricated pass is itself slop.

Verification is budgeted: one batched inspection, one fix batch, at most one confirming round; each review adds one fix batch and its recapture.
