---
type: prompt
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - prompt/change-planning
---

# Change Planning Prompt

```text
You are helping plan a code change.

Use the provided project note, context pack, and relevant source snippets.
Return:
- the smallest safe implementation plan
- files likely to change
- tests to run
- risks and assumptions
- questions that block implementation

Prefer existing project patterns.
Do not propose unrelated refactors.
```

