# Central Medical Associates — Website

Live site: the `main` branch auto-deploys via GitHub Pages (~1 minute after every push).
Custom domain: cmahardin.com (once DNS is connected; otherwise the *.github.io/cma-website URL).

## What this is

A multi-page static website for Central Medical Associates, a physician-led primary care
group in Elizabethtown & Radcliff, Kentucky. **No build step, no frameworks, no dependencies,
no templating** — each `.html` file is a complete, standalone document with its own inline
`<style>` block and `<script>` tags. Photos live in `assets/img/`.

## Pages

- `index.html` — Home: hero, fact strip, About (`#about`), Mission, Services (`#services`)
- `clinicians.html` — 12 clinician cards with expandable bios
- `locations.html` — 5 offices w/ Google Maps embeds
- `patients.html` — visit prep + patient portal
- `health-library.html` — patient-education articles
- `news.html` — announcements
- `billing.html` — payment policies
- `for-clinicians.html` — clinical resources for healthcare professionals (e.g. ACC PREVENT
  cardiovascular risk calculator, an external link to tools.acc.org)
- `heat-exhaustion.html` — current seasonal "Focus On" deep-dive
- `tick-bites.html` — previous seasonal "Focus On" deep-dive
- `lipoprotein-a-apob.html` — patient-facing "Focus On" topic (not seasonal): Lp(a) and
  ApoB cholesterol markers

Every page shares the same header (top-bar, nav, announcement bar) and footer, copy-pasted
into each file — **there is no shared include/template**. About and Services are the only
sections that still live on a single page and are linked to via anchor (`index.html#about`);
everything else is a real page. The nav's "Focus On…" item is a dropdown pointing at whichever
files are the current/previous topics — when the season changes, retire the old topic to a
differently-named file (or update it in place) and repoint the dropdown + "Current feature" /
"Previous topic" kickers.

## How to make edits

1. Edit the relevant `.html` file directly (content is plain HTML; CSS is in that file's
   `<style>` block). **If the edit touches the shared header, nav, footer, or the JS at the
   bottom, apply it to all 9 files** — grep for the string you're changing across `*.html` to
   find every copy.
2. Commit and push to `main`. GitHub Pages redeploys automatically — verify at the live URL
   about a minute later. There is no build command; what you push is what serves.
3. Preview locally with `python3 -m http.server 8000` and open http://localhost:8000.
4. If you add, rename, or remove a page, update the nav on all 9 pages, `sitemap.xml`, and
   the page list above.

## Common tasks

- **Update a bio**: find the clinician's `<div class="provider-card">` in `clinicians.html`;
  the bio is inside `<details><div class="bio">`. (Spelling note: it's Carrie **Westbrook**.)
- **Add a news post**: copy an existing `<div class="post-card">` in `news.html`.
- **Add a health article**: copy an `<div class="article-card">` in `health-library.html`.
- **Change the announcement bar**: edit `.announce-text` near the top of `<body>` — on all
  9 pages.
- **Add a "Focus On" topic**: copy an existing focus page (e.g. `heat-exhaustion.html`) to a
  new filename, update its content, then update the nav dropdown links and kickers
  ("Current feature" / "Previous topic") on all 9 pages, and add the new file to `sitemap.xml`.
- **Photos**: optimized JPEGs in `assets/img/providers/` (~700px) and `assets/img/locations/`
  (~1200px). Compress before adding (`sips -s format jpeg -s formatOptions 80 -Z 700 in.png --out out.jpg`).
  Never inline images as base64.

## Design system (do not drift from it)

- Palette via CSS variables in `:root`: `--pine #24463F` (primary), `--gold #A97A2B` (accent),
  `--deepblue #1B3A5C` (info/billing thread), `--paper #F1F3EC` (ground).
- Type: Fraunces (display), Source Sans 3 (body), IBM Plex Mono (labels/eyebrows) via Google Fonts.
- Keep the flat/editorial look: 2px radii, 1px `--line` borders, mono uppercase eyebrows.
- Interactions (scroll reveal, nav active-page highlighting, back-to-top) are in the
  `<script>` at the bottom of each page and respect `prefers-reduced-motion`. Nav highlighting
  is page-based (matches the current filename), not scroll-based, since sections now live on
  separate pages.

## Facts to keep consistent (single source of truth)

- **Five locations** — four in Elizabethtown, one in Radcliff (stated in hero, fact strip,
  and `#locations`; keep all three in sync if it ever changes).
- FHH = **Family Healing and Health**, 5900 N Dixie Hwy.
- Phones: Quadri 270-769-0892 · Nasir 270-900-4555 · Ahmed 270-986-7392 · Psychiatry
  270-982-2002 · Labs 270-982-2027 · FHH 270-737-1215 · Movania (Radcliff) 270-351-3192 ·
  Billing office 270-982-2015.
- Patient portal (HEALOW): https://mycw104.ecwcloud.com/portal14112/jsp/login.jsp
- Founded 2016 (merger of the practices of Drs. Movania, Ahmed, Quadri, Nasir).
- Hours: Mon–Fri 8:00 AM – 5:00 PM. All insurances accepted; new patients welcome.

## Content cautions

- This is a medical practice site: keep health content educational, sourced (CDC etc.),
  and keep the Health Library disclaimer intact. No specific medical advice.
- Time-sensitive content to watch: the flu-vaccine announcement in the announcement bar
  (present on every page), `news.html`, and `patients.html`; and the seasonal Focus On topic
  pages.
- `_previous-draft/` is an unrelated archived early draft — ignore it; not deployed.
