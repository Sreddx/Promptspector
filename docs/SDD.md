# SDD — PromptForge (MVP)

## 1. Overview
PromptForge is a public web application that helps non-technical users build high-quality prompts by filling a friendly form. The system compiles a structured **PromptSpec** into a **raw prompt** (Markdown) and a **machine-readable spec** (JSON).

The exported raw prompt includes a standard **OPTIMIZER INSTRUCTIONS** block intended to be pasted into an external LLM that will validate, classify, and optimize the prompt before final execution.

## 2. Goals
- Non-tech-first UX for building prompts that follow best practices.
- Output is **copy/paste-ready** and consistently structured.
- Templates with **variables** to reduce repetitive work.
- Multi-language: **English + Spanish** (UI + template metadata; content can be either).
- User accounts to save personal prompts/templates.
- Seed a **public template marketplace**.

## 3. Non-Goals (MVP)
- Running prompts against models (no execution runner).
- Built-in AI optimization / validation (external only).
- Prompt evaluation harness / automated tests of prompts.
- Fine-grained versioning of prompts (store latest state only).

## 4. Target Users
- Primary: PMs, analysts, operators, and other non-technical users.
- Secondary: developers who want an “advanced mode” (JSON editing) later.

## 5. Core Concepts
### 5.1 PromptSpec
A structured representation of a prompt. Stored as JSON and rendered to Markdown.

### 5.2 Raw Prompt
A Markdown document with labeled sections:
- OPTIMIZER INSTRUCTIONS (standardized)
- PROMPT SPEC (human-readable)
- EXECUTION PROMPT (the actual prompt to paste into the final model/chat)

### 5.3 Templates
Templates are PromptSpecs with:
- prefilled fields
- declared variables (e.g. `{{audience}}`)
- UI hints and examples

## 6. Product Scope (MVP Screens)
1. **Landing**: value prop, browse public templates.
2. **Template Gallery**: filter by use case and language; “Use template”.
3. **Prompt Builder Wizard**:
   - select unit type (Chat Prompt / Conversation / Agent Spec)
   - fill guided fields
   - live preview (Markdown)
   - export/copy
   - save (private)
4. **My Library**:
   - saved prompts
   - saved templates
   - duplicate/edit
5. **Template Publish (basic)**:
   - submit template to public gallery (v0 can be “publish immediately” or “pending review”).

## 7. Architecture (MVP Recommendation)
### 7.1 Stack
- **Next.js (TypeScript)** fullstack
- DB: **Postgres** (Supabase or Neon)
- ORM: Prisma
- Auth: **Email magic link** via Supabase Auth (no custom SMTP required for MVP)
- Hosting: Vercel (web) + Supabase/Neon (DB)

Rationale: minimum moving parts for a public CRUD app with auth, i18n, and JSON storage.

### 7.2 High-level Components
- UI
  - Wizard + Preview
  - Gallery + Library
  - i18n layer
- API
  - CRUD prompts/templates
  - publish template
  - export endpoints (optional; can be client-only)
- PromptSpec renderer
  - `PromptSpec -> Markdown`
  - `PromptSpec -> JSON`

## 8. Data Model (logical)
### Entities
- **User**
  - id, email
- **Prompt** (private)
  - id, userId
  - title
  - spec (JSONB)
  - renderedMarkdown (optional cache)
  - updatedAt
- **Template**
  - id, ownerUserId (nullable for system templates)
  - visibility: `public | private`
  - status: `published | pending | rejected`
  - useCase: `presentation | brief | agent_runbook | exec_email | other`
  - language: `en | es | mixed`
  - variables: string[]
  - spec (JSONB)
  - createdAt, updatedAt

## 9. PromptSpec (MVP shape)
See `docs/PROMPTSPEC.md`.

## 10. Internationalization
- UI strings: standard i18n (next-intl or similar)
- Template metadata supports EN/ES
- Prompt content can be EN/ES per template

## 11. Security & Abuse
- Rate limit template publishing
- Basic content policy + report button (v1)
- Prevent leaking secrets: UI copy warns users not to paste credentials

## 12. Open Questions
- Moderation workflow for public templates (manual vs community reporting).
- Whether to cache rendered Markdown or render on demand.
- How strict variable syntax should be (`{{var}}` vs JSONPath-like).
