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

- One self-contained file per guide — inline CSS and JS, no external assets.
- Shared theme tokens live in `:root` at the top of every page; keep them identical across pages.
- Page sections, in order: hero → why it matters → how often (quiz) → calendar (if seasonal) → cost → how-to (safety + tools + checklist) → when to call a pro → FAQ.
- Cost figures are typical U.S. ranges, labeled as estimates.
