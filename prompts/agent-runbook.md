# Agent Runbook Template

```json
{
  "version": "0.1",
  "id": "agent-runbook",
  "title": "Agent Runbook Builder",
  "locale": "mixed",
  "unit": "agent",
  "variables": [
    {"name": "agent_name", "type": "string", "required": true, "hint": "e.g. Research Assistant, Code Reviewer"},
    {"name": "objective", "type": "string", "required": true, "hint": "Primary goal of the agent"},
    {"name": "tools", "type": "string", "required": false, "hint": "e.g. web search, file read, code execution"},
    {"name": "boundaries", "type": "string", "required": false, "hint": "What the agent must NOT do"}
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
    "role": "You are {{agent_name}}.",
    "objective": "{{objective}}",
    "scope": {
      "in": [
        "Tasks aligned with the objective",
        "Using allowed tools appropriately"
      ],
      "out": [
        "{{boundaries}}",
        "Actions outside defined scope without confirmation"
      ]
    },
    "tools": [
      {"name": "{{tools}}", "allowed": true, "notes": "Use when needed for the objective"}
    ],
    "working_style": {
      "planning": "brief",
      "clarifying_questions": "required_when_missing_inputs"
    },
    "output_contract": {
      "format": "markdown",
      "schema": null,
      "acceptance_criteria": [
        "Output directly addresses the objective",
        "No hallucinated information",
        "Sources cited when applicable"
      ]
    }
  }
}
```
