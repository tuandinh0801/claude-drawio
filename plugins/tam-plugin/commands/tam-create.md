---
name: tam-create
description: Create TAM diagram from natural language
triggers:
  - tam create
  - tam diagram
  - block diagram
  - architecture diagram
  - fmc diagram
---

# /tam-create

Create a TAM-compliant diagram from natural language description.

## Usage

```
/tam-create [description]
```

## Examples

```
/tam-create a microservices architecture with API gateway, user service, and PostgreSQL database

/tam-create an online shop with customers, web server, order processor, and product catalog
```

## Process

1. **Start Session** - Call `start_session` to open browser
2. **Analyze Request** - Extract TAM elements (agents, storages, channels)
3. **Apply TAM Rules** - Validate agent↔storage↔channel relationships
4. **Generate XML** - Create Draw.io compatible mxGraphModel
5. **Create Diagram** - Call `create_new_diagram`
6. **Iterate** - Refine based on feedback

## TAM Element Detection

| User Says | TAM Element |
|-----------|-------------|
| "user", "customer", "operator" | Human Agent |
| "server", "service", "processor" | Agent |
| "database", "storage", "cache" | Storage |
| "API", "HTTP", "message queue" | Channel |

## Output

TAM-compliant block diagram with:
- Rectangular agents (active components)
- Rounded storages (passive components)
- Circular channels (communication)
- Directional access arrows (data flow)

## TAM Rules Applied

- Agents cannot connect directly to agents (use channels)
- Storages are passive (cannot initiate)
- Access arrows show data flow direction
- Request direction (R→) indicates initiator
