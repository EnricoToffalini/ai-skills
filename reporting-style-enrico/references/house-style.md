# Enrico's House Style (default look for HTML output)

Enrico's personal visual identity for the web. He has chosen it as the **default for HTML reporting**, especially Quarto websites, unless he says otherwise. Everything needed is in this file and in `assets/house-style/`; do not depend on external sites or repositories to reproduce it.

Ready-made files are in `assets/house-style/`:

- `_brand.yml`: palette and fonts (Quarto brand; use with `theme: [cosmo, brand]`);
- `styles.css`: navbar, title banner, typography, links, callouts, tables, code, footer;
- `listing.css`: optional, only for Quarto listing pages (blog/news/talk lists).

## When it applies

Use it as the default for:

- Quarto websites and blogs by or for Enrico (courses, teaching material, personal projects, his research microsites);
- standalone HTML reports and supplementary materials with no other identity;
- any other HTML page for Enrico where the look has not been specified.

Do **not** impose it when:

- Enrico asks for a different look;
- an existing project already has a coherent style (preserve it; borrow at most the palette if asked);
- the project has its own identity (a lab, a consortium, a journal or society template, a co-authored project with someone else's branding): use that identity and the general rules in `html-style.md`, possibly with the same structure and a different accent;
- the output is PDF: there, borrow at most the accent color (`#9b0014`) and keep the conventions in `pdf-style.md`.

## Ingredients

- **Palette:** red `#9b0014` (accent), deep red `#5e0010`, gold `#c8a26b` (and light gold `#e7d3ae`) for thin hairlines and small details only, **white page background** `#ffffff` (not ivory or cream), warm ink `#231c19`, muted warm gray `#6f625a` for metadata, very light warm gray `#f7f5f2` only for small tinted surfaces (blockquotes, code blocks, closed `details`, hovered cards), warm hairline `#e8e1d8` for borders.
- **Fonts:** body in Source Sans Pro (the `cosmo` default); headings in **Cormorant Garamond** (600). Cormorant is thin at small sizes: use it for titles, `h2`-`h4`, card titles and subtitles, never for body text, small labels or UI.
- **Navbar:** solid red with a subtle red gradient, white text/icons, a 1 px gold hairline at the bottom, site title in Cormorant italic.
- **Title banner** (`title-block-banner: true`): full-width deep-red-to-red gradient, title in white Cormorant, subtitle in italic, gold bottom hairline. Optional soft glow and very light paper grain.
- **Hierarchy:** `h2` with a short red-to-gold rule underneath (not a full-width line); `h3`/`h4` in deep red; metadata labels and table headers in small uppercase letterspaced text.
- **Details:** links in red with an animated red-gold underline; blockquotes on a light warm-gray tint with a gold left rule; callouts as white boxes with a red left rule, thin warm border and a barely visible shadow; `details` likewise (tinted when closed, white when open); code blocks on the light tint with a thin border; booktabs-like tables with tabular numerals; centered footer with a short gold hairline above.
- **Motion:** restrained and one-off (a light sweep on the navbar at load, short fade-up of the title, listing cards lifting slightly on hover, a gold reading progress bar in pure CSS). Always respect `prefers-reduced-motion` (already in `styles.css`).

These choices are a deliberate, owner-approved identity. The cautions in `html-style.md` against gradients and banners address generic, purposeless decoration; they do not forbid this house style. Do not escalate it either: no extra hero sections, large blurred blobs, glassmorphism, or animated backgrounds beyond what is listed here.

## How to apply

1. Copy `_brand.yml` and `styles.css` next to `_quarto.yml` (or next to the `.qmd` for a standalone report).
2. Configure:

   ```yaml
   format:
     html:
       theme: [cosmo, brand]
       css: styles.css
   title-block-banner: true
   ```

   For a website, put this in `_quarto.yml`; a short centered `page-footer` with a few links fits the style.
3. For a listing page, also add `css: listing.css` on that page only.
4. Scale to the task: for a small report, keep `_brand.yml` + `styles.css` and delete the `OPTIONAL` blocks if they add nothing. Do not add JavaScript for effects; everything here is CSS.
5. Render and check desktop and mobile widths as in `qa-checklist.md`.

Fonts: Cormorant Garamond is loaded from Google Fonts through `_brand.yml`; if it is unavailable the CSS falls back to Georgia/Times, which keeps the hierarchy intact.

Known gotcha: do not declare a font family whose name contains a digit (e.g. "Source Sans 3") in `_brand.yml` typography; Quarto 1.7 emits it unquoted and the CSS declaration is invalid. Leave the body font to `cosmo`.
