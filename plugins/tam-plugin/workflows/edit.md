# TAM Edit Workflow

Detailed workflow for editing existing TAM diagrams.

---

## Overview

The `/tam-edit` command modifies existing TAM diagrams while preserving TAM semantics and validation rules.

---

## Step 1: Get Current Diagram

Retrieve the current diagram state:

```
get_diagram
```

This returns the current mxGraphModel XML with all cell IDs.

---

## Step 2: Analyze Edit Request

Parse the user's edit instructions:

| Edit Type | Examples |
|-----------|----------|
| **Add** | "Add a cache storage", "Add message queue" |
| **Rename** | "Change X to Y", "Rename the database" |
| **Delete** | "Remove the queue", "Delete the connection" |
| **Restyle** | "Make it grayscale", "Use SAP Blue theme" |
| **Move** | "Move database below", "Reposition agents" |

---

## Step 3: Validate Against TAM Rules

Before applying edits, validate:

1. **Adding agent-to-agent access?** → Reject, suggest channel
2. **Adding storage write access?** → Check direction (agent → storage)
3. **Adding channel?** → Ensure connects exactly 2 agents
4. **Removing channel?** → Warn about disconnected agents

---

## Step 4: Apply Edits

Use the `edit_diagram` MCP tool with operations:

### Add Operation

```json
{
  "operations": [{
    "operation": "add",
    "cell_id": "10",
    "new_xml": "<mxCell id=\"10\" value=\"Cache\" style=\"rounded=1;arcSize=60;...\" vertex=\"1\" parent=\"1\"><mxGeometry x=\"300\" y=\"200\" width=\"120\" height=\"60\" as=\"geometry\"/></mxCell>"
  }]
}
```

### Update Operation

```json
{
  "operations": [{
    "operation": "update",
    "cell_id": "3",
    "new_xml": "<mxCell id=\"3\" value=\"New Label\" style=\"...\" vertex=\"1\" parent=\"1\"><mxGeometry x=\"100\" y=\"100\" width=\"120\" height=\"60\" as=\"geometry\"/></mxCell>"
  }]
}
```

### Delete Operation

```json
{
  "operations": [{
    "operation": "delete",
    "cell_id": "5"
  }]
}
```

---

## Step 5: Verify Changes

After editing:
1. Check browser preview for visual correctness
2. Verify TAM rules are maintained
3. Confirm with user

---

## Common Edit Patterns

### Add Storage Between Agent and Database

1. Get current positions
2. Add new storage at midpoint
3. Update existing access to point to new storage
4. Add new access from storage to original target

### Convert to Different Theme

1. Get all cells
2. Update style attributes for each cell type:
   - Agent: `strokeColor`, `fillColor`
   - Storage: `strokeColor`, `fillColor`
   - Channel: `strokeColor`, `fillColor`
   - Connectors: `strokeColor`

### Add Channel Between Agents

1. Calculate position between two agents
2. Add channel circle
3. Add connector lines from each agent to channel
4. Add request direction if needed

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Edit not appearing | Call `get_diagram` first to sync state |
| Wrong element edited | Verify cell_id from get_diagram output |
| Style not changing | Include complete style string, not partial |
| Position wrong | Use 8px grid-aligned coordinates |
