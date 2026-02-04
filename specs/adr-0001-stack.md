# ADR-0001: Choose Next.js fullstack + Supabase Auth (magic link) + Postgres

## Status
Proposed (for MVP)

## Context
We need a public web app with:
- email magic-link auth **without running our own SMTP**
- CRUD for prompts/templates
- JSON storage for PromptSpec
- i18n (EN/ES)
- deployable quickly

## Decision
Use:
- Next.js (TypeScript) fullstack
- Supabase Auth for magic links (uses managed email provider by default; custom SMTP optional later)
- Postgres (Supabase managed) with JSONB columns

## Consequences
### Positive
- Minimal moving parts
- No custom email infrastructure required for MVP
- Fast iteration on UI and API together

### Negative / Risks
- Vendor coupling to Supabase Auth (mitigatable by abstracting auth)
- Deliverability constraints on managed emails at scale (fixable with custom SMTP later)

## Alternatives Considered
- NextAuth + custom SMTP: more control, but requires email provider setup immediately.
- Clerk: excellent DX, but paid sooner for some usage levels.
- FastAPI backend + static frontend: more services and deployment complexity for MVP.
