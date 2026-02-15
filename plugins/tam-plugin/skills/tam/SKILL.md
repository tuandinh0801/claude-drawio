---
name: tam
version: 1.0.0
description: SAP TAM (Technical Architecture Modeling) diagram generation with FMC block diagrams and UML notation
category: visual-design
tags: [tam, fmc, sap, architecture, block-diagram, uml]
---

# TAM Skill

AI-powered diagram generation following SAP's TAM (Technical Architecture Modeling) standard.

## Quick Start

| What you want to do | Command | Description |
|---------------------|---------|-------------|
| Create block diagram | `/tam-create` | Natural language → TAM diagram |
| Replicate architecture | `/tam-replicate` | Image → TAM notation |
| Edit diagram | `/tam-edit` | Modify existing TAM diagram |

## What is TAM?

TAM (Technical Architecture Modeling) is SAP's standardized notation for technical architecture, combining:

- **FMC Block Diagrams** - Agents, Storages, Channels (conceptual level)
- **UML 2.0** - Components, Classes, Sequence diagrams (design level)

### TAM vs Generic Diagrams

| Aspect | Generic | TAM |
|--------|---------|-----|
| Shape semantics | Arbitrary | Agents (active) vs Storages (passive) |
| Connections | Any to any | Agents ↔ Storages via Access, Agents ↔ Agents via Channels |
| Data flow | Undefined | Read/Write/Modify with direction |
| Request/Response | Not shown | Explicit R→ on channels |

## Core TAM Elements

### Block Diagram (Conceptual Level)

| Element | Shape | Purpose |
|---------|-------|---------|
| **Agent** | Rectangle | Active component (processes data) |
| **Human Agent** | Rectangle + Stick Figure | Human participant |
| **Storage** | Rounded Rectangle | Passive data holder |
| **Channel** | Circle | Communication between agents |
| **Read Access** | Arrow → | Agent reads from storage |
| **Write Access** | Arrow → | Agent writes to storage |
| **Modify Access** | Curved arrows ↔ | Agent reads AND writes |

### Design Level Elements

| Element | Shape | Purpose |
|---------|-------|---------|
| Component | Rectangle + icon | Implementation unit |
| Interface | Lollipop/Socket | Provided/Required API |
| Class | 3-part rectangle | Data structure |
| Package | Folder | Namespace grouping |

## Themes

| Theme | Use Case |
|-------|----------|
| **SAP Blue** | SAP technical documentation (default) |
| **SAP Grayscale** | Print-ready documents |
| **TAM Classic** | FMC notation style |

## TAM Rules (Enforced)

1. **Agents cannot directly connect to agents** - use channels
2. **Storages are passive** - cannot initiate actions
3. **Access arrows show data flow** - not control flow
4. **Request direction (R→) indicates initiator**
5. **Channels are volatile** - data does not persist

## Installation

Uses same MCP server as drawio-plugin:

```json
{
  "mcpServers": {
    "drawio": {
      "command": "npx",
      "args": ["--yes", "@next-ai-drawio/mcp-server@latest"]
    }
  }
}
```

## MCP Tools

| Tool | Description |
|------|-------------|
| `start_session` | Opens browser with real-time preview |
| `create_new_diagram` | Create diagram from XML |
| `edit_diagram` | Edit by ID-based operations |
| `get_diagram` | Get current diagram XML |
| `export_diagram` | Save to `.drawio` file |

## Workflows

### `/tam-create` - Create TAM Diagram

```
/tam-create a web application with frontend, backend, and database
```

Generates TAM-compliant block diagram with proper agent/storage/channel semantics.

### `/tam-replicate` - Replicate Architecture

```
/tam-replicate
[Upload architecture diagram image]
```

Extracts TAM elements and recreates with proper notation.

### `/tam-edit` - Modify Diagram

```
/tam-edit
Add a cache storage between API and Database
```

## Example Specification

```yaml
meta:
  theme: sap-blue
  diagramType: block
  level: conceptual
  title: Online Shop Architecture

agents:
  - id: webBrowser
    label: Web Browser
    type: human-agent

  - id: webServer
    label: Web Server
    type: agent

  - id: orderProcessor
    label: Order Processor
    type: agent
    multiple: true

storages:
  - id: productDB
    label: Product Catalog
  - id: orderDB
    label: Orders

channels:
  - id: httpChannel
    label: HTTP
    type: channel-request
    requestDirection: east
    between: [webBrowser, webServer]

accesses:
  - from: webServer
    to: productDB
    type: read
    label: Query Products

  - from: orderProcessor
    to: orderDB
    type: modify
    label: Process Orders
```

## Documentation

| Topic | File |
|-------|------|
| TAM Shapes | [docs/design-system/shapes.md](../../docs/design-system/shapes.md) |
| TAM Connectors | [docs/design-system/connectors.md](../../docs/design-system/connectors.md) |
| Specification Format | [docs/design-system/specification.md](../../docs/design-system/specification.md) |

## References

- [SAP TAM Standard](https://www.sap.com)
- [FMC Modeling](https://www.fmc-modeling.org)
- [TAM Draw.io Plugin](https://github.com/ariel-bentu/tam-drawio)

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Agent-to-agent access" error | Use a channel between agents |
| "Storage cannot write" error | Storages are passive; reverse the access |
| Missing R→ on channel | Set `type: channel-request` with `requestDirection` |

## License

- **License**: MIT
- **Author**: Tuan Dinh
- **Version**: 1.0.0
