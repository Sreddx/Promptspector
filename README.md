# PromptForge (working title)

Public, non-technical-first **prompt builder** that generates a **raw prompt** (Markdown/JSON) from a friendly form, with a built-in **Optimizer Instructions** block designed to be pasted into an external LLM for validation/optimization.

## MVP (v0)
- Web app (TypeScript, Next.js)
- Email magic-link login (no custom SMTP required)
- Create prompts from templates (presentation, brief, agent runbook, executive email)
- Variables in templates (e.g. `{{audience}}`, `{{style}}`)
- Export: Markdown + JSON
- Save latest state (no versioning)
- Public templates marketplace (curated/light moderation later)

## Docs
See `docs/`.
