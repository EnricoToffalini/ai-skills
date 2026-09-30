---
name: long-horizon-work
description: Manage genuinely long-horizon repository, research, or development work that must be decomposed, resumed, or advanced across substantial stages, especially when the next step depends on what is learned during execution. Use when a project already has roadmap/work-packet machinery, when the user explicitly asks for sustained autonomous progress, or when the work clearly requires multiple coherent work units across sessions. Do not use for ordinary coding tasks, local fixes, well-scoped analyses, or merely because many files are involved. Never introduce persistent roadmap, worklog, agent-state, or other AI/project-management artifacts into a project without an existing convention or explicit user approval.
---

# Long-Horizon Work

Manage long work by controlling **scope, continuation, checkpoints, and stopping conditions**, not by maximizing how much work an agent does in one run.

## 1. Triage before planning

Classify the task into one of three regimes.

### A. Ordinary bounded task

Use when the requested outcome is clear and can be completed coherently in one working session, even if several files are involved.

- Work directly.
- Use an internal plan if useful.
- Validate the result.
- Do **not** create persistent planning or agent-state files.

### B. Substantial but session-bounded task

Use when the task needs several dependent steps but still has a clear endpoint that can reasonably be reached in one session.

- Inspect relevant project context first.
- Plan internally, then execute through implementation, validation, repair, and final review.
- Do not stop merely because the initial plan is complete; re-check the original goal.
- Do **not** create persistent planning artifacts unless the user explicitly asks for them.

### C. Genuine long-horizon work

Use only when at least one strong signal is present:

- the project already contains an explicit roadmap, work queue, work packets, execution plan, or equivalent;
- the user explicitly asks for sustained autonomous work, a roadmap with continuation, or work across multiple substantial stages;
- the goal is clearly too large for one coherent session and later steps depend on results or decisions from earlier ones;
- multiple agents or future sessions must be able to resume from a stable project state;
- the work contains natural review gates where evidence from one stage determines the next stage.

Do not infer regime C merely from repository size, number of files, novelty of the project, or the fact that the task is difficult.

## 2. Preserve project conventions first

Before inventing any long-horizon machinery, inspect the project for existing instructions and state, including likely files such as:

- `AGENTS.md`, `CLAUDE.md`, or equivalent agent instructions;
- `ROADMAP*`, `PLAN*`, `TODO*`, issue/backlog files;
- work-packet, milestone, decision-record, or status files;
- repository-specific contribution and testing instructions.

If such machinery exists:

1. treat it as authoritative unless the user says otherwise;
2. continue from its current state instead of creating a parallel system;
3. preserve its vocabulary, states, granularity, and review gates;
4. update only the artifacts that its workflow requires.

For a vague instruction such as "continue" or "proceed", use the existing project queue or roadmap when it unambiguously defines the next eligible work unit.


### Adopt the project's operating model

Once genuine long-horizon machinery is recognized, adapt to it rather than merely consulting it episodically. Internalize and preserve the project's:

- terminology for states, milestones, packets, gates, and priorities;
- rules for selecting the next eligible work unit;
- update cadence and required state transitions;
- validation and completion criteria;
- boundaries between autonomous work and human review.

Use that operating model consistently for the rest of the run. On later resumptions, reconstruct it from the project's persistent instructions/state before selecting new work. Do not silently replace it with a generic agent workflow.

## 3. Gate persistent artifacts

Persistent planning/state files are a project-level intervention. Do not create them casually.

If the project has no existing convention:

- create no roadmap, worklog, agent-state directory, task ledger, or similar file for regimes A or B;
- for regime C, obtain explicit user approval before introducing persistent planning/state artifacts;
- if there is genuine doubt about whether regime C applies, ask the user rather than leaving new AI-oriented artifacts in the repository;
- if asking is not possible, default to **no persistent artifacts** and keep planning internal.

When the user approves persistent state:

- prefer one minimal, human-readable structure over an elaborate agent framework;
- follow any requested location and version-control policy;
- avoid names that unnecessarily advertise AI provenance (`AI_WORKLOG`, `.agent-state`, etc.) unless the user explicitly wants them;
- store only information useful to humans and future sessions: goal, current state, dependencies, decisions, acceptance criteria, and next eligible work.

## 4. Work in coherent units

Long-horizon does not mean "do everything possible until context or time runs out."

Define a **work unit** that has:

- one primary outcome;
- explicit prerequisites;
- an observable completion condition;
- relevant validation/tests;
- a known relationship to the next unit.

Prefer one autonomous run to produce one coherent, verifiable advance when later work depends on review of the current result.

A good work unit may be a prototype, one analysis stage, one migration slice, one subcomponent, one audit, or one integration step. Avoid units such as "finish the whole project" when intermediate evidence can change the plan.

## 5. Use evidence-driven continuation

Within an authorized work unit:

1. inspect the current state and preserve unfinished user/agent work;
2. identify prerequisites and constraints;
3. execute the smallest coherent path to the unit's outcome;
4. validate with the strongest practical evidence available;
5. repair failures introduced or exposed by the work;
6. re-evaluate the original unit goal, not merely the checklist;
7. stop only when the unit's completion condition is satisfied or a genuine block/review gate is reached.

If new necessary work is discovered and it is clearly inside the same unit, incorporate it. If it changes scope materially, record or report it as a separate next unit instead of silently expanding the task.

## 6. Distinguish autonomous continuation from human gates

Continue autonomously through mechanical or logically implied steps that do not materially change the project's direction.

Stop at a human gate when the next action depends on a substantive judgment that should not be smuggled in as implementation, for example:

- choosing among materially different designs;
- approving a prototype before large-scale expansion;
- changing scientific assumptions, constructs, scoring, inclusion criteria, or other consequential specifications;
- making a difficult-to-reverse architectural choice not already authorized;
- deciding whether uncertain output quality is acceptable.

A human gate is a valid completion condition for a work unit. Do not treat it as failure to finish.

## 7. Definition of done

For every non-trivial unit, derive a concrete definition of done from the task and repository conventions. Normally require that:

- the requested substantive outcome exists;
- relevant tests/checks pass or any failure is explained;
- dependent artifacts that are clearly in scope are updated;
- no required TODO remains hidden behind a nominally completed checklist;
- the final diff/output has been reviewed for accidental or unnecessary changes;
- uncertainties and blocks are stated explicitly rather than guessed away.

Do not stop after producing a roadmap unless the user asked only for a roadmap.

## 8. Re-orient to the big picture periodically

In genuine long-horizon work, do not let local progress obscure the overall project state. Produce a concise big-picture recap **occasionally**, not mechanically after every unit.

A recap is especially useful:

- after a meaningful milestone or several completed work units;
- when a result changes priorities, dependencies, or the roadmap;
- before switching to a different workstream;
- when reaching a human review gate;
- when resuming after a substantial interruption or when the current position may be unclear.

The recap should answer, briefly:

- What is the overall goal?
- What major parts are now complete?
- Where are we now in the larger plan?
- What remains, including important blockers or review gates?
- What is the next most sensible work unit or small set of candidate units?
- Does the current roadmap still make sense, or should it be revised?

Prefer a short synthesis in the agent's progress/final report. Update persistent project state only when the project's existing workflow calls for it. Do not create a new recap file merely to satisfy this rule, and do not turn recaps into verbose project diaries.

## 9. Keep state concise

If persistent project state is already authorized or already exists, update it so that a fresh capable agent can answer:

- What is the project trying to achieve?
- What has been completed?
- What is currently in progress or blocked?
- What evidence/tests support the current state?
- What is the next eligible work unit, and what prerequisites or review gates apply?

Do not turn the state file into a transcript or verbose diary. Detailed historical changes belong in normal version control, changelogs, or decision records when the project uses them.

## 10. Examples

**Use this skill:** a repository has `AGENTS.md`, a strategic roadmap, and a queue of `ready / blocked / review_gate / done` work packets; the user says "continue with the project." Follow that machinery and complete the next eligible unit.

**Use this skill:** the user asks to build a substantial new research/software project from scratch over multiple stages and wants agents to be able to resume it. Before adding roadmap/state files, confirm that persistent project artifacts are desired.

**Do not use this skill:** "fix this R script and update the corresponding paragraph in the paper." Plan internally if needed, make the coherent change, validate it, and finish without creating roadmap/worklog files.

**Do not use this skill:** "refactor these ten functions and run the tests." File count alone does not make the work long-horizon.

## 11. Interaction with coding/style skills

This skill governs **how far to work, how to checkpoint, and when to stop**. It does not define coding style, scientific methodology, or domain conventions.

When another applicable skill or repository instruction defines those matters, compose with it rather than overriding it.
