# Brief / PRD Template

```json
{
  "version": "0.1",
  "id": "brief",
  "title": "Brief / PRD Builder",
  "locale": "mixed",
  "unit": "chat",
  "variables": [
    {"name": "project_name", "type": "string", "required": true, "hint": "Name of the project or feature"},
    {"name": "problem", "type": "string", "required": true, "hint": "What problem are we solving?"},
    {"name": "target_users", "type": "string", "required": true, "hint": "Who is this for?"},
    {"name": "success_criteria", "type": "string", "required": false, "hint": "How do we know it worked?"},
    {"name": "constraints", "type": "string", "required": false, "hint": "Budget, timeline, tech constraints"}
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
    "task": "Write a product brief / PRD for {{project_name}}",
    "context": [
      {"label": "Problem", "text": "{{problem}}"},
      {"label": "Target users", "text": "{{target_users}}"},
      {"label": "Constraints", "text": "{{constraints}}"}
    ],
    "audience": "Product and engineering stakeholders",
    "tone": "professional",
    "language": "en",
    "constraints": {
      "do": [
        "Be specific about scope (in/out)",
        "Include measurable success criteria",
        "List assumptions and risks"
      ],
      "dont": [
        "Prescribe implementation details unless necessary",
        "Leave success criteria vague"
      ]
    },
    "output": {
      "format": "markdown",
      "sections": ["Executive summary", "Problem statement", "Goals", "Non-goals", "User stories", "Success criteria", "Risks", "Open questions"],
      "length": "medium"
    },
    "quality_check": [
      "A new team member can understand the why",
      "Success criteria are measurable"
    ]
  }
}
```
