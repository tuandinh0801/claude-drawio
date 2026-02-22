# TAM Specification Format

YAML-based specification for TAM diagrams using exact shape names.

---

## Structure

```yaml
meta:
  diagramType: block    # block | activity | class | sequence
  title: System Name

nodes:
  - id: unique-id
    shape: BD-Agent     # Exact shape name from stencils
    label: Display Text
    x: 100              # X position (snap to 8px grid)
    y: 100              # Y position

edges:
  - from: source-id
    to: target-id
    shape: BD-InfoFlowArrow-Rect-N  # Optional: connector shape
    label: Connection Label
```

---

## Shape Names

### Block Diagram
| Shape | Purpose | Size |
|-------|---------|------|
| `BD-Agent` | Active component | 120x60 |
| `BD-HumanAgent` | Human participant | 60x60 |
| `BD-Storage` | Data storage | 120x60 |
| `BD-Channel` | Communication point | 20x20 |
| `BD-Channel-Rect-N` | Horizontal channel connector | 50x50 |
| `BD-Channel-Rect-Z` | Vertical channel connector | 50x50 |
| `BD-modAccessHor` | Horizontal modify access | 40x40 |
| `BD-modAccessVert` | Vertical modify access | 40x40 |
| `BD-InfoFlowArrow-Rect-N` | Horizontal arrow | 50x50 |
| `BD-InfoFlowArrow-Rect-Z` | Vertical arrow | 50x50 |
| `BD-Queue` | Queue/Buffer | 120x60 |

### Activity Diagram
| Shape | Purpose | Size |
|-------|---------|------|
| `AD-Action` | Activity step | 120x60 |
| `AD-StartOfActivity` | Start node | 20x20 |
| `AD-EndOfActivity` | End node | 30x30 |
| `AD-Decision` | Decision diamond | 20x20 |
| `AD-Fork` | Fork/Join bar | 120x10 |

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
    x: 100
    y: 200

  - id: webapp
    shape: BD-Agent
    label: Web App
    x: 300
    y: 200

  - id: db
    shape: BD-Storage
    label: Database
    x: 500
    y: 200

  - id: channel1
    shape: BD-Channel
    x: 200
    y: 215

edges:
  - from: user
    to: channel1
  - from: channel1
    to: webapp
  - from: webapp
    to: db
    shape: BD-InfoFlowArrow-Rect-N
```
