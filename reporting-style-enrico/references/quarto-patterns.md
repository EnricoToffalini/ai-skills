# Quarto Starter Patterns

Adapt these patterns to the task. Do not copy every option into every project.

## Small standalone report

```text
report.qmd
styles.scss        # optional
references.bib     # optional
```

Example front matter:

```yaml
---
title: "Report title"
format:
  html:
    toc: true
    css: styles.css
  pdf:
    toc: true
execute:
  echo: false
  warning: false
  message: false
---
```

If only one format is needed, configure only that format.

## Small multi-page website

```text
_quarto.yml
index.qmd
methods.qmd
results.qmd
styles.scss
assets/
docs/              # only if GitHub Pages publishes from docs/
```

Example `_quarto.yml`:

```yaml
project:
  type: website
  output-dir: docs

website:
  title: "Project title"
  navbar:
    left:
      - href: index.qmd
        text: Home
      - href: methods.qmd
        text: Methods
      - href: results.qmd
        text: Results

format:
  html:
    theme: [default, styles.scss]
    toc: true
    anchor-sections: false

execute:
  echo: false
  warning: false
```

Keep pages at root until their number makes a `pages/` directory genuinely clearer.

## Research site with analysis outputs

```text
README.md
AGENTS.md
_quarto.yml
index.qmd
methods.qmd
results.qmd
styles.scss
R/
data/
figs/
tables/
assets/
docs/
```

Use `R/` or `scripts/`, not both, unless there is a real distinction. Keep generated tables/figures reproducible from code when possible.

## Format-specific styling

Prefer a clean shared source with format-specific adjustments rather than forcing identical rendering.

For HTML, use CSS/SCSS for:

- content width;
- navbar/colors;
- typography;
- callouts/cards;
- responsive tables/figures.

For PDF, use LaTeX includes for:

- table row spacing;
- paper/margins;
- float/page-break behavior;
- longtable/landscape needs.

## GitHub Pages

When publishing from `docs/`:

- treat `_quarto.yml`/`.qmd`/styles as source;
- treat `docs/` as generated output;
- state this in `README.md` and `AGENTS.md` for substantial projects;
- do not hand-edit files in `docs/` unless the project explicitly makes them source files.

## Generated source files

If scripts generate `.qmd`, `_quarto.yml`, or other source-like files, mark generated files clearly at their top and point to the true generator/data source. Avoid workflows where future maintainers cannot tell what may be edited safely.
