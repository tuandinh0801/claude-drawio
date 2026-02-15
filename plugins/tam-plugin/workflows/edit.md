# TAM Edit Workflow

Detailed workflow for editing existing TAM diagrams.

---

## Overview

The `/tam-edit` command modifies existing TAM diagrams while preserving TAM semantics.

---

## Step 1: Get Current Diagram

```
get_diagram
```

Returns current mxGraphModel XML with all cell IDs.

---

## Step 2: Analyze Edit Request

| Edit Type | Examples |
|-----------|----------|
| **Add** | "Add a cache storage", "Add message queue" |
| **Rename** | "Change X to Y", "Rename the database" |
| **Delete** | "Remove the queue", "Delete the connection" |
| **Move** | "Move database below", "Reposition agents" |

---

## Step 3: Validate Against TAM Rules

Before applying edits:
1. Adding agent-to-agent access? → Reject, suggest channel
2. Adding storage write access? → Check direction (agent → storage)
3. Adding channel? → Ensure connects exactly 2 agents
4. Removing channel? → Warn about disconnected agents

---

## Step 4: Apply Edits

Use `edit_diagram` with operations:

```json
{
  "operations": [{
    "operation": "add",
    "cell_id": "10",
    "new_xml": "<mxCell ... stencil XML ...>"
  }]
}
```

---

## Step 5: Verify

Check browser preview for correctness.
