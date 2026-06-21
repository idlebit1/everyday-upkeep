# Everyday Upkeep

Interactive, single-file HTML guides to home maintenance tasks: how often, when, why it matters, and how to do it.

The site doubles as a subtle marketing funnel for [Upkeep Ledger](https://upkeepledger.com) (`~/code/upkeepledger`): each guide teaches a schedule, then offers the app as the way to remember it.

## Structure

- `index.html` — home page: searchable, filterable catalog of upkeep tasks grouped by category
- `gutters.html` — Gutter Upkeep guide (the reference implementation)
- 100 completed guides across the 10 categories — home: `gutters.html`, `replace-hvac-filter.html`, `test-smoke-detectors.html`, `flush-water-heater.html`, `clean-dryer-vent.html`, `clean-washing-machine.html`, `clean-shower-head.html`, `deep-clean-bathroom.html`, `replace-toilet-flapper.html`, `recaulk-shower.html`, `clean-ceiling-fans.html`, `wash-windows-interior.html`, `replace-smoke-detector-batteries.html`, `test-co-detectors.html`, `wash-windows-exterior.html`, `clean-blinds-shades.html`, `test-gfci-outlets.html`, `inspect-roof.html`; kitchen: `sharpen-knives.html`, `clean-dishwasher-filter.html`, `clean-refrigerator-coils.html`, `descale-coffee-maker.html`, `clean-garbage-disposal.html`, `deep-clean-oven.html`, `season-cast-iron.html`, `replace-water-filter.html`, `clean-range-hood-filter.html`, `descale-electric-kettle.html`, `oil-cutting-board.html`, `hone-knives.html`, `descale-espresso-machine.html`, `deep-clean-kitchen.html`; personal: `replace-toothbrush.html`, `dentist-visit.html`, `physical-exam.html`, `replace-sunscreen.html`, `clean-water-bottle.html`, `clean-makeup-brushes.html`, `replace-electric-toothbrush-head.html`; vehicle: `oil-change.html`, `check-tire-pressure.html`, `tire-rotation.html`, `replace-wiper-blades.html`, `replace-cabin-air-filter.html`, `replace-engine-air-filter.html`, `replace-car-battery.html`, `replace-spark-plugs.html`, `replace-brake-pads.html`, `detail-car-interior.html`, `wax-car.html`, `car-wash.html`; wardrobe: `wash-bedding.html`, `replace-running-shoes.html`, `rotate-mattress.html`, `replace-pillows.html`, `wash-pillows.html`, `replace-mattress.html`, `wash-duvet.html`, `condition-leather.html`, `polish-dress-shoes.html`; equipment: `clean-bike-chain.html`, `bike-tune-up.html`, `replace-helmet.html`, `battery-health-check-phone.html`, `wash-yoga-mat.html`, `clean-laptop-fans.html`, `clean-phone-case.html`, `watch-battery.html`; tools: `sharpen-mower-blade.html`, `service-snow-blower.html`, `sharpen-pruners.html`, `replace-cordless-batteries.html`, `sharpen-chainsaw-chain.html`, `lubricate-door-hinges.html`; yard: `clean-grill.html`, `fertilize-lawn.html`, `winterize-sprinklers.html`, `pressure-wash.html`, `aerate-lawn.html`, `mow-lawn.html`, `overseed-lawn.html`, `reseal-deck.html`, `mulch-beds.html`, `trim-hedges.html`, `fall-leaf-cleanup.html`, `spring-yard-cleanup.html`; pets: `trim-pet-nails.html`, `flea-tick-treatment.html`, `annual-vet-checkup.html`, `clean-litter-box.html`, `bathe-pet.html`, `brush-pet-teeth.html`, `pet-vaccinations.html`; other: `backup-data.html`, `review-insurance.html`, `update-emergency-kit.html`, `weekly-money-review.html`, `digital-cleanup.html`, `replace-passport.html`, `home-inventory.html`
- `_template.html` — skeleton for new guides, with the shared theme and TODO markers
- `data/upkeepPresets.ts` — verbatim copy of Upkeep Ledger's preset library (source of truth: `~/code/upkeepledger/backend/src/data/upkeepPresets.ts`)
- `assets/` — brand kit: mark SVGs, OG image, social banners/avatars (see `assets/README.md`); favicons + `site.webmanifest` live at the root

No build step, no dependencies. Open any file in a browser.

## Task catalog

The index inlines a curated **start set of 4 presets per category** (40 tasks across the 10 Upkeep Ledger categories: home, kitchen, personal, vehicle, wardrobe, equipment, tools, yard, pets, other), chosen from `data/upkeepPresets.ts`. Each card shows the preset's title, description, and default cadence. Cards are "Coming soon" until a guide page exists — then add the preset id → filename mapping to the `GUIDES` object in `index.html` and the card becomes a link with a "Guide ready" badge.

Search matches title, description, cadence, tags, and category name; category chips filter the view; both combine. To refresh or expand the catalog, re-copy the presets file from the app and update the inlined `PRESETS` array.

## Adding a new guide

1. Copy `_template.html` to `<slug>.html` and fill in the TODOs.
2. For interactive pieces (quiz, calendar, calculator, checklist), copy the relevant CSS/JS blocks from `gutters.html` and adapt the content/logic.
3. Use a unique localStorage key per page: `upkeepguides:<slug>:checklist`.
4. On `index.html`, change the task's card from `<div class="guide soon">` to `<a class="guide" href="<slug>.html">` and swap the "Coming soon" badge for "Guide ready".

## Conventions

- One self-contained file per guide — inline CSS and JS. The only external requests are Google Fonts (Fraunces); everything else, including all artwork, is inline.
- Shared theme tokens live in `:root` at the top of every page; keep them identical across pages.
- Typography: Fraunces (Google Fonts) for `h1`, `h2`, and the brand; system sans for body text.
- Illustrations are hand-drawn inline SVG in a flat, friendly style using the theme palette (greens `#3e7c59`/`#2c5a40`/`#5e9a78`, terracotta `#c96f4a`/`#d9663f`, gold `#e0a93d`/`#d98e3b`, water blues `#7fb3c8`/`#dce8ee`, earth tones `#b9b1a3`/`#8a6a4f`). Every page gets: a hero scene, a spot icon per "why" card, and diagram cards for key techniques. Give meaningful `role="img"` + `aria-label` to scene/diagram SVGs and `aria-hidden="true"` to decorative icons.
- Page sections, in order: hero → why it matters → how often (quiz) → calendar (if seasonal) → cost → how-to (safety + tools + technique diagrams + checklist) → when to call a pro → FAQ.
- No scroll-driven animation; hover transitions only.
- Cost figures are typical U.S. ranges, labeled as estimates.

## Upkeep Ledger funnel

Deliberately restrained — exactly two touches per page, no banners or popups:

1. **One closing card** (`.ledger-cta`, dark green) before the footer, with copy tied to what the page just taught ("you now know the schedule — let the app remember it") and a "Try Upkeep Ledger →" button.
2. **One footer line**: "From the makers of Upkeep Ledger — one place to track every recurring task."

All links use UTM params: `utm_source=upkeepguides`, `utm_medium=content`, `utm_campaign=<page-slug>` (e.g. `gutters`, `index`), `utm_content=<placement>` (`closing-card` or `footer`) — so per-guide and per-placement conversion is visible in analytics.
