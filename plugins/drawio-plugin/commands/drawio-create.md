---
description: Create a new Draw.io diagram from natural language description
---

# /drawio-create

Create diagrams from scratch using natural language descriptions with Design System support.

## Usage

```
/drawio-create a login flowchart with validation and error handling
/drawio-create --theme academic AWS serverless architecture
```

## Procedure

1. **Start Session** - Opens browser with draw.io editor
2. **Analyze Request** - Identify diagram type, entities, relationships
3. **Generate Specification** - Create YAML with nodes, edges, modules
4. **Convert to XML** - Apply theme tokens, calculate grid positions
5. **Create Diagram** - Diagram appears in browser
6. **Iterate** - Use /drawio-edit for modifications

## Theme Options

| Theme | Use Case | Flag |
|-------|----------|------|
| **tech-blue** (default) | Software architecture, DevOps | - |
| **academic-color** ⭐ | Academic papers, research (color) | `--theme academic-color` |
| **academic** | IEEE grayscale print only | `--theme academic` |
| **nature** | Environmental, lifecycle | `--theme nature` |
| **dark** | Presentations, slides | `--theme dark` |

## Node Types

Specify semantic types for automatic shape selection:

- `service` → Rounded rectangle (API, backend)
- `database` → Cylinder (DB, storage)
- `decision` → Diamond (if, check, condition)
- `terminal` → Stadium/Pill (start, end)
- `queue` → Parallelogram (queue, kafka)
- `user` → Circle (user, actor)
- `document` → Wave rect (doc, file)

## Examples

### Basic Flowchart
```
/drawio-create a login flowchart with:
- Start (terminal)
- Input credentials form
- Validation check (decision)
- Success → Dashboard
- Error → Back to login
```

### AWS Architecture
```
/drawio-create --theme tech-blue
AWS serverless architecture:
- API Gateway (service) as entry point
- Lambda (service) for business logic
- DynamoDB (database) for storage
```

### Academic Diagram
```
/drawio-create --theme academic
Neural network training pipeline with loss formula
```

## Full Documentation

See [workflows/create.md](workflows/create.md) for complete workflow details.
