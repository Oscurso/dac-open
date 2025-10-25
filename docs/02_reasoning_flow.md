# Reasoning Flow in DAC

## Overview

Every DAC reasoning cycle generates a structured JSON representation called `reasoning.json`.  
This file captures *how* a system arrived at its conclusion — not just *what* it concluded.

---

## Example Flow

```json
{
  "input": "Create a blog system",
  "steps": [
    {"reason": "Detect domain concept", "output": "Blog"},
    {"reason": "Identify components", "output": ["Post", "Comment", "User"]},
    {"reason": "Map deterministic relationships", "output": "post_user_relation.sql"}
  ],
  "result": "Reasoning complete."
}
````

---

## Structure of a Reasoning JSON

| Field    | Description                            |
| -------- | -------------------------------------- |
| `input`  | The initial instruction or question    |
| `steps`  | Sequential reasoning units             |
| `reason` | The logic or rule applied              |
| `output` | The generated result or transformation |
| `result` | Final state of reasoning process       |

---

## Visual Flow (Conceptual)

```
Input → Step 1 (Reason) → Step 2 (Rule) → Step 3 (Decision) → Output → Result
```

---

## Determinism Guarantee

Each step is reproducible:

> Same input → Same reasoning → Same output.

That’s the DAC promise.
