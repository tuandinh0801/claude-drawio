# TAM Shape Styles

This document provides the **exact mxCell style strings** for each TAM shape. Use these styles directly when building mxGraphModel XML.

> **Note:** For construction rules and patterns, see [SKILL.md](../../skills/tam/SKILL.md).

---

## FMC Classification

TAM follows FMC's **bipartite graph** structure:

| Classification | Graphical | Examples |
|----------------|-----------|----------|
| **Active** (Angular) | Rectangle | Agent, Human Agent |
| **Passive** (Rounded) | Circle/Rounded rect | Storage, Channel, Queue |

**Rule:** Active shapes connect ONLY to passive shapes.

---

## Block Diagram Shapes

### BD-Agent (Active Component)

| Property | Value |
|----------|-------|
| **Classification** | Active (Angular) |
| **Style** | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;` |
| **Width** | 120 |
| **Height** | 60 |
| **Purpose** | Software component that processes/transforms data |

**Example:**
```xml
<mxCell id="2" value="Web Server" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry"/>
</mxCell>
```

### BD-Storage (Passive Storage)

| Property | Value |
|----------|-------|
| **Classification** | Passive (Rounded) |
| **Style** | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` |
| **Width** | 120 |
| **Height** | 60 |
| **Purpose** | Data storage that holds information persistently |

**Example:**
```xml
<mxCell id="3" value="Database" style="rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;" vertex="1" parent="1">
  <mxGeometry x="100" y="200" width="120" height="60" as="geometry"/>
</mxCell>
```

### BD-Channel (Communication Port)

| Property | Value |
|----------|-------|
| **Classification** | Passive (Rounded) |
| **Style** | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;` |
| **Width** | 20 |
| **Height** | 20 |
| **Purpose** | Access point at agent boundary for communication |

**Placement:** Position at agent boundary edge. Add `value="R"` for read, `value="W"` for write.

**Example - Read Access Channel:**
```xml
<mxCell id="4" value="R" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;fontSize=10;" vertex="1" parent="1">
  <mxGeometry x="210" y="120" width="20" height="20" as="geometry"/>
</mxCell>
```

### BD-HumanAgent (Human Participant)

| Property | Value |
|----------|-------|
| **Classification** | Active (Angular) |
| **Style** | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;` |
| **Width** | 60 |
| **Height** | 60 |
| **Purpose** | Human user interacting with system |

**Placement:** Position OUTSIDE system boundary when representing external users.

**Example:**
```xml
<mxCell id="5" value="User" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="20" y="200" width="60" height="60" as="geometry"/>
</mxCell>
```

### BD-Queue (Queue/Buffer)

| Property | Value |
|----------|-------|
| **Classification** | Passive (Rounded) |
| **Style** | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` |
| **Width** | 120 |
| **Height** | 60 |
| **Purpose** | Message queue or buffer (same style as Storage, label differentiates) |

### System Boundary (Container)

| Property | Value |
|----------|-------|
| **Style** | `swimlane;horizontal=1;startSize=30;strokeWidth=2;` |
| **Width** | Variable |
| **Height** | Variable |
| **Purpose** | Container for system scope, groups related agents |

**Example:**
```xml
<mxCell id="2" value="System Name" style="swimlane;horizontal=1;startSize=30;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="400" height="300" as="geometry"/>
</mxCell>
```

---

## Connector Shapes

### BD-InfoFlowArrow-Rect-N (Horizontal Arrow)

| Property | Value |
|----------|-------|
| **Style** | `endArrow=classic;strokeWidth=2;` |
| **Type** | Edge (not vertex) |
| **Purpose** | Unidirectional data flow |

**Example:**
```xml
<mxCell id="5" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="2" target="3">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

### BD-modAccess (Bidirectional)

| Property | Value |
|----------|-------|
| **Style** | `endArrow=classic;startArrow=classic;strokeWidth=2;` |
| **Type** | Edge |
| **Purpose** | Bidirectional read/write access |

---

## Activity Diagram Shapes

### AD-Action (Activity Step)

| Property | Value |
|----------|-------|
| **Style** | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=20;` |
| **Width** | 120 |
| **Height** | 60 |

### AD-StartOfActivity (Start Node)

| Property | Value |
|----------|-------|
| **Style** | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#000000;strokeWidth=2;` |
| **Width** | 20 |
| **Height** | 20 |

### AD-EndOfActivity (End Node)

| Property | Value |
|----------|-------|
| **Style** | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;` |
| **Width** | 30 |
| **Height** | 30 |
| **Note** | Contains inner filled circle |

### AD-Decision (Decision Diamond)

| Property | Value |
|----------|-------|
| **Style** | `rhombus;whiteSpace=wrap;html=1;strokeWidth=2;` |
| **Width** | 40 |
| **Height** | 40 |

### AD-Fork (Fork/Join Bar)

| Property | Value |
|----------|-------|
| **Style** | `rounded=0;whiteSpace=wrap;html=1;fillColor=#000000;strokeWidth=0;` |
| **Width** | 120 |
| **Height** | 10 |

---

## Quick Reference Table

| Shape | Classification | Style | W × H |
|-------|---------------|-------|-------|
| BD-Agent | Active | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;` | 120×60 |
| BD-Storage | Passive | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` | 120×60 |
| BD-Channel | Passive | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;` | 20×20 |
| BD-HumanAgent | Active | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;` | 60×60 |
| Container | - | `swimlane;horizontal=1;startSize=30;strokeWidth=2;` | Variable |
| AD-Action | - | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=20;` | 120×60 |
| AD-Decision | - | `rhombus;whiteSpace=wrap;html=1;strokeWidth=2;` | 40×40 |
| AD-Fork | - | `rounded=0;whiteSpace=wrap;html=1;fillColor=#000000;strokeWidth=0;` | 120×10 |
