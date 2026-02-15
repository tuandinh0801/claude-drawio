---
name: tam-replicate
description: Convert image to TAM notation
triggers:
  - tam replicate
  - convert to tam
---

# /tam-replicate

Convert existing architecture diagrams to TAM-compliant notation.

## Usage

```
/tam-replicate
[Upload image]
```

## Process

1. **Start Session** - `start_session`
2. **Analyze Image** - Identify visual elements
3. **Map to TAM** - Convert to TAM stencils
4. **Generate Diagram** - Create with official stencils
5. **Refine** - Adjust based on feedback

## Visual to TAM Mapping

| Visual Element | TAM Stencil |
|----------------|-------------|
| Rectangle (labeled service) | `agent` |
| Stick figure / Person | `human-agent` |
| Cylinder / Database | `storage` |
| Circle (message/event) | `channel` |
| Cloud shape | subsystem boundary |
| Arrow with label | `n-hor-arrow` or `z-vert-arrow` |
| Dashed box | module boundary |

## TAM Rules Applied

1. Direct agent-to-agent → Add channel between
2. Arrow TO database → Write access
3. Arrow FROM database → Read access
4. Bidirectional → Use `mod-access-*` stencils
