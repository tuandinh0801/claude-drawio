---
name: tam-edit
description: Edit an existing TAM diagram
triggers:
  - tam edit
  - edit tam
  - modify tam diagram
---

# /tam-edit

Edit an existing TAM diagram with natural language instructions.

## Usage

```
/tam-edit [instructions]
```

## Examples

```
/tam-edit Add a cache storage between API and Database

/tam-edit Change "User Service" to "Auth Service"

/tam-edit Add a message queue channel between Order Processor and Notification Service
```

## Process

1. **Get Current Diagram** - Call `get_diagram` to retrieve XML
2. **Analyze Request** - Understand what changes are needed
3. **Apply TAM Rules** - Validate changes follow TAM semantics
4. **Edit Diagram** - Call `edit_diagram` with operations
5. **Verify** - Confirm changes in browser preview

## Supported Operations

| Operation | Description |
|-----------|-------------|
| Add agent | Add new active component |
| Add storage | Add new passive data holder |
| Add channel | Add communication between agents |
| Add access | Add read/write/modify arrow |
| Rename | Change label of existing element |
| Delete | Remove element from diagram |
| Move | Reposition element |
| Restyle | Change colors/theme |

## TAM Validation

All edits are validated against TAM rules:
- No direct agent-to-agent connections
- Storages cannot have outgoing writes
- Channels connect exactly 2 agents
