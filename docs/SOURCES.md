# Sources & References (PromptSpec / Prompting Best Practices)

Primary/official-ish references used to shape PromptSpec v0 and the “Optimizer Instructions” concept:

## Anthropic
- Anthropic Claude docs — Prompt engineering (structure prompts, separate context/instructions, give clear output formats)
  - https://docs.anthropic.com/claude/docs/prompt-engineering
- Anthropic Claude docs — System prompts / messages (role separation concepts)
  - https://docs.anthropic.com/claude/docs

## OpenAI
- OpenAI Academy — Prompting resource (clear instructions, specify output, role/audience)
  - https://academy.openai.com/public/clubs/work-users-ynjqu/resources/prompting
- (Historical) OpenAI developer guide — Prompt engineering (URL sometimes changes; include for completeness)
  - https://platform.openai.com/docs/guides/prompt-engineering

## Google
- Google Cloud / Vertex AI learning materials — Prompt design patterns (clear instructions, examples, constraints)
  - https://cloud.google.com/vertex-ai
  - https://www.cloudskillsboost.google/paths/118/course_templates/976

## General prompting/agent patterns
- Role + task + context + constraints + output contract is a common pattern across major providers.
- Template variables are a pragmatic adaptation from prompt template libraries (e.g., LangChain-style templating), but PromptSpec remains provider-neutral.

Notes:
- Some provider docs move frequently; if any link 404s, we should pin a specific doc path/version and/or mirror key points into `docs/`.
