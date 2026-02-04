# Presentation Template

```json
{
  "version": "0.1",
  "id": "presentation",
  "title": "Presentation Builder",
  "locale": "mixed",
  "unit": "chat",
  "variables": [
    {"name": "topic", "type": "string", "required": true, "hint": "What is the presentation about?"},
    {"name": "audience", "type": "string", "required": true, "hint": "e.g. C-suite, engineering team, investors"},
    {"name": "style", "type": "string", "required": false, "hint": "e.g. formal, casual, TED-style"},
    {"name": "duration", "type": "string", "required": false, "hint": "e.g. 10 minutes, 30 slides"},
    {"name": "key_points", "type": "string", "required": false, "hint": "Main points to cover"}
  ],
  "optimizer": {
    "enabled": true,
    "mode": "optimize_and_classify",
    "constraints": {
      "preserve_intent": true,
      "allow_semantic_changes": false
    }
  },
  "content": {
    "task": "Create an outline for a presentation on {{topic}}",
    "context": [
      {"label": "Topic", "text": "{{topic}}"},
      {"label": "Key points", "text": "{{key_points}}"}
    ],
    "audience": "{{audience}}",
    "tone": "{{style}}",
    "language": "en",
    "constraints": {
      "do": [
        "Structure with clear sections (intro, body, conclusion)",
        "Include speaker notes for each slide",
        "Suggest visuals or data points where appropriate"
      ],
      "dont": [
        "Make slides text-heavy",
        "Use jargon the audience won't understand"
      ]
    },
    "output": {
      "format": "markdown",
      "sections": ["Title slide", "Agenda", "Main sections", "Key takeaways", "Q&A"],
      "length": "medium"
    },
    "quality_check": [
      "Each slide has a single clear message",
      "Flow is logical for the audience"
    ]
  }
}
```
