# TAM Specification Format

YAML-based specification for TAM diagrams using exact shape names.

> **Note:** For construction rules and FMC patterns, see [SKILL.md](../../skills/tam/SKILL.md).

---

## Structure

```yaml
meta:
  diagramType: block    # block | activity | class | sequence
  title: System Name

modules:                 # Optional: containers for nesting
  - id: container-id
    label: System Boundary
    x: 100
    y: 100
    width: 400
    height: 300

nodes:
  - id: unique-id
    shape: BD-Agent      # Exact shape name
    label: Display Text
    x: 100               # X position (snap to 8px grid)
    y: 100               # Y position
    parent: container-id # Optional: for nesting inside module
    accessType: R        # Optional for channels: R | W | RW

edges:
  - from: source-id
    to: target-id
    type: write          # read | write | modify | channel
    protocol: SCIM2      # Optional: protocol label
```

---

## Shape Names

### Block Diagram
| Shape | Purpose | Size |
|-------|---------|------|
| `BD-Agent` | Active component | 120×60 |
| `BD-HumanAgent` | Human participant | 60×60 |
| `BD-Storage` | Data storage | 120×60 |
| `BD-Channel` | Communication port | 20×20 |
| `BD-Queue` | Queue/Buffer | 120×60 |

### Activity Diagram
| Shape | Purpose | Size |
|-------|---------|------|
| `AD-Action` | Activity step | 120×60 |
| `AD-StartOfActivity` | Start node | 20×20 |
| `AD-EndOfActivity` | End node | 30×30 |
| `AD-Decision` | Decision diamond | 40×40 |
| `AD-Fork` | Fork/Join bar | 120×10 |

---

## Field Reference

### Node Fields

| Field | Required | Description |
|-------|----------|-------------|
| `id` | Yes | Unique identifier |
| `shape` | Yes | Shape name (e.g., `BD-Agent`) |
| `label` | No | Display text |
| `x`, `y` | Yes | Position (8px grid) |
| `parent` | No | Parent module ID for nesting |
| `accessType` | No | For channels: `R`, `W`, or `RW` |

### Edge Fields

| Field | Required | Description |
|-------|----------|-------------|
| `from` | Yes | Source node ID |
| `to` | Yes | Target node ID |
| `type` | No | `read`, `write`, `modify`, `channel` |
| `protocol` | No | Protocol label (e.g., `SCIM2`) |

### Module Fields

| Field | Required | Description |
|-------|----------|-------------|
| `id` | Yes | Unique identifier |
| `label` | No | Container title |
| `x`, `y` | Yes | Position |
| `width`, `height` | Yes | Dimensions |

---

## Example: Simple Web App

```yaml
meta:
  diagramType: block
  title: Web Application

nodes:
  - id: user
    shape: BD-HumanAgent
    label: User
    x: 40
    y: 200

  - id: channel1
    shape: BD-Channel
    accessType: R
    x: 140
    y: 215

  - id: webapp
    shape: BD-Agent
    label: Web App
    x: 200
    y: 200

  - id: db
    shape: BD-Storage
    label: Database
    x: 400
    y: 200

edges:
  - from: user
    to: channel1
    type: channel

  - from: channel1
    to: webapp
    type: channel

  - from: webapp
    to: db
    type: modify
```

---

## Example: Nested System Boundary

```yaml
meta:
  diagramType: block
  title: SAP Cloud Identity Services

modules:
  - id: system
    label: SAP Cloud Identity Services
    x: 150
    y: 80
    width: 400
    height: 280

nodes:
  # External actor (outside boundary)
  - id: client
    shape: BD-HumanAgent
    label: Application Client
    x: 40
    y: 170

  # Agents inside system boundary
  - id: auth
    shape: BD-Agent
    label: Identity Authentication
    parent: system
    x: 40
    y: 60

  - id: directory
    shape: BD-Storage
    label: Identity Directory
    parent: system
    x: 200
    y: 60

  # Channel at boundary with read access
  - id: boundary-channel
    shape: BD-Channel
    accessType: R
    parent: system
    x: 380
    y: 80

edges:
  - from: auth
    to: directory
    type: read

  - from: boundary-channel
    to: auth
    type: channel

  - from: client
    to: boundary-channel
    protocol: Federation
    type: channel
```
