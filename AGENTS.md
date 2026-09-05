# Nyi Nyi Lin Running Portfolio — Agent Guide

Use this file as the starting context for all work in this repository. Do not reread every page unless the requested change requires it.

## Project purpose

This is Nyi Nyi Lin's mobile-friendly personal running record, hosted as a static GitHub Pages site at `https://nyinyilin.github.io/`.

The visual direction is clean, editorial, and minimal: oversized typography, generous spacing, dark/light section contrast, one strong accent per section, and real race media. Preserve that direction when adding features.

## Technology stack

- Static HTML5 only; no template engine.
- Plain CSS with responsive media queries and CSS custom properties.
- Small, dependency-free vanilla JavaScript.
- GitHub Pages serves the repository directly from `main`.
- Google Fonts are imported in `assets/css/styles.css`: DM Sans and Manrope.
- Images are stored locally, normally as optimized WebP files.
- Videos are local browser-ready MP4 files.
- There is no package manager, bundler, framework, database, server code, or build step.

## Important files

- `index.html` — homepage and all main sections.
- `assets/css/styles.css` — homepage styles and global design tokens.
- `assets/css/race-detail.css` — shared layout and per-event themes for race detail pages.
- `assets/js/main.js` — reveal animations, number counters, race accordions, and footer year.
- `races/<race-slug>/index.html` — standalone race detail pages.
- `assets/images/events/<race-slug>/` — certificate, result, medal, map, and race-kit media for one race.
- `assets/images/highlights/` — five race-day photos shown on the homepage.
- `assets/images/hero/` — full-screen hero image and transparent medal-tower image.
- `assets/images/video-posters/` and `assets/videos/` — homepage race videos.
- `assets/images/strava/follow-qr.webp` — Strava follow QR code.

## Homepage section order

Keep this order unless the user explicitly requests a structural change:

1. Full-screen photo hero with Nyi Nyi Lin's name.
2. Running record summary.
3. Medal Tower.
4. Race timeline.
5. Next Goal.
6. Race Day Moments.
7. Running in Motion.
8. Strava follow call-to-action.
9. Footer.

Current summary data:

- Total race distance: 72.2 km.
- Finish lines crossed: 5.
- All-time runs: 223.
- All-time distance: 1,260 km.
- Last updated: 05 September 2026.

Current goals:

- 27 September 2026 — Amazing Thailand Pattaya Marathon, 21.1 km.
- 29 November 2026 — Amazing Thailand Marathon Bangkok, 42.2 km; first full marathon.

## Race pages and official data

Use the official certificate/result values below. They replace earlier rounded estimates.

| Race | Detail path | Distance | Official finish | Pace | Theme class |
| --- | --- | ---: | ---: | ---: | --- |
| Race to Heal | `races/race-to-heal/index.html` | 10 km | 1:10:08 | 7:03/km | default |
| Bangkok Park Run | `races/bangkok-park-run/index.html` | 21.1 km | 2:39:21 | 7:33/km | `race-page--park` |
| Lazada Run | `races/lazada-run/index.html` | 10 km | 1:12:11 | 7:13/km | `race-page--lazada` |
| Amazing Thailand Marathon | `races/amazing-thailand-marathon/index.html` | 21.1 km | 2:51:07 | 8:06/km | `race-page--atm` |
| Run for Nurses | `races/run-for-nurses/index.html` | 10 km | 1:07:19 | 6:44/km | `race-page--nurses` |

Every homepage race row must remain an accordion. Expanding it shows finish time and pace. A separate orange `View race detail` link opens the standalone page. Do not turn the whole timeline row into a link.

When adding or changing an accordion:

- The button needs `.race-toggle`, `aria-expanded`, and `aria-controls`.
- The details container ID must match `aria-controls`.
- Detail-enabled rows use `.race-details--with-link` and `.race-detail-link`.
- `main.js` deliberately binds only `.race-toggle[aria-controls]`.

## Race detail page pattern

New race pages should reuse `assets/css/race-detail.css` and follow the established narrative regions where data is available:

1. Event hero with race number, date, location, and distance.
2. Official result summary.
3. Race-day location, shoe, timing, rankings, or splits.
4. Official proof: result and/or certificate.
5. Medal.
6. Course map or race kit.
7. Back-to-timeline navigation and footer.

Create a theme modifier on `<body>` and define only its color variables in `race-detail.css`; do not duplicate the shared page layout.

All local navigation links must use explicit filenames, for example:

- Homepage to detail: `races/race-to-heal/index.html`.
- Detail to homepage: `../../index.html#timeline`.

Explicit `index.html` links are required because the user also previews the site directly with `file://`, where folder URLs show a directory listing instead of loading the page.

## Design rules

- Reuse global variables from `:root` in `styles.css`: `--ink`, `--paper`, `--accent`, `--line`, `--muted`, and `--page-pad`.
- Use Manrope for large headings/numbers and DM Sans for body/interface copy.
- Prefer restrained editorial layouts over generic cards, gradients, shadows, or decorative UI.
- Maintain strong contrast and visible keyboard focus states.
- Keep headings short and use intentional line breaks where needed.
- Preserve the existing reveal-animation class pattern.
- Respect `prefers-reduced-motion`.
- Use semantic sections, headings, time elements, figures, and accessible labels.
- Mobile layouts must not rely on hover.
- Existing responsive breakpoints are 900 px and 620 px for race pages, and 760 px and 420 px for the homepage.

## Assets and media

- Store images in the relevant dedicated asset folder; never leave production assets on the Desktop or in temporary directories.
- Prefer WebP. Use lossless/high quality for QR codes and maps with small text; use quality around 88–92 for photos and certificates.
- A typical photo should be resized to roughly 1,400–1,800 px on its long edge before committing.
- Convert HEIC with `heif-convert`, then optimize the converted image with `cwebp`. Do not modify the user's original HEIC file.
- Use lowercase descriptive filenames with hyphens.
- Add useful `alt` text. Decorative elements should use `aria-hidden="true"`.
- Use `loading="lazy" decoding="async"` for below-the-fold images.
- Keep video files as H.264 MP4 with poster images, `controls`, `playsinline`, and `preload="metadata"`.
- Do not hotlink externally hosted images or videos.
- Do not expose emergency phone numbers, addresses, QR codes containing private data, or other private identifiers visible on race bibs. Crop or redact them from the committed web asset while preserving the original source file. The public Strava QR is intentionally included because the user explicitly requested it.

## External links

- Google Maps and Strava links open in a new tab.
- Always use `target="_blank" rel="noopener noreferrer"` for these external links.
- Keep URLs exactly as supplied by the user unless a displayed Markdown label differs from its actual target; use the actual target.

## What not to introduce

- Do not add React, Vue, Tailwind, Bootstrap, jQuery, npm, or a build pipeline.
- Do not add a backend, analytics, cookies, trackers, or third-party embeds unless explicitly requested.
- Do not replace local media with remote URLs.
- Do not add large animation libraries or heavy JavaScript.
- Do not duplicate the race-detail stylesheet for individual events.
- Do not change official race values back to earlier rounded estimates.
- Do not commit temporary conversion files, screenshots used only for QA, or local server artifacts.
- Do not remove or overwrite unrelated user changes in a dirty worktree.

## Validation workflow

For ordinary changes, run:

```sh
git diff --check
node --check assets/js/main.js
```

For visual or navigation changes, also start a local server from the repository root:

```sh
python3 -m http.server 4180
```

Then verify the affected page at `http://127.0.0.1:4180/`, including a narrow mobile viewport when responsive styles changed. Confirm that image requests return successfully and check that accordion buttons, explicit detail links, back links, and external links have the correct destinations.

Opening `index.html` directly is supported for quick review, but use the local HTTP server for final visual testing.

## Git and deployment

- Work on the current branch unless the user asks for another branch.
- Preserve unrelated edits.
- Do not commit or push unless the user explicitly asks.
- The live GitHub Pages site changes only after the relevant commit reaches the configured publishing branch (`main` at present).
