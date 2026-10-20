---
name: reporting-style-enrico
description: Apply Enrico Toffalini's preferred conventions for scientific and technical reports, Quarto documents, research websites, supplementary materials, and publication-oriented HTML/PDF outputs. Use when creating or substantially revising reporting artifacts for Enrico, especially when the authoring stack is unspecified. Prefer Quarto Markdown as the default for new work, while preserving an explicit user choice or a sensible existing stack. For substantial new or nearly empty repositories, also organize a shallow, agent-friendly project and create AGENTS.md/README/roadmap material only when scale warrants it; do not add scaffolding or AI-oriented files to small or already well-structured tasks by habit.
---

# Enrico's Reporting Style

Produce reporting artifacts that are predictable, readable, reproducible, and easy to maintain. Treat Quarto as the default authoring system, not as a dogma.

## Priority order

When choices conflict, prefer in this order:

1. Explicit instructions from Enrico.
2. A coherent existing project stack and structure.
3. Readability of the rendered artifact, especially tables and figures.
4. Reproducibility and a clear source-of-truth workflow.
5. Quarto-based uniformity for new reporting work.
6. Visual polish without decorative excess.

Do not replace a working existing stack merely to impose Quarto. Do not introduce React, Jekyll, bespoke static-site frameworks, raw HTML applications, or other infrastructure for an ordinary report/site unless there is a concrete need.

## Default authoring choices

- For a new scientific/technical report, website, supplementary document, or research microsite with no requested stack, use **Quarto Markdown (`.qmd`)**.
- For web-first work, prefer Quarto HTML/website output with focused CSS/SCSS customization.
- For paginated documents, prefer Quarto PDF with targeted LaTeX adjustments rather than accepting poor default pagination.
- Use one source for multiple outputs when this remains clean, but allow HTML and PDF to have format-specific styling and layout rules.
- Keep source files inspectable. Avoid generated framework complexity that obscures where content or styling lives.
- If the task is a small one-off document, keep it small: often one `.qmd` plus at most one style/config file is enough.

## Decide whether this is a project or a document

Before adding infrastructure, classify the work:

- **Existing structured project:** preserve its tree, conventions, build commands, and source-of-truth files. Make surgical changes.
- **Small standalone report/page:** create only the files needed to author and render it. Do not add `AGENTS.md`, a roadmap, or a directory hierarchy by default.
- **Substantial new project, empty/nearly empty repository, or large body of disordered source material:** establish a shallow Quarto project, document the build, and create agent guidance so future work remains coherent. Read `references/project-bootstrap.md`.
- **Ambiguous middle case:** prefer the smaller structure. Add project-level files only when they solve a real coordination or maintenance problem.

For long-running substantial projects, keep agent-facing guidance useful to the big picture. Encourage occasional concise recaps of overall progress, current phase, major decisions, and next steps. Do not litter repositories with AI-only artifacts when the work is small.

## Visual language

**Default look for HTML output:** unless Enrico asks otherwise or the project already has (or needs) its own identity, use Enrico's **house style**, the look shared by his homepage, `/slides` and `/blog`: UniPD-like red `#9b0014` with gold hairlines on an ivory background, Cormorant Garamond headings with Source Sans Pro body, red navbar with gold hairline, red title banner. Ready-made `_brand.yml`, `styles.css` and `listing.css` are in `assets/house-style/`; read `references/house-style.md` before applying it. It applies especially to Quarto websites, but also to standalone HTML reports.

Beyond that, aim for an editorial, restrained, information-first appearance.

- Control line length and content width rather than filling the viewport.
- Prefer a strong but limited accent color and quiet neutral supporting colors.
- When a conventional top navbar is appropriate, strongly prefer a **solid accent-color bar with white text/icons** and a clear but restrained active state.
- Use muted text for metadata, captions, secondary notes, and supporting information.
- Prefer compact cards, thin rules, restrained shadows, and callouts with a strong left rule over large colored panels.
- Avoid generic "AI-designed" aesthetics: oversized hero sections, excessive gradients, huge rounded cards, decorative dashboards, and large areas of purposeless whitespace. The house style's gradient navbar/banner and gold hairlines are a deliberate identity, not a license to add more decoration.
- Use typography and spacing to show hierarchy before adding decoration.

For detailed HTML/CSS conventions, read `references/html-style.md`.

## Tables are a first-class layout problem

Never treat a table as acceptable merely because it technically fits.

- A table with overlapping text, clipped content, unreadably small type, or ambiguous row boundaries is a failed render.
- Make it visually obvious which wrapped lines belong to the same cell and where the next row begins.
- Prefer `booktabs`-like structure and semantic horizontal separation over uniform full grids.
- Align numeric material carefully; use tabular numerals where possible.
- Do not solve a difficult table only by shrinking it. First reconsider widths, wrapping, grouping, orientation, and page strategy.

For PDF/LaTeX table rules and the preferred intra-cell versus inter-row spacing pattern, read `references/pdf-style.md`.

## Repository and code conventions

When analysis code is part of the report, compose with Enrico's coding conventions if available. Keep reporting repositories shallow and transparent:

- prefer obvious folders such as `R/` or `scripts/`, `data/`, `figs/`, `tables/`, `assets/`, `paper/` only when they correspond to real categories;
- avoid `src/`, `lib/`, `utils/`, `modules/`, elaborate config systems, or deep trees by habit;
- keep generated output clearly separate from source when practical;
- never make generated HTML/PDF the only editable source.

## Workflow

1. Inspect the existing repository/material before choosing architecture.
2. Decide whether to preserve an existing stack, create a small standalone Quarto artifact, or bootstrap a substantial project.
3. Establish the source of truth and build/render commands.
4. Author content and styling with HTML/PDF-specific adjustments where useful.
5. Render the real output, not just the source.
6. Visually inspect and correct overflow, spacing, table structure, figure legibility, navigation, and pagination.
7. For substantial projects, keep `README.md`, `AGENTS.md`, and any genuine roadmap aligned with the current workflow.

Read `references/qa-checklist.md` before declaring a substantial site/report finished.

## Quarto patterns

For sensible starter structures and configuration fragments, read `references/quarto-patterns.md`. Adapt them rather than copying blindly.

## Scope discipline

This skill governs authoring system, project structure, visual reporting conventions, and rendering QA. It should compose with separate writing-style and coding-style guidance rather than duplicate them.
