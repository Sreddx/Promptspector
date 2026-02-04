# /speckit.tasks

You are running the **Spec Kit / SDD** workflow.

## Goal
Break the plan into executable tasks with clear acceptance criteria.

## Inputs
- `.specify/memory/constitution.md`
- `specs/spec.md`
- `specs/plan.md`

## Output
Create `specs/tasks/` and write:
- `specs/tasks/000-overview.md` (phases)
- `specs/tasks/###-<task>.md` for each task

Each task must include:
- Summary
- Preconditions
- Steps
- Acceptance criteria
- Definition of done
