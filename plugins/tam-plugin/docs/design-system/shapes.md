# TAM Shape Styles

This document provides the **exact mxCell style strings** for each TAM shape. Use these styles directly when building mxGraphModel XML.

---

## How to Use

Generate XML using documented style + dimensions:

```xml
<mxCell id="2" value="Label" style="[STYLE_STRING]" vertex="1" parent="1">
  <mxGeometry x="[X]" y="[Y]" width="[W]" height="[H]" as="geometry"/>
</mxCell>
```

---

## Block Diagram Shapes

### BD-Agent (Active Component)
| Property | Value |
|----------|-------|
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

### BD-Channel (Communication Point)
| Property | Value |
|----------|-------|
| **Style** | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;rotatable=0;` |
| **Width** | 20 |
| **Height** | 20 |
| **Purpose** | Small circle indicating agent-to-agent communication |

**Example:**
```xml
<mxCell id="4" value="" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;rotatable=0;" vertex="1" parent="1">
  <mxGeometry x="160" y="120" width="20" height="20" as="geometry"/>
</mxCell>
```

### BD-HumanAgent (Human Participant)
| Property | Value |
|----------|-------|
| **Container Style** | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;rotatable=0;verticalAlign=bottom;align=center;` |
| **Width** | 60 |
| **Height** | 60 |
| **Purpose** | Human user interacting with system |

**Note:** Contains stick figure as child group. See BD-HumanAgent.xml in official repo for full structure.

### BD-Queue (Queue/Buffer)
| Property | Value |
|----------|-------|
| **Style** | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` |
| **Width** | 120 |
| **Height** | 60 |
| **Purpose** | Message queue or buffer (same style as Storage, label differentiates) |

---

## Connector Shapes

### BD-InfoFlowArrow-Rect-N (Horizontal Arrow)
| Property | Value |
|----------|-------|
| **Style** | `edgeStyle=elbowEdgeStyle;elbow=vertical;rounded=1;endArrow=classic;html=1;endFill=1;` |
| **Type** | Edge (not vertex) |
| **Purpose** | Unidirectional data flow (horizontal) |

**Example:**
```xml
<mxCell id="5" value="" style="edgeStyle=elbowEdgeStyle;elbow=vertical;rounded=1;endArrow=classic;html=1;endFill=1;" edge="1" parent="1" source="2" target="3">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

### BD-InfoFlowArrow-Rect-Z (Vertical Arrow)
| Property | Value |
|----------|-------|
| **Style** | `edgeStyle=elbowEdgeStyle;elbow=horizontal;rounded=1;endArrow=classic;html=1;endFill=1;` |
| **Type** | Edge |
| **Purpose** | Unidirectional data flow (vertical) |

### BD-modAccessHor (Horizontal Modify Access)
| Property | Value |
|----------|-------|
| **Style** | Curved bidirectional arrows (group with two edges) |
| **Width** | 40 |
| **Height** | 40 |
| **Purpose** | Bidirectional read/write access |

**Note:** Complex shape - see BD-modAccessHor.xml for full structure.

### BD-modAccessVert (Vertical Modify Access)
| Property | Value |
|----------|-------|
| **Width** | 40 |
| **Height** | 40 |
| **Purpose** | Vertical version of modify access |

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

| Shape | Style | W × H |
|-------|-------|-------|
| BD-Agent | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;` | 120×60 |
| BD-Storage | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` | 120×60 |
| BD-Channel | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;rotatable=0;` | 20×20 |
| BD-HumanAgent | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;rotatable=0;verticalAlign=bottom;` | 60×60 |
| AD-Action | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=20;` | 120×60 |
| AD-Decision | `rhombus;whiteSpace=wrap;html=1;strokeWidth=2;` | 40×40 |
| AD-Fork | `rounded=0;whiteSpace=wrap;html=1;fillColor=#000000;strokeWidth=0;` | 120×10 |
