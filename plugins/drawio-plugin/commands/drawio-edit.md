---
description: Edit an existing Draw.io diagram with natural language instructions
---

# /drawio-edit

Edit existing diagrams with natural language modifications while preserving Design System consistency.

## Usage

```
/drawio-edit
Change "User Service" to "Auth Service"
Make database nodes green
```

## Edit Operations

### Modify Labels
```
/drawio-edit
Change "User Service" to "Auth Service"
Update the database label to include "PostgreSQL"
```

### Modify Styles
```
/drawio-edit
Make the API Gateway node use the accent color
Change all service nodes to database type
```

### Add Elements
```
/drawio-edit
Add a new "Cache" node (type: service) between API and Database
Add a data flow arrow from Order Service to Notification Service
```

### Delete Elements
```
/drawio-edit
Remove the legacy system node
Delete the connection between A and B
```

### Theme Switch
```
/drawio-edit
Switch to dark theme for presentation
Convert to academic theme for paper
```

## Procedure

1. **Identify Target** - Current session, file, or XML
2. **Get Current State** - Call get_diagram to see structure
3. **Parse Instructions** - Add, modify, delete, layout operations
4. **Apply Design System** - Preserve theme, semantic types
5. **Apply Changes** - Batch operations, real-time update
6. **Verify** - Review and iterate

## Reference Elements By

- **Label**: "the node labeled 'API Gateway'"
- **Position**: "the leftmost node"
- **Type**: "all database nodes"
- **Module**: "nodes in the Data module"

## Batch Operations

```
/drawio-edit
1. Change "Service A" to "User Service"
2. Change its type to database
3. Add a new "Cache" node (service type)
4. Connect Cache to Database with data flow
5. Apply academic theme
```

## Full Documentation

See [workflows/edit.md](workflows/edit.md) for complete workflow details.
