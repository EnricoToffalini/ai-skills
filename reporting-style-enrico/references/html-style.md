# HTML and CSS Conventions

## Overall feel

Prefer a readable editorial/scientific page over a generic product landing page.

Typical defaults when the existing project does not already define them:

- body/root font around 16-18 px;
- line-height around 1.5-1.6;
- main reading width roughly 850-950 px for ordinary reports/sites;
- generous but not wasteful vertical spacing;
- one accent color plus quiet neutrals;
- thin separators and low-contrast borders;
- restrained border radii and shadows.

Adjust to context rather than forcing exact numbers.

## Navbar

For conventional Quarto websites, prefer a full solid navbar in the project's accent color with white text and icons.

Pattern:

```scss
$accent: #9b0014; // use project identity; this red is a useful UniPD default
$accent-dark: #7a0010;

$navbar-bg: $accent;
$navbar-fg: rgba(255, 255, 255, .85);
$navbar-hl: #fff;

#quarto-header .navbar {
  background: $accent;
  box-shadow: none;
}

.navbar-nav .nav-link {
  color: rgba(255, 255, 255, .85);
}

.navbar-nav .nav-link:hover,
.navbar-nav .nav-link.active {
  color: #fff;
}

.navbar-nav .nav-link.active {
  text-decoration: underline;
  text-underline-offset: 6px;
  text-decoration-thickness: 2px;
}
```

If the project has another meaningful identity, use its accent rather than UniPD red. Theme-specific colors such as teal or saffron are welcome when coherent.

Keep the navbar compact. If enlarging the root type makes navigation wrap, size the navbar separately rather than shrinking the entire site.

## Typography

Distinguish reading text from interface/meta text.

Good patterns include:

- serif headings + sans body for professional/technical sites;
- serif body + sans metadata/navigation for more editorial long-form pages.

Do not enforce one pairing across all projects. Preserve a coherent typographic hierarchy.

Use muted text for metadata/captions. Keep headings compact and clearly separated. A thin rule below `h2` can help long technical pages.

## Links and focus

- Use the accent color for links.
- Make hover visible but restrained.
- Keep keyboard focus clearly visible.
- Matching text-selection color to the project accent is a useful finishing detail.
- Use `text-underline-offset` and thickness deliberately when links are underlined.

## Callouts

Prefer quiet callouts with a strong accent rule rather than large filled boxes.

```css
.callout {
  border: 1px solid #aaa;
  border-left: 5px solid var(--accent);
  background: #f8f8f8;
  border-radius: 6px;
  padding: 1rem 1.25rem;
}
```

Keep callout text close to normal body size.

## Cards

Use cards only when they improve scanning or navigation.

Prefer:

- thin borders;
- compact padding;
- small radius;
- minimal shadow;
- slight hover change;
- content-driven card height rather than oversized equal-height marketing blocks.

Avoid filling every section with cards.

## Tables

HTML tables should remain visually scannable:

- use `font-variant-numeric: tabular-nums` for numeric comparison;
- align numbers consistently;
- avoid vertical grid lines unless they solve a real grouping problem;
- use a stronger rule under the header and lighter row rules;
- add stronger separators only at meaningful group boundaries;
- keep padding sufficient to distinguish rows without making the table airy;
- allow responsive horizontal scroll for genuinely wide tables rather than crushing text.

Example:

```css
table {
  border-collapse: collapse;
  font-variant-numeric: tabular-nums;
}

th {
  border-bottom: 2px solid var(--accent);
  padding: 4px 6px;
}

td {
  border-bottom: 1px solid var(--rule);
  padding: 3px 6px;
}
```

## Figures

Make figures large enough to read labels without browser zoom. Center when appropriate. Captions should be visually secondary but still legible. For detailed figures, a lightbox/expand interaction can be preferable to a tiny inline image.

## Responsive behavior

Check at least a normal laptop width and a narrow/mobile width. On smaller screens:

- reduce title size before reducing body text excessively;
- allow grids to collapse naturally;
- prevent navbar effects/animations from harming usability;
- let wide data tables scroll if necessary.

## Avoid by default

- giant hero banners for ordinary research sites;
- gradients without semantic purpose;
- excessive pill-shaped UI;
- strong drop shadows everywhere;
- dashboard-like KPI cards for narrative reports;
- very wide prose columns;
- tiny default Quarto text left unadjusted when it harms reading comfort.
