---
name: tam-replicate
description: Replicate an image as a TAM diagram
triggers:
  - tam replicate
  - replicate tam
  - convert to tam
  - tam from image
---

# /tam-replicate

Replicate an existing architecture diagram/image as a TAM-compliant diagram.

## Usage

```
/tam-replicate
[Upload image]
```

## Examples

```
/tam-replicate
[Upload architecture diagram screenshot]

/tam-replicate
【领域】软件架构
[Upload system design image]
```

## Process

1. **Start Session** - Call `start_session` to open browser
2. **Analyze Image** - Extract components, connections, and relationships
3. **Map to TAM** - Convert elements to TAM notation:
   - Services/Components → Agents
   - Databases/Caches → Storages
   - APIs/Queues → Channels
   - Arrows → Accesses (read/write/modify)
4. **Apply TAM Rules** - Validate and fix any violations
5. **Generate Diagram** - Create TAM-compliant Draw.io diagram
6. **Iterate** - Refine based on feedback

## TAM Mapping

| Original Element | TAM Element |
|-----------------|-------------|
| Box/Rectangle (active) | Agent |
| Person icon | Human Agent |
| Cylinder/Database | Storage |
| Circle/Queue | Channel |
| Arrow (data flow) | Access |

## Output

TAM-compliant block diagram that faithfully represents the original while following SAP's TAM standard notation.
