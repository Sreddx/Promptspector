# PromptSpec v0 (MVP)

This spec is designed to:
- map cleanly to a non-technical form UI
- compile to a consistent Markdown “raw prompt”
- support multiple “units” (chat / conversation / agent)
- support template variables

## 1) Top-level
```json
{
  "version": "0.1",
  "id": "uuid-or-slug",
  "title": "string",
  "locale": "en|es|mixed",
  "unit": "chat|conversation|agent",
  "variables": [
    {"name": "audience", "type": "string", "required": false, "hint": "e.g. CFO"}
  ],
  "optimizer": {
    "enabled": true,
    "mode": "optimize_and_classify",
    "constraints": {
      "preserve_intent": true,
      "allow_semantic_changes": false
    }
  },
  "content": {"... unit-specific ..."}
}
```

## 2) Unit: chat
```json
{
  "unit": "chat",
  "content": {
    "task": "What the user wants",
    "context": [
      {"label": "Background", "text": "..."}
    ],
    "audience": "{{audience}}",
    "tone": "professional|friendly|direct|...",
    "language": "en|es",
    "constraints": {
      "do": ["..."],
      "dont": ["..."]
    },
    "output": {
      "format": "markdown|json|bullets|table|mixed",
      "schema": "optional JSON schema or pseudo-schema",
      "sections": ["Executive summary", "Details", "Next steps"],
      "length": "short|medium|long"
    },
    "quality_check": [
      "Ask clarifying questions if inputs are missing",
      "Avoid hallucinating sources"
    ]
  }
}
```

## 3) Unit: conversation
```json
{
  "unit": "conversation",
  "content": {
    "system": "System message",
    "examples": [
      {
        "input": "Example user input",
        "output": "Ideal assistant output"
      }
    ],
    "user": "Actual user request (may include variables)"
  }
}
```

## 4) Unit: agent (light)
```json
{
  "unit": "agent",
  "content": {
    "role": "You are an expert ...",
    "objective": "Primary goal",
    "scope": {
      "in": ["what the agent should do"],
      "out": ["what it must not do"]
    },
    "tools": [
      {"name": "browser", "allowed": true, "notes": "Only when needed"}
    ],
    "working_style": {
      "planning": "brief",
      "clarifying_questions": "required_when_missing_inputs"
    },
    "output_contract": {
      "format": "markdown|json",
      "schema": "optional schema",
      "acceptance_criteria": ["..."]
    }
  }
}
```

## 5) Raw Prompt Rendering (Markdown)
MVP rendering should output sections in this order:

1. `# OPTIMIZER INSTRUCTIONS`
   - classify use case + unit
   - normalize structure
   - tighten constraints & output contract
   - ensure variables are preserved
   - forbid adding new requirements unless explicitly asked

2. `# PROMPT SPEC`
   - readable representation of the PromptSpec

3. `# EXECUTION PROMPT`
   - the final prompt text to paste into the execution model

## 6) Variable Rules (MVP)
- Variable token: `{{var_name}}`
- Names: `[a-zA-Z_][a-zA-Z0-9_]*`
- Renderer must not expand variables; it only preserves them.
