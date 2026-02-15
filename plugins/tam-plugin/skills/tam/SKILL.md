---
name: tam
version: 2.0.0
description: SAP TAM (Technical Architecture Modeling) diagram generation using official TAM stencils
category: visual-design
tags: [tam, fmc, sap, architecture, block-diagram, uml]
---

# TAM Skill

AI-powered diagram generation using **official SAP TAM stencils**.

## Quick Start

| Command | Description |
|---------|-------------|
| `/tam-create` | Create TAM diagram from description |
| `/tam-replicate` | Convert image to TAM notation |
| `/tam-edit` | Modify existing TAM diagram |

## What is TAM?

TAM (Technical Architecture Modeling) is SAP's standardized notation combining:
- **FMC Block Diagrams** - Agents, Storages, Channels
- **UML 2.0** - Components, Classes, Sequences

## Official Stencils

This plugin uses **exact stencil definitions** from SAP's TAM library:

| Library | Shapes |
|---------|--------|
| TAM-BD | Agent, Storage, Channel, Human Agent, Arrows, Connectors |
| TAM-AD | Action, Start/End, Decision, Swimlane, Fork/Join |
| TAM-CD | Class, Association, Composition, Aggregation, Package |
| TAM-SeqD | Lifeline, Activation, Sync/Async Messages |
| TAM-Ann | Text, Note, Borders, Braces |

## Diagram Types

### Block Diagram (Primary)

| Element | Stencil | Purpose |
|---------|---------|---------|
| Active component | `agent` | Processes data |
| Human participant | `human-agent` | User interaction |
| Passive storage | `storage` | Data persistence |
| Communication | `n-hor-channel`, `z-vert-channel` | Agent-to-agent |
| Data flow | `n-hor-arrow`, `z-vert-arrow` | Direction indicator |
| Read/Write | `mod-access-hor`, `mod-access-vert` | Bidirectional access |

### Activity Diagram

| Element | Stencil | Purpose |
|---------|---------|---------|
| Action | `action` | Activity step |
| Start | `start-of-activity` | Initial node |
| End | `end-of-activity` | Final node |
| Decision | `decision-or-merge` | Branch/merge |
| Parallel | `fork-or-join` | Synchronization |

## Example

```yaml
meta:
  diagramType: block
  title: E-Commerce System

nodes:
  - id: customer
    stencil: human-agent
    label: Customer

  - id: webApp
    stencil: agent
    label: Web Application

  - id: productDB
    stencil: storage
    label: Product Catalog

  - id: httpChannel
    stencil: n-hor-channel

edges:
  - from: customer
    to: httpChannel
  - from: httpChannel
    to: webApp
  - from: webApp
    to: productDB
    stencil: z-vert-arrow
    label: Query
```

## TAM Rules (Enforced)

1. **Agents cannot connect directly** - use channels
2. **Storages are passive** - cannot initiate
3. **Use official stencils only** - no custom shapes

## MCP Tools

| Tool | Description |
|------|-------------|
| `start_session` | Opens browser preview |
| `create_new_diagram` | Create from XML |
| `edit_diagram` | Modify by cell ID |
| `get_diagram` | Get current XML |
| `export_diagram` | Save to file |

## Documentation

- [Shapes Reference](../../docs/design-system/shapes.md)
- [Connectors Reference](../../docs/design-system/connectors.md)
- [Specification Format](../../docs/design-system/specification.md)

## References

- [SAP TAM Standard](https://www.sap.com/documents/tam-standard.pdf)
- [FMC Modeling](https://www.fmc-modeling.org)
