---
name: tam-edit
description: Edit existing TAM diagram
triggers:
  - tam edit
  - modify tam
---

# /tam-edit

Modify an existing TAM diagram while preserving TAM semantics.

## Usage

```
/tam-edit [instructions]
```

## Process

1. **Get Diagram** - `get_diagram` to fetch current XML
2. **Parse Instructions** - Identify add/update/delete operations
3. **Validate TAM Rules** - Ensure changes comply with TAM semantics
4. **Apply Edits** - `edit_diagram` with operations
5. **Verify** - Check browser preview

## Edit Operations

| Operation | Description |
|-----------|-------------|
| Add | Insert new stencil element |
| Update | Modify existing element's label/position |
| Delete | Remove element by ID |

## TAM Validation

Before applying edits:
- Adding agent-to-agent access? → Reject, suggest channel
- Adding storage write access? → Check direction (agent → storage)
- Removing channel? → Warn about disconnected agents
