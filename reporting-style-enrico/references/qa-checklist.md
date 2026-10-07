# Rendering QA Checklist

Use this checklist for substantial sites/reports. The source compiling without an error is not sufficient.

## Source and build

- Identify the editable source of truth.
- Confirm the documented render command works.
- Confirm generated outputs are regenerated from source rather than hand-edited.
- Check that relative paths work from a clean project root.
- Ensure required data/assets are present or clearly documented.

## HTML/site

- Open the rendered site, not only the `.qmd` source.
- Check a normal laptop/desktop width.
- Check a narrow/mobile width.
- Verify navbar labels, active state, links, icons, and wrapping.
- Verify reading width and body text size are comfortable.
- Check callouts/cards for excessive whitespace or awkward heights.
- Check figures at actual display size.
- Check wide tables for clipping or unreadably compressed columns.
- Check external/internal links and obvious broken assets.

## PDF

Inspect representative pages and every page containing a difficult table/figure.

- No overlapping text.
- No clipping into margins.
- Wrapped table cells remain visually grouped.
- Row boundaries are unambiguous.
- Font sizes remain readable.
- Figure labels are legible at final page size.
- Captions/notes are visually attached to their objects.
- Page breaks do not create misleading whitespace or stranded headings.
- Long tables repeat headers and break sensibly.

## Tables

For each dense table ask:

1. Can I tell immediately where each row starts and ends?
2. If a cell wraps, is it clearly still part of the same row?
3. Are numeric columns visually comparable?
4. Are group boundaries more salient than ordinary row boundaries?
5. Has scaling made the text too small?
6. Would landscape, controlled widths, or a split table be better?

If any answer is unsatisfactory, revise the table layout.

## Project hygiene

For substantial repositories:

- `README.md` still matches the real build/publish process.
- `AGENTS.md` contains project-specific guidance and no stale generic instructions.
- A roadmap exists only if the project genuinely benefits from one.
- Generated directories are clearly identifiable.
- The tree remains shallow and understandable.
- No extra framework or AI artifacts were added without a real purpose.

## Completion standard

Consider the artifact finished only when the rendered output is pleasant to read and structurally clear. Treat visual defects that impede interpretation as functional bugs.
