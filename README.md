# Everyday Upkeep

Interactive, single-file HTML guides to home maintenance tasks: how often, when, why it matters, and how to do it.

## Structure

- `index.html` — home page listing all guides (live + coming soon)
- `gutters.html` — Gutter Upkeep guide (the reference implementation)
- `_template.html` — skeleton for new guides, with the shared theme and TODO markers

No build step, no dependencies. Open any file in a browser.

## Adding a new guide

1. Copy `_template.html` to `<slug>.html` and fill in the TODOs.
2. For interactive pieces (quiz, calendar, calculator, checklist), copy the relevant CSS/JS blocks from `gutters.html` and adapt the content/logic.
3. Use a unique localStorage key per page: `everyday-upkeep:<slug>:checklist`.
4. On `index.html`, change the task's card from `<div class="guide soon">` to `<a class="guide" href="<slug>.html">` and swap the "Coming soon" badge for "Guide ready".

## Conventions

- One self-contained file per guide — inline CSS and JS. The only external requests are Google Fonts (Fraunces); everything else, including all artwork, is inline.
- Shared theme tokens live in `:root` at the top of every page; keep them identical across pages.
- Typography: Fraunces (Google Fonts) for `h1`, `h2`, and the brand; system sans for body text.
- Illustrations are hand-drawn inline SVG in a flat, friendly style using the theme palette (greens `#3e7c59`/`#2c5a40`/`#5e9a78`, terracotta `#c96f4a`/`#d9663f`, gold `#e0a93d`/`#d98e3b`, water blues `#7fb3c8`/`#dce8ee`, earth tones `#b9b1a3`/`#8a6a4f`). Every page gets: a hero scene, a spot icon per "why" card, and diagram cards for key techniques. Give meaningful `role="img"` + `aria-label` to scene/diagram SVGs and `aria-hidden="true"` to decorative icons.
- Page sections, in order: hero → why it matters → how often (quiz) → calendar (if seasonal) → cost → how-to (safety + tools + technique diagrams + checklist) → when to call a pro → FAQ.
- No scroll-driven animation; hover transitions only.
- Cost figures are typical U.S. ranges, labeled as estimates.
