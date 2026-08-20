# Strong Cents Associates — Website

A one-page marketing site for Strong Cents Associates, a Sri Lankan accounting, bookkeeping, payroll and HR outsourcing firm.

Built as a static HTML/CSS/JS site (no build step, no framework) on the "Modernist" design system, customised with the brand's blue accent.

## Project structure

```
index.html              Single-page site (nav, hero, stats, services, about, testimonials, contact, footer)
assets/
  css/
    styles.css           Design-system tokens and component classes (source of truth for colors, spacing, buttons, cards, nav)
    main.css              Page layout and section styles built on top of the design-system tokens
  js/
    main.js               Mobile nav (hamburger) toggle
  images/                Logo and photography (grayscale via CSS filter)
favicon.ico              Multi-size icon (16/32/48px) for browser tabs and Google search results
favicon-16x16.png        \
favicon-32x32.png         > Standalone PNG favicons referenced directly in <head>
apple-touch-icon.png     / iOS home-screen icon (180x180, opaque white background)
android-chrome-192x192.png \
android-chrome-512x512.png  > Referenced from site.webmanifest for Android/PWA install icons
site.webmanifest        PWA manifest listing the Android icons, theme and background color
.claude/launch.json      Local dev server config (used by the Claude Code browser preview)
```

## Local development

No build step or dependencies — it's plain HTML/CSS/JS. To preview it locally you just need any static file server, since the page loads CSS/JS/images via relative paths that won't resolve correctly from a bare `file://` URL.

Pick whichever you have available:

```bash
npx --yes serve -l 4173 .
```

```bash
python -m http.server 4173
```

Then open `http://localhost:4173`.

## Editing content

- **Copy, links, contact details**: edit directly in `index.html`.
- **Colors, spacing, type, shadows**: edit the CSS custom properties at the top of `assets/css/styles.css`.
- **Section layout**: edit `assets/css/main.css`.
- **Testimonials**: the three testimonial cards in `index.html` (search `testimonial-quote`) currently hold placeholder copy — replace with real client quotes when available.
- **Images**: replace files in `assets/images/` with the same filenames, or update the `src` attributes in `index.html`. Keep photography passed through the `.grayscale` class per the design system.

## Deployment guide

This is a static site — any static host works. Two common options:

### Option A — GitHub Pages (simplest, no extra service)

1. In the GitHub repo, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to `Deploy from a branch`.
3. Set **Branch** to `main` and folder to `/ (root)`, then **Save**.
4. GitHub will publish the site at `https://strongcentsit.github.io/sca-web/` within a minute or two.
5. To use a custom domain (e.g. `www.strongcents.lk`), add it under **Settings → Pages → Custom domain**, and create a `CNAME` DNS record at your domain registrar pointing to `strongcentsit.github.io`. GitHub will add a `CNAME` file to the repo automatically once verified.

Every push to `main` redeploys automatically — no CI config needed for a plain static site.

### Option B — Netlify / Vercel / Cloudflare Pages

1. Create a new site/project and connect it to the `strongcentsit/sca-web` GitHub repo.
2. Build command: none (leave blank).
3. Publish/output directory: `/` (repo root).
4. Deploy. Subsequent pushes to `main` redeploy automatically.
5. Attach a custom domain from the host's dashboard (each provides its own DNS instructions).

### Manual/self-hosted (e.g. shared hosting, VPS, cPanel)

Upload the contents of the repo (`index.html` and the `assets/` folder) to the web server's public root (e.g. `public_html/`) via FTP/SFTP or the host's file manager. No server-side runtime is required — any web server that can serve static files (Apache, Nginx, IIS) works.

> **Current production status:** `strongcents.lk` is already live, serving a different, existing site (a separate React/Vite build). This repo is the redesign and is not yet what visitors to `strongcents.lk` see. Cutting the domain over — updating DNS/hosting to point at wherever this repo gets deployed — is a manual step outside this repo; do that deliberately once the redesign is approved, not as a side effect of pushing here.

## Favicon & Google Search indexing

The root-level `favicon.ico`, `favicon-16x16.png`, `favicon-32x32.png`, `apple-touch-icon.png`, `android-chrome-192x192.png`/`android-chrome-512x512.png` and `site.webmanifest` were generated from a 48×48 "SCA" monogram source using high-quality bicubic upscaling (no AI upscaling — the 512×512 and 180×180 versions are honestly soft/blurred rather than fake-detailed, since the true source is small). If a higher-resolution master logo becomes available later, regenerate the larger sizes from that instead for a crisper result.

For the favicon to actually show up in Google search results, three things need to be true, and only the first is something this repo controls:
1. **The page serves a valid, crawlable icon** — done here via the `<link rel="icon">` tags in `index.html`'s `<head>`.
2. **The site is verified in Google Search Console** for whichever domain ends up serving it (`strongcents.lk` once cut over, or the GitHub Pages/host URL if that's the canonical one). This requires access to the Google account that owns/manages `strongcents.lk` — it can't be done from this repo or by an AI assistant. In Search Console: **Settings → Ownership verification**, or add the property fresh if it isn't already verified.
3. **Google has crawled/indexed the page since the favicon was added.** After verifying, use **URL Inspection → Request Indexing** on the homepage to speed this up; otherwise Google will pick it up on its next regular crawl (can take days to weeks). Favicons are also cached separately from the page and can lag behind even after reindexing.

Since `strongcents.lk` currently points at a different, already-indexed site, don't request reindexing until after the domain actually serves this redesign — otherwise Google will (re-)index the old site's content, not this one.

## Notes for future edits

- The design has no rounded corners, uses strong 2px dividers, and grayscale photography by design — see `assets/css/styles.css` and the tokens at its top before changing the visual language.
- The Google Maps embed in the contact section is a live, working iframe pinned to the Galle office — swap the `src` if the office address changes.
- Mobile nav collapses into a hamburger menu below 720px viewport width (`assets/js/main.js` + `.nav-toggle` in `assets/css/main.css`).
