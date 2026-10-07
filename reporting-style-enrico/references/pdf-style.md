# PDF and LaTeX Conventions

Treat a PDF as a typeset document, not as an automatic printout of the HTML.

## General layout

Choose paper size, margins, font size, figure placement, and pagination for the actual reading context.

- Use A4 for ordinary reports/manuscripts unless another format is appropriate.
- A5/book-like output is fine for compact reading editions, but set margins deliberately and inspect every dense element.
- Use `xelatex` when font/language requirements make it useful.
- Keep figures large enough that labels remain readable on the final page.
- `\raggedbottom` can be preferable when forcing equal page heights creates awkward vertical stretching.

## Table principle: distinguish within-cell from between-row spacing

A wrapped cell must visually read as one cell. The next table row must read as a new record.

Do **not** rely only on a global `\arraystretch` increase, because it can make wrapped lines and row boundaries equally spaced.

A preferred pattern is:

```latex
\usepackage{etoolbox}
\usepackage{array}

\AtBeginEnvironment{longtable}{%
  \linespread{0.95}\selectfont
  \setlength{\extrarowheight}{4pt}}

\AtBeginEnvironment{tabular}{%
  \linespread{0.95}\selectfont
  \setlength{\extrarowheight}{4pt}}
```

Use around 4-6 pt of `\extrarowheight` depending on the document. The key idea is more important than the exact number:

- lines **inside the same cell**: slightly tighter;
- transition **to the next row**: visibly more open.

This prevents a line wrap from being mistaken for a new observation.

## Structural table rules

Prefer:

- `booktabs` rules;
- no full vertical grid by default;
- a clear header rule;
- semantic horizontal separators at group changes;
- repeated headers for long multipage tables;
- `longtable` for naturally multipage material;
- deliberate column widths when wrapping matters;
- numeric alignment and consistent precision.

A table with overlapping text or ambiguous row boundaries is not acceptable.

## Remediation order for difficult tables

When a table does not fit/read well, try roughly in this order:

1. Remove genuinely unnecessary columns or redundant wording.
2. Shorten/clarify labels without losing meaning.
3. Set sensible column widths and wrapping.
4. Use line breaks inside headers/cells deliberately.
5. Split the table into meaningful panels/parts if that improves interpretation.
6. Use `longtable` for vertical length.
7. Use landscape for genuinely wide tables.
8. Reduce table font modestly (`\small`, `\footnotesize`, occasionally `\scriptsize` in constrained A5 material).
9. Use `scale_down`/global scaling only as a last or secondary measure, then inspect readability again.

Do not jump immediately to tiny type.

## Grouping and rules

If rows belong to groups, add a separator after the last row of a group rather than drawing the same line after every row. In `kableExtra`, `row_spec(..., hline_after = TRUE)` at meaningful boundaries is preferable to a visually noisy grid.

## APA/manuscript work

When an existing manuscript uses `apaquarto`, preserve it. Targeted LaTeX additions for table spacing, float placement, or page behavior are appropriate when they fix real rendering problems.

Do not rewrite an APA manuscript into a different framework merely because another PDF system is available.

## Page-break checks

Inspect for:

- heading orphaned at the bottom of a page;
- caption separated awkwardly from its figure/table;
- a table row split or crowded at a page break;
- large unexplained blank areas caused by float behavior;
- notes or references colliding with page margins;
- illegibly scaled figures/tables.

Fix the cause rather than accepting it as a normal LaTeX artifact.
