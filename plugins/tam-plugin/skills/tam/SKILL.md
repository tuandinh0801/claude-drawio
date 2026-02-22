---
name: tam
version: 3.1.0
description: SAP TAM diagram generation using FMC methodology
category: visual-design
tags: [tam, fmc, sap, architecture, block-diagram]
---

# TAM Skill

Generate TAM-compliant diagrams using **FMC (Fundamental Modeling Concepts)** methodology with inline mxCell styles.

---

## FMC Fundamentals

### Bipartite Graph Structure

TAM/FMC uses a **bipartite graph** - the most fundamental rule:

| Type | Shape | Graphical | Examples |
|------|-------|-----------|----------|
| **Active** | Angular | Rectangle | Agent, Human Agent |
| **Passive** | Rounded | Circle/Rounded rect | Storage, Channel, Queue |

**RULE:** Active shapes connect ONLY to passive shapes. Never direct Agent → Agent.

```
CORRECT:                         WRONG:
Agent ─── Channel ─── Agent      Agent ─────── Agent
Agent ─── Storage                (direct connection forbidden)
```

### Component Reference

| Component | Type | Style | Size | Purpose |
|-----------|------|-------|------|---------|
| Agent | Active | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;` | 120×60 | Processes/transforms data |
| Human Agent | Active | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;` | 60×60 | Human participant |
| Storage | Passive | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` | 120×60 | Persists data |
| Channel | Passive | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;` | 20×20 | Communication port |
| Queue | Passive | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` | 120×60 | Message buffer |

### Access Types (Arrow Direction)

Arrow direction indicates **data flow direction**:

| Access | Arrow | Meaning |
|--------|-------|---------|
| Read | Storage → Agent | Agent reads from storage |
| Write | Agent → Storage | Agent writes to storage |
| Modify | ↔ (bidirectional) | Agent reads AND writes |
| Channel | No arrow | Communication link |

**Key insight:** Arrow points in direction of data flow, not request direction.

---

## Construction Patterns

### Pattern 1: Channel as Access Port

Channels are **access points** positioned at agent boundaries:

```
┌─────────────────┐
│     Agent       │
│            ┌───┐│
│            │ R ││◄─── External connection
│            └───┘│
└─────────────────┘
```

**XML Example - Read Access Channel:**
```xml
<!-- Agent at x=100, width=120, so right edge is x=220 -->
<mxCell id="2" value="Server" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry"/>
</mxCell>

<!-- Channel at right edge (x=210, centered on edge) with "R" label -->
<mxCell id="3" value="R" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;fontSize=10;" vertex="1" parent="1">
  <mxGeometry x="210" y="120" width="20" height="20" as="geometry"/>
</mxCell>
```

**Channel Labels:**
- `R` = Read access (external can read)
- `W` = Write access (external can write)
- Empty = Bidirectional access

### Pattern 2: Agent-to-Agent Communication

Agents NEVER connect directly. Always use a channel:

```
┌──────────┐     ┌───┐     ┌──────────┐
│  Client  │─────│   │─────│  Server  │
└──────────┘     └───┘     └──────────┘
                Channel
```

**XML Example:**
```xml
<!-- Client Agent -->
<mxCell id="2" value="Client" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry"/>
</mxCell>

<!-- Channel between agents -->
<mxCell id="3" value="" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="250" y="120" width="20" height="20" as="geometry"/>
</mxCell>

<!-- Server Agent -->
<mxCell id="4" value="Server" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="300" y="100" width="120" height="60" as="geometry"/>
</mxCell>

<!-- Edge: Client to Channel -->
<mxCell id="5" style="endArrow=none;strokeWidth=2;" edge="1" parent="1" source="2" target="3">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>

<!-- Edge: Channel to Server -->
<mxCell id="6" style="endArrow=none;strokeWidth=2;" edge="1" parent="1" source="3" target="4">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

### Pattern 3: Storage Access

**Read Access (Storage → Agent):**
```xml
<mxCell id="5" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="storage" target="agent">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

**Write Access (Agent → Storage):**
```xml
<mxCell id="5" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="agent" target="storage">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

**Modify Access (Bidirectional):**
```xml
<mxCell id="5" style="endArrow=classic;startArrow=classic;strokeWidth=2;" edge="1" parent="1" source="agent" target="storage">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

### Pattern 4: Request-Response (APIs)

For HTTP/API patterns, use labeled edges:

```
┌──────────┐  [SCIM2]  ┌───┐     ┌──────────┐
│  Client  │──────────►│ R │────►│  Server  │
└──────────┘           └───┘     └──────────┘
```

**XML Example with Protocol Label:**
```xml
<mxCell id="5" value="SCIM2" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="2" target="3">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

---

## Layout Guidelines

### System Boundary (Containment)

Use swimlane container for system scope:

```
┌─────────────────────────────────────────────┐
│  SAP Cloud Identity Services                │
│  ┌────────────┐         ┌────────────┐     │
│  │  Identity  │───○─────│  Identity  │     │
│  │   Auth     │         │  Directory │     │
│  └────────────┘         └────────────┘     │
│        │                                    │
│     ┌──┴──┐                                │
│     │  R  │◄─────────────────────────────────── External
│     └─────┘                                 │
└─────────────────────────────────────────────┘
```

**XML Example - Nested Container:**
```xml
<!-- System boundary container -->
<mxCell id="2" value="SAP Cloud Identity Services"
        style="swimlane;horizontal=1;startSize=30;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="400" height="300" as="geometry"/>
</mxCell>

<!-- Agent inside system (parent="2") - coordinates relative to container -->
<mxCell id="3" value="Identity Auth" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;"
        vertex="1" parent="2">
  <mxGeometry x="40" y="50" width="120" height="60" as="geometry"/>
</mxCell>

<!-- Channel at container boundary for external access -->
<mxCell id="4" value="R" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;fontSize=10;"
        vertex="1" parent="2">
  <mxGeometry x="380" y="140" width="20" height="20" as="geometry"/>
</mxCell>
```

### External Actor Placement

Human actors positioned **OUTSIDE** system boundary:

```
       ┌──────────────────────────────┐
┌────┐ │  ┌──────┐       ┌──────────┐ │
│User│─┼──│  R   │──────►│  Server  │ │
└────┘ │  └──────┘       └──────────┘ │
       └──────────────────────────────┘
```

**XML Example:**
```xml
<!-- Human actor outside boundary -->
<mxCell id="5" value="User" style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;"
        vertex="1" parent="1">
  <mxGeometry x="20" y="200" width="60" height="60" as="geometry"/>
</mxCell>

<!-- Connect to channel at system boundary -->
<mxCell id="6" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="5" target="4">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

### FMC Visualization Best Practices

1. **Layout:**
   - Minimize edge crossings
   - Use horizontal/vertical edges (avoid diagonals)
   - Keep edges neither too short nor too long

2. **Positioning:**
   - System-of-interest at center
   - Environment components at periphery
   - External actors outside boundary

3. **Grouping:**
   - Group related agents together
   - Use consistent spacing (8px grid)
   - Apply rounded corners to edges for visual tracking

4. **Clarity:**
   - Use consistent font sizes
   - Place labels horizontally
   - Ensure adequate whitespace

---

## Complete Example

**SAP Cloud Identity Services Architecture:**

```xml
<mxGraphModel>
  <root>
    <mxCell id="0"/>
    <mxCell id="1" parent="0"/>

    <!-- System Boundary -->
    <mxCell id="2" value="SAP Cloud Identity Services"
            style="swimlane;horizontal=1;startSize=30;strokeWidth=2;fillColor=#f5f5f5;"
            vertex="1" parent="1">
      <mxGeometry x="150" y="80" width="450" height="280" as="geometry"/>
    </mxCell>

    <!-- Identity Authentication (Agent) -->
    <mxCell id="3" value="Identity&#xa;Authentication"
            style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;"
            vertex="1" parent="2">
      <mxGeometry x="40" y="60" width="120" height="60" as="geometry"/>
    </mxCell>

    <!-- Identity Directory (Storage) -->
    <mxCell id="4" value="Identity&#xa;Directory"
            style="rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;"
            vertex="1" parent="2">
      <mxGeometry x="200" y="60" width="120" height="60" as="geometry"/>
    </mxCell>

    <!-- Identity Provisioning (Agent) -->
    <mxCell id="5" value="Identity&#xa;Provisioning"
            style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;"
            vertex="1" parent="2">
      <mxGeometry x="200" y="180" width="120" height="60" as="geometry"/>
    </mxCell>

    <!-- Read Channel at boundary (for external read access) -->
    <mxCell id="6" value="R"
            style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;fontSize=10;"
            vertex="1" parent="2">
      <mxGeometry x="420" y="80" width="20" height="20" as="geometry"/>
    </mxCell>

    <!-- Auth to Directory (read) -->
    <mxCell id="7" style="endArrow=classic;strokeWidth=2;" edge="1" parent="2" source="3" target="4">
      <mxGeometry relative="1" as="geometry"/>
    </mxCell>

    <!-- Provisioning to Directory (modify) -->
    <mxCell id="8" style="endArrow=classic;startArrow=classic;strokeWidth=2;" edge="1" parent="2" source="5" target="4">
      <mxGeometry relative="1" as="geometry"/>
    </mxCell>

    <!-- Channel to Auth connection -->
    <mxCell id="9" style="endArrow=none;strokeWidth=2;" edge="1" parent="2" source="6" target="3">
      <mxGeometry relative="1" as="geometry"/>
    </mxCell>

    <!-- External: Human Actor (outside boundary) -->
    <mxCell id="10" value="Application&#xa;Client"
            style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;"
            vertex="1" parent="1">
      <mxGeometry x="40" y="170" width="60" height="60" as="geometry"/>
    </mxCell>

    <!-- External: SAP BTP (Agent) -->
    <mxCell id="11" value="SAP BTP"
            style="rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;"
            vertex="1" parent="1">
      <mxGeometry x="650" y="120" width="100" height="50" as="geometry"/>
    </mxCell>

    <!-- External connection: Client to Channel (with protocol label) -->
    <mxCell id="12" value="Federation" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="10" target="6">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="100" y="200"/>
          <mxPoint x="560" y="200"/>
        </Array>
      </mxGeometry>
    </mxCell>

    <!-- External connection: SAP BTP to Channel -->
    <mxCell id="13" value="SCIM2" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="11" target="6">
      <mxGeometry relative="1" as="geometry"/>
    </mxCell>
  </root>
</mxGraphModel>
```

---

## Quick Reference

### Shape Styles

| Shape | Style |
|-------|-------|
| Agent | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;` |
| Storage | `rounded=1;whiteSpace=wrap;html=1;strokeWidth=2;arcSize=40;` |
| Channel | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;strokeWidth=2;` |
| Human | `rounded=0;whiteSpace=wrap;html=1;strokeWidth=2;verticalAlign=bottom;` |
| Container | `swimlane;horizontal=1;startSize=30;strokeWidth=2;` |

### Edge Styles

| Connection | Style |
|------------|-------|
| Read | `endArrow=classic;strokeWidth=2;` (from storage) |
| Write | `endArrow=classic;strokeWidth=2;` (to storage) |
| Modify | `endArrow=classic;startArrow=classic;strokeWidth=2;` |
| Channel link | `endArrow=none;strokeWidth=2;` |

### Construction Checklist

1. [ ] Bipartite structure: Agents only connect to passive elements
2. [ ] Agent-to-agent: Always via channel (never direct)
3. [ ] Channels at boundaries: Position at agent/container edges
4. [ ] R/W labels: Add to channels showing access type
5. [ ] Arrow direction: Points in data flow direction
6. [ ] System boundary: Container for scope
7. [ ] External actors: Position outside boundary
8. [ ] Protocol labels: On edges for API connections

## MCP Tools

| Tool | When to Use |
|------|-------------|
| `start_session` | Opens browser preview |
| `create_new_diagram` | Create from XML |
| `edit_diagram` | Modify existing |
| `get_diagram` | Get current XML |
| `export_diagram` | Save to file |
