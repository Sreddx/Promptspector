# Constitution — Promptspector

Non‑negotiable principles for this project. These guide all specs, plans, and implementation.

## Product principles
1. **Non‑technical first**: the default UI must be usable without prompting knowledge.
2. **Structured by default**: everything is a PromptSpec first; “raw prompt text” is a rendered artifact.
3. **Copy/paste ready**: exports must be immediately usable in external LLMs.
4. **Bilingual**: English + Spanish are first‑class.

## Engineering principles
5. **Minimal infra for MVP**: avoid running our own mail server; prefer managed magic-link auth.
6. **Security & privacy**: default user prompts are private; public templates are explicitly published.
7. **No model execution in MVP**: the app does not run prompts; it only builds/exports them.
8. **Explicit contracts**: every template must define output format/contract (even if simple).

## Marketplace principles
9. **Abuse-aware**: rate-limit publishing and provide reporting hooks early.
10. **Provider-neutral**: PromptSpec must not hard-code a single LLM provider format.
