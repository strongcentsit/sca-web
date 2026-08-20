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

## Notes for future edits

- The design has no rounded corners, uses strong 2px dividers, and grayscale photography by design — see `assets/css/styles.css` and the tokens at its top before changing the visual language.
- The Google Maps embed in the contact section is a live, working iframe pinned to the Galle office — swap the `src` if the office address changes.
- Mobile nav collapses into a hamburger menu below 720px viewport width (`assets/js/main.js` + `.nav-toggle` in `assets/css/main.css`).
