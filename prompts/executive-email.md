# Executive Email Template

```json
{
  "version": "0.1",
  "id": "executive-email",
  "title": "Executive Email Builder",
  "locale": "mixed",
  "unit": "chat",
  "variables": [
    {"name": "recipient", "type": "string", "required": true, "hint": "e.g. CEO, Board, Client VP"},
    {"name": "subject", "type": "string", "required": true, "hint": "Email subject or topic"},
    {"name": "key_message", "type": "string", "required": true, "hint": "The one thing they must take away"},
    {"name": "context", "type": "string", "required": false, "hint": "Background info recipient needs"},
    {"name": "ask", "type": "string", "required": false, "hint": "What action or decision you need"}
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
    "task": "Draft an executive email to {{recipient}} about {{subject}}",
    "context": [
      {"label": "Recipient", "text": "{{recipient}}"},
      {"label": "Background", "text": "{{context}}"},
      {"label": "Key message", "text": "{{key_message}}"},
      {"label": "Ask", "text": "{{ask}}"}
    ],
    "audience": "{{recipient}}",
    "tone": "professional",
    "language": "en",
    "constraints": {
      "do": [
        "Lead with the key message or ask",
        "Keep it scannable (short paragraphs, bullets if needed)",
        "End with a clear call to action"
      ],
      "dont": [
        "Bury the lead",
        "Use jargon the recipient won't know",
        "Make it longer than necessary"
      ]
    },
    "output": {
      "format": "markdown",
      "sections": ["Subject line", "Email body"],
      "length": "short"
    },
    "quality_check": [
      "Can be read in under 2 minutes",
      "Action/decision needed is crystal clear"
    ]
  }
}
```
