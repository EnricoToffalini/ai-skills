# Project Bootstrap for Substantial Reporting Work

Use this reference only when starting a substantial project from an empty/nearly empty repository or when raw material is disordered enough that a stable project structure is genuinely needed.

## Decision rule

Create project scaffolding when several of these are true:

- the work will span multiple pages/sections or multiple work sessions;
- there are source data, scripts, figures, tables, references, or assets that need stable homes;
- the repository is empty/nearly empty or contains unorganized source material;
- multiple agents or future sessions are likely to modify the project;
- rendering/publishing has nontrivial commands or generated outputs;
- the project has a meaningful roadmap with phases or dependencies.

Do **not** create `AGENTS.md`, `ROADMAP.md`, nested directories, or build machinery for a small one-off page/report merely because they are available.

## Preferred shallow tree

A substantial Quarto website/report may reasonably look like:

```text
project/
├── README.md
├── AGENTS.md
├── _quarto.yml
├── index.qmd
├── styles.scss              # or styles.css
├── references.bib           # when needed
├── assets/                  # images/static files actually used
├── R/                       # or scripts/, only if analysis/generation exists
├── data/                    # only if data can/should live in the repo
├── figs/                    # generated or publication figures, if useful
├── tables/                  # generated tabular outputs, if useful
├── pages/                   # only when many content pages justify it
└── docs/                    # generated site only when the publishing setup uses it
```

Use fewer folders whenever possible. A multi-page site with five `.qmd` files can keep them at root. Add `pages/` only when root clutter becomes a real problem.

For a manuscript-centered repository, `paper/` or `manuscript/` can replace `pages/`. Do not create both without a reason.

## Starting from messy material

Before moving files around:

1. Inventory what exists.
2. Identify human-authored sources, generated outputs, raw data, intermediate data, figures, and obsolete duplicates.
3. Decide which files are sources of truth.
4. Prefer non-destructive organization until provenance is understood.
5. Move material only when the new location is stable and obvious.
6. Do not silently discard old files because they look redundant.

## AGENTS.md

Create `AGENTS.md` for substantial projects likely to be continued by coding agents. Keep it concise and project-specific. Include only information that helps an agent work correctly.

A useful structure is:

```markdown
# AGENTS.md

## Project goal
One short paragraph describing the reporting/site goal and intended audience.

## Source of truth
- Main Quarto source: ...
- Data source(s): ...
- Generated files: ... (do not hand-edit)

## Build
- Local preview: `quarto preview`
- Full render: `quarto render`
- Any prerequisite generation step: ...

## Repository structure
Explain only non-obvious directories/files.

## Reporting conventions
- Preserve Quarto unless Enrico explicitly requests another stack.
- Keep visual style restrained and readable.
- Treat table layout as a quality-critical issue.
- Preserve existing project-specific CSS/LaTeX conventions.

## Agent behavior
- Inspect before refactoring.
- Make surgical changes to existing working structure.
- Do not introduce frameworks or abstractions without a concrete need.
- Do not hand-edit generated HTML/PDF when a source file exists.
- For long tasks, occasionally recap big-picture progress and next steps.

## Validation
List the actual render/test/check commands for this repository.
```

Do not turn `AGENTS.md` into a long generic handbook. Link to project files when possible instead of duplicating them.

## README.md

Keep `README.md` human-facing. Explain:

- what the project is;
- what the primary rendered artifact/site is;
- how to render/reproduce it;
- where important source material lives;
- publication/deployment details when relevant.

Do not make the README primarily about AI agents.

## Roadmap

Create a roadmap only for genuinely substantial, multi-stage work. It may be `ROADMAP.md` or a clearly delimited section of `AGENTS.md`/`README.md`.

A useful roadmap records:

- current phase;
- completed milestones;
- open work;
- blocking decisions/dependencies;
- next concrete steps.

Update it when the big picture changes. Do not create or maintain a roadmap for a simple report with a short finite edit list.
