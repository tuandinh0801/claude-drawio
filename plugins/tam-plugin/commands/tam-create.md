---
name: tam-create
description: Create TAM diagram using official stencils
triggers:
  - tam create
  - tam diagram
  - block diagram
---

# /tam-create

Create a TAM-compliant diagram using official SAP stencils.

## Usage

```
/tam-create [description]
```

## Process

1. **Start Session** - `start_session`
2. **Analyze Request** - Identify TAM elements
3. **Map to Stencils** - Use official TAM stencil IDs
4. **Generate XML** - Create mxGraphModel with stencil XML
5. **Create Diagram** - `create_new_diagram`

## Stencil Mapping

| User Says | TAM Stencil |
|-----------|-------------|
| user, customer, person | `human-agent` |
| server, service, handler | `agent` |
| database, storage, cache | `storage` |
| channel, api, http, queue | `n-hor-channel` or `z-vert-channel` |

## Example

```
/tam-create an e-commerce system with customers, web server, and product database
```

Maps to:
- Customer → `human-agent`
- Web Server → `agent`
- Product Database → `storage`
- HTTP connection → `n-hor-channel`
