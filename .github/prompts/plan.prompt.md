# /speckit.plan

You are running the **Spec Kit / SDD** workflow.

## Goal
Produce the **HOW**: a technical implementation plan grounded in the constitution.

## Inputs
- Read `.specify/memory/constitution.md`.
- Read `specs/spec.md`.

## Output
Create/update `specs/plan.md` with:
- Architecture overview
- Data model
- Key components
- Auth approach (magic link, no custom SMTP for MVP)
- Internationalization approach (EN/ES)
- Milestones
- Risks / trade-offs

Also create ADRs in `specs/adr-*.md` when decisions are made.
