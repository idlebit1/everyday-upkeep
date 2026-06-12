# Upkeep Guides — brand assets

The mark: a deep-green rounded tile (#2c5a40), cream house silhouette (#fffdf8), gold checkmark (#e0a93d). Wordmark: "Upkeep Guides" in Fraunces, "Guides" in accent green (#3e7c59). Background cream: #faf6f0.

## Masters (edit these, then re-render)

| File | What |
|---|---|
| `mark.svg` | The icon mark, square 512 viewBox (same file as `/favicon.svg`) |
| `mark-light.svg` | Light-tile variant for dark UIs |
| `src/og-image.html` | OG/share card master (render at 1200×630) |
| `src/banner-x.html` | X/Twitter header master (render at 1500×500) |
| `src/banner-youtube.html` | YouTube channel art master (render at 2560×1440; all essential branding inside the centered 1546×423 safe zone) |
| `src/splash.html` | Wide splash master (render at 1920×1080) |
| `src/render-mark.html` | Harness for rasterizing the mark at any size |

Re-render with headless Chrome, e.g.:
`chrome --headless --window-size=1200,630 --virtual-time-budget=10000 --screenshot=assets/og-image.png file://$PWD/assets/src/og-image.html`
For small icon sizes, render at 512 and downscale with `sips -z` (Chrome renders blank below ~100px windows).

## Web icons (site root)

| File | Size | Used by |
|---|---|---|
| `/favicon.svg` | vector | modern browsers |
| `/favicon.ico` | 16+32+48 | legacy browsers, bookmarks |
| `/apple-touch-icon.png` | 180×180 | iOS home screen |
| `/icon-192.png`, `/icon-512.png` | 192/512 | `site.webmanifest` (Android/PWA) |

Every page's `<head>` carries the favicon links, theme-color (#2c5a40), and OG/Twitter meta pointing at `assets/og-image.png`. New pages: copy the block from `_template.html`.

## Social kit (`assets/social/`)

| File | Size | Use |
|---|---|---|
| `avatar-1024.png` | 1024² | profile avatar master (downscale as needed) |
| `avatar-400.png` | 400² | platforms that want small uploads |
| `avatar-light-1024.png` | 1024² | avatar on dark UIs |
| `banner-x-1500x500.png` | 1500×500 | X/Twitter profile header |
| `banner-youtube-2560x1440.png` | 2560×1440 | YouTube channel art. TVs render the whole canvas, desktop a ~2560×423 center strip, phones only the center 1546×423 — so logo/wordmark/tagline live in that safe zone and everything outside is decoration |
| `splash-1920x1080.png` | 1920×1080 | LinkedIn/anywhere wide; presentation covers |
| `../og-image.png` | 1200×630 | link-share card (also fine for Facebook/LinkedIn posts) |
