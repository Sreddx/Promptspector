# Promptspector

Public, non‑technical‑first **prompt builder** that generates a **raw prompt** (Markdown/JSON) from a friendly form, with a built‑in **Optimizer Instructions** block designed to be pasted into an external LLM for validation/optimization.

## MVP (v0)
- Web app (TypeScript, Next.js)
- Email magic-link login (no custom SMTP required)
- Templates: presentation, brief, agent runbook, executive email
- Variables in templates (e.g. `{{audience}}`, `{{style}}`)
- Export: Markdown + JSON
- Save latest state (no versioning)
- Public templates marketplace (curated/light moderation later)

## Repository Structure

```
.specify/                      # Spec Kit SDD primitives
  memory/
    constitution.md            # Non-negotiable project principles
    constitution_update_checklist.md
  templates/                   # SDD document templates
    spec-template.md
    plan-template.md
    tasks-template.md

specs/                         # Feature-scoped SDD artifacts
  0001-mvp-core/
    spec.md                    # Product specification
    plan.md                    # Technical plan (TBD)
    tasks.md                   # Implementation tasks (TBD)
  adr-*.md                     # Architecture Decision Records

prd/                           # PRD research inputs
  PROMPTSPEC.md                # PromptSpec v0 schema
  SOURCES.md                   # References for prompting best practices

prompts/                       # Product prompt templates
  presentation.md
  brief.md
  agent-runbook.md
  executive-email.md
```

## Branching Strategy
- `main` — production / releases
- `dev` — integration
- `feature/<slug>` — new features (from `dev`)
- `fix/<slug>` — bug fixes (from `dev`)
- `chore/<slug>` — scaffolding, docs, config

PRs target `dev`; `dev → main` for releases.
