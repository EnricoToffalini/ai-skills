---
name: coding-style-enrico
description: Write, revise, debug, or extend code in Enrico Toffalini's preferred academic coding style. Use for data analysis, statistical modelling, simulations, reproducible research scripts, Quarto/R Markdown code, and repository organization, especially in R and occasionally Python. Prefer simple, explicit, compact, self-contained research code over software-engineering abstractions. Preserve existing code surgically when editing. Apply unless Enrico explicitly requests a different style, a production-grade software architecture, or project conventions clearly require otherwise.
---

# Enrico's Coding Style

Write code for academic research as if the main goals are transparency, inspectability, easy manual debugging, and getting the analysis right. Do not optimize for software-engineering elegance by default.

## Priority order

When choices conflict, prefer in this order:

1. Statistical/scientific correctness.
2. Reproducibility and transparency.
3. Simple code that can be read top-to-bottom.
4. Compactness.
5. Computational efficiency when it materially matters.
6. Generality, abstraction, extensibility, defensive programming.

Do not sacrifice correctness merely to imitate a rough style. Otherwise, resist "improving" simple research code into a framework.

## Language defaults

- Use **R by default** for data analysis, statistics, simulations, and plotting.
- Do not switch an R task to Python merely because a Python solution is convenient.
- Use Python only when requested, when the existing project is Python, or when the task genuinely depends on a Python-specific ecosystem.
- In R, prefer ordinary base-R constructs plus focused domain packages.
- Treat **ggplot2 as the default plotting system**.
- Avoid the tidyverse as a default dependency apart from ggplot2. Use `dplyr`, `tidyr`, `purrr`, etc. only when they make a particular operation clearly simpler or are already central to the project.

## Core style

- Write code that proceeds visibly from inputs to transformations to models to outputs.
- Prefer explicit intermediate objects over dense nesting or long pipelines.
- Prefer short, ordinary object names when their meaning is obvious: `df`, `fit`, `model`, `results`, `N`, `niter`, `power`.
- Preserve the naming conventions of existing code when editing it.
- Prefer `=` for ordinary assignment in new R code, matching Enrico's usual style. Do not churn existing code solely to change assignment operators.
- Prefer simple indexing and direct column assignment when readable.
- Accept some duplication when removing it would require a helper, abstraction, or indirection that makes the analysis harder to inspect.
- Keep code compact, but not cryptic.
- Avoid clever one-liners when two or three explicit lines are easier to audit.

## Loops and functions

- Prefer a plain `for` loop when iteration is conceptually simple and computational intensity is low or moderate.
- Preallocate a vector/data frame when convenient, then fill it by index.
- Do not replace a clear `for` loop with `purrr`, functional programming, metaprogramming, or a custom iterator merely for style.
- Create a custom function only when it is genuinely useful: substantial repetition, a natural reusable unit, simulation iterations that must be parallelized, or another clear practical reason.
- Do not wrap a five-line analysis in a function just to make it look modular.
- Keep functions local and task-specific rather than designing a general API unless requested.

## Comments

- Comment only at strategic points.
- Keep comments laconic and functional.
- Use comments to mark major stages, explain a non-obvious methodological choice, or warn about an important assumption.
- Do not narrate obvious syntax line by line.
- Section separators such as `####...` are acceptable when they make a long script easier to scan.

## Defensive programming and errors

Default to minimal defensive programming.

- Do not add routine type checks, schema validators, elaborate assertions, custom error classes, retries, logging systems, or `tryCatch()` wrappers to ordinary analysis scripts.
- Let ordinary code fail at the point of the problem; manual debugging is acceptable and often preferable.
- Do not silently suppress warnings merely to keep output clean.
- Use checks only when a realistic silent failure would be scientifically dangerous or unusually hard to diagnose.

Exception for expensive computation:

- If one rare failed iteration could waste hours of computation, use a minimal `tryCatch()` or equivalent around the risky iteration/model fit.
- Return `NA` or a small status field rather than building an elaborate recovery system.
- Save intermediate/checkpoint results when losing the run would be costly.

## Simulation style

For ordinary simulations:

- Make the data-generating mechanism visible in the main script.
- Set a seed when reproducibility matters.
- Declare key quantities explicitly near the top (`N`, `niter`, effect sizes, parameter grids).
- Prefer preallocated result objects and transparent loops.
- Print occasional progress/results if useful; do not add a logging framework.
- Keep the simulation and the summary code close together when feasible.

For computationally expensive simulations:

- Parallelize only when runtime savings are material.
- Prefer a simple, explicit parallel pattern such as base `parallel` with `makeCluster()` / `parLapply()` when suitable.
- Encapsulate a single simulation iteration in a function if required for parallel execution.
- Export only the objects actually needed by workers.
- Stop clusters explicitly.
- Preserve reproducible random-number generation when results depend on parallel RNG.
- Avoid complex orchestration frameworks unless the scale genuinely demands them.

## Data wrangling

- Prefer base R for straightforward filtering, indexing, recoding, merging, reshaping, summaries, and column creation.
- Use dedicated packages when they provide a clear substantive capability (`readxl`, `lavaan`, `lme4`, `psych`, `mclust`, etc.).
- Do not introduce `dplyr` merely to replace one or two clear base-R operations.
- Avoid long pipe chains. A short native pipe is acceptable when it clearly improves readability.
- Favor visible steps over a single highly compressed transformation expression.

## Plotting

- Use `ggplot2` by default in R.
- Build plots directly from a clearly prepared plotting data frame.
- Prefer readable, explicit layers over custom plotting wrappers.
- Create a helper for plotting only if many genuinely repetitive plots justify it.
- Save publication figures explicitly when requested, with dimensions/resolution stated near the save call.

## Self-contained analysis documents

Strongly prefer self-contained `.R`, `.Rmd`, or `.qmd` analysis files.

- Load required packages near the top.
- Read the required data directly.
- Define analysis parameters locally.
- Run the analysis and create/save outputs in the same file when practical.
- Avoid `source()` and hidden helper files unless avoiding them would make the project substantially more cumbersome.
- Accept duplicated small blocks across scripts if the alternative is a maze of dependencies.
- Use relative project paths; never introduce machine-specific absolute paths unless explicitly required.

If an expensive simulation should not rerun every time, it is fine to separate it from downstream analysis and save a simple `.RData`, `.rds`, or tabular result that later scripts read.

## Editing existing code

When Enrico provides existing code, modify as little as necessary.

- Preserve structure, variable names, package choices, ordering, and formatting unless they cause the problem or Enrico asks for cleanup.
- Fix the specific bug or conceptual issue rather than rewriting the script in your preferred style.
- Do not refactor working code into functions, classes, pipelines, or a new package ecosystem unless that is required.
- If a larger refactor would help, mention it separately rather than silently imposing it.

## Repository organization

Prefer shallow repositories with a few obvious locations rather than many nested folders.

A typical research repository may need only some of:

- root-level README / project files
- `R/` or `scripts/`
- `data/` when data can be included
- `outputs/`
- `figs/`
- `tables/`
- `paper/` or `manuscript/`

Rules:

- Do not create `src/`, `lib/`, `utils/`, `helpers/`, `config/`, `pipeline/`, `modules/`, etc. by habit.
- Add a folder only when it corresponds to a real, stable category of project material.
- Prefer one or two directory levels.
- For a genuinely sequential workflow, simple numeric filenames such as `01-...R`, `02-...R` are acceptable.
- Do not split a coherent analysis across many tiny files.

## Python fallback

When Python is actually appropriate, mirror the same philosophy:

- simple top-to-bottom scripts;
- explicit variables and loops;
- few helpers;
- no classes unless naturally required;
- minimal defensive programming;
- standard scientific packages only as needed (`numpy`, `pandas`, `scipy`, `statsmodels`, `sklearn`, `matplotlib`);
- no architecture for architecture's sake.

Do not translate R idioms into Python if the user did not ask for Python.

## Avoid by default

Avoid these unless there is a concrete reason:

- broad tidyverse dependency for ordinary analysis;
- `purrr` replacing simple loops;
- deep function hierarchies;
- object-oriented design for analysis scripts;
- configuration systems for a handful of constants;
- automatic validators everywhere;
- pervasive `tryCatch()`;
- custom logging;
- generalized plotting/data-processing wrappers;
- excessive DRY refactoring;
- package-like architecture for a one-paper repository;
- multiple helper files sourced into an analysis that could reasonably be self-contained.

## Calibration

The target is deliberately closer to **clear, slightly rough research code written by an empirically minded PhD student** than to polished production software. Code should be easy to inspect, alter manually, and debug at the exact line where it fails.

For substantial new R code or a refactor where style choices are ambiguous, consult `references/r-patterns.md` for concrete preferred and non-preferred patterns.
