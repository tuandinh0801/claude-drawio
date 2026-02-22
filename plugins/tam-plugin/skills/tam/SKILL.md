---
name: tam
version: 3.0.0
description: SAP TAM diagram generation with inline shape styles
category: visual-design
tags: [tam, fmc, sap, architecture, block-diagram]
---

# TAM Skill

Generate TAM-compliant diagrams using **inline mxCell styles**. No external files needed - styles are documented directly.

## Core Shapes (Block Diagram)

### Shape Styles

| Shape | Style | Size |
|-------|-------|------|
| Agent | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;` | 120×60 |
| Storage | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` | 120×60 |
| Channel | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;rotatable=0;` | 20×20 |
| HumanAgent | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;` | 60×60 |

### Connector Styles

| Connector | Style |
|-----------|-------|
| Arrow (H) | `edgeStyle=elbowEdgeStyle;elbow=vertical;rounded=1;endArrow=classic;endFill=1;` |
| Arrow (V) | `edgeStyle=elbowEdgeStyle;elbow=horizontal;rounded=1;endArrow=classic;endFill=1;` |
| Line only | `endArrow=none;strokeWidth=2;` |

## How to Generate

Build mxGraphModel using documented styles:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0"/>
    <mxCell id="1" parent="0"/>
    <!-- Agent -->
    <mxCell id="2" value="Web Server" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;" vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="120" height="60" as="geometry"/>
    </mxCell>
    <!-- Storage -->
    <mxCell id="3" value="Database" style="rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;" vertex="1" parent="1">
      <mxGeometry x="200" y="250" width="120" height="60" as="geometry"/>
    </mxCell>
    <!-- Arrow from Agent to Storage -->
    <mxCell id="4" style="edgeStyle=elbowEdgeStyle;elbow=horizontal;rounded=1;endArrow=classic;endFill=1;" edge="1" parent="1" source="2" target="3">
      <mxGeometry relative="1" as="geometry"/>
    </mxCell>
  </root>
</mxGraphModel>
```

## TAM Rules

1. **Agents cannot connect directly** - put a Channel between them
2. **Storages are passive** - arrows point TO storage (write) or FROM storage (read)
3. **Use modify access** for bidirectional Agent↔Storage

## Element Mapping

| User Says | Shape | Style |
|-----------|-------|-------|
| user, customer, person | HumanAgent | `rounded=0;...verticalAlign=bottom;` |
| server, service, handler | Agent | `rounded=0;strokeWidth=2;` |
| database, storage, cache | Storage | `rounded=1;arcSize=40;` |
| API, channel, queue | Channel | `ellipse;aspect=fixed;` |

## MCP Tools

| Tool | When to Use |
|------|-------------|
| `start_session` | Opens browser preview |
| `create_new_diagram` | Create from XML |
| `edit_diagram` | Modify existing |
| `get_diagram` | Get current XML |
| `export_diagram` | Save to file |

## Documentation

- [Shape Styles](../../docs/design-system/shapes.md) - Complete style reference
- [Connectors](../../docs/design-system/connectors.md) - Connection patterns
- [Specification](../../docs/design-system/specification.md) - YAML format
