# Independence OS — Website

Marketing site for **Independence OS**, which runs its own clinics and builds the AI that runs them — an operating system for American healthcare. Pre-launch.

It's a single, self-contained page with client-side (hash) routing across four views: **Overview**, **Products**, **Vision**, and **Team**. No framework, no build step, no dependencies.

**Live:** independenceos.ai

## Run locally

It's a static site, so any of these work:

```bash
# Simplest: open the file directly
open index.html

# Or serve it (recommended — closer to production)
python3 -m http.server 8000
# then visit http://localhost:8000/
```

The only external request is to Google Fonts (Spectral + Hanken Grotesk); everything else — images, logo, styles, scripts — is local, so the page works offline aside from font fallbacks.

## Structure

```
.
├── index.html         # the entire site: markup, CSS, and JS in one file
├── indoslogo.png      # brand logo (used in the nav, footer, and as the favicon)
├── images/            # 14 team photos, referenced as images/<name>.jpg
├── .nojekyll          # tells GitHub Pages to serve files as-is (no Jekyll)
└── README.md
```

## What's on the page

- **Overview** — hero, the clinics we operate, how the system grows, the ecosystem diagram, the product grid, and roadmap.
- **Products** — the ten products on one shared foundation: Foundry, Models, Scribe, Clinics, Guardian, RCM, Credentialing, Supply chain, Castle, and Bishop. Includes a system diagram and a map linking to each product.
- **Vision** — the long-term thesis: build from inside the clinic outward.
- **Team** — the people, grouped by function.

Interactive bits: a light/dark theme toggle, animated product mockups, the ecosystem diagram (each product links to its card in the Overview grid), and the products map (each row links to its product section).

## Editing

Everything lives in `index.html`:

- **Team** — search for `<article class="person">` in the Team section. Each entry has a LinkedIn link, a photo tile (`images/<name>.jpg`) or initials, a name, a role, a short bio, and badge pills.
- **Products** — each product appears in three places that should stay in sync: the Overview product grid (`.ovp-card`, keyed by `data-prodlink`), the ecosystem diagram and products map, and the detail section (`<section class="prod" id="...">`). Animated mockups are driven by `data-sim` in the script at the bottom of the file.
- **Theme colors / layout** — CSS variables live in the `:root` block at the top of the `<style>` tag (e.g. `--maxw` controls the max content width).

## Deploy (GitHub Pages)

This repo is published with GitHub Pages from the default branch at:

> <https://tasmay-tibrewal.github.io/indos-web/>

Requirements for it to serve the site (rather than the README):

- The entry file must be named **`index.html`** and sit at the repo root. GitHub Pages serves `index.html` as the homepage; if it's missing, Pages falls back to rendering `README.md` as the page.
- **`.nojekyll`** is committed so Pages skips Jekyll and serves the static files exactly as they are.
- Keep `index.html`, `indoslogo.png`, `images/`, and `.nojekyll` together; asset paths are relative.

After pushing, give Pages a minute to rebuild and hard-refresh (Cmd/Ctrl+Shift+R) to clear any cached page.

Any other static host (Netlify, Vercel, S3, …) works too — just publish the repo root.

---

Houston · Bangalore — [hello@independenceos.ai](mailto:hello@independenceos.ai)
