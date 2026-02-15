# TAM Semantic Shapes

The TAM Design System maps semantic node types to FMC/UML compliant shapes.

---

## Core TAM Shapes (Block Diagram)

| Semantic Type | Shape | mxCell Style | Keywords |
|---------------|-------|--------------|----------|
| `agent` | Rectangle | `rounded=0;strokeWidth=2` | agent, service, process, component, handler |
| `human-agent` | Rectangle + Stick Figure | `shape=actor;rounded=0` | user, person, human, actor, operator |
| `storage` | Rounded Rectangle | `rounded=1;arcSize=60;strokeWidth=2` | storage, database, db, data, repository, cache |
| `channel` | Circle | `ellipse;aspect=fixed` | channel, queue, message, event, topic |
| `channel-request` | Circle + R Arrow | `ellipse;aspect=fixed` | request, http, api, rpc |
| `multiple` | Stacked Shape | `+offsetSize=8` | multiple, many, instances |
| `subsystem` | Rectangle (thin) | `rounded=0;strokeWidth=1;dashed=1` | subsystem, boundary, system |

---

## UML Shapes (Design Level)

| Semantic Type | Shape | mxCell Style | Keywords |
|---------------|-------|--------------|----------|
| `component` | Rectangle + Icon | `shape=component` | component |
| `interface-provided` | Lollipop | Circle on stick | provides, exposes |
| `interface-required` | Socket | Half circle | requires, depends |
| `package` | Folder | `shape=folder` | package, module, namespace |
| `class` | Rectangle 3-part | `swimlane;fontStyle=1` | class, entity, type |

---

## Behavioral Shapes

| Semantic Type | Shape | mxCell Style | Keywords |
|---------------|-------|--------------|----------|
| `use-case` | Ellipse | `ellipse` | use case, scenario, feature |
| `action` | Rounded Rectangle | `rounded=1;arcSize=20` | action, activity, step |
| `decision` | Diamond | `rhombus` | decision, condition, if, branch |
| `fork-join` | Bar | `line;strokeWidth=4` | fork, join, sync |
| `initial` | Filled Circle | `ellipse;fillColor=#000000` | start, begin, initial |
| `final` | Double Circle | `shape=doubleEllipse` | end, finish, final |
| `state` | Rounded Rectangle | `rounded=1` | state, status |

---

## Shape Styles by Theme

### SAP Blue (Default)

| Type | Fill | Stroke |
|------|------|--------|
| agent | `#FFFFFF` | `#0070F2` (SAP Blue) |
| human-agent | `#FFFFFF` | `#0070F2` |
| storage | `#E5F0FF` | `#0070F2` |
| channel | `#FFFFFF` | `#0070F2` |
| subsystem | `#F5F5F5` | `#666666` |

### SAP Grayscale (Print)

| Type | Fill | Stroke |
|------|------|--------|
| agent | `#FFFFFF` | `#000000` |
| human-agent | `#FFFFFF` | `#000000` |
| storage | `#E5E5E5` | `#000000` |
| channel | `#FFFFFF` | `#000000` |

---

## mxCell Style Reference

### Agent (Active Component)

```xml
<mxCell style="rounded=0;whiteSpace=wrap;html=1;
  fillColor=#FFFFFF;strokeColor=#0070F2;strokeWidth=2;
  fontColor=#1E1E1E;fontSize=12;fontFamily=72,Arial;" />
```

### Human Agent (with Stick Figure)

```xml
<!-- Container rectangle -->
<mxCell style="rounded=0;whiteSpace=wrap;html=1;verticalAlign=bottom;
  fillColor=#FFFFFF;strokeColor=#0070F2;strokeWidth=2;" />
<!-- Stick figure inside (positioned at top) -->
<mxCell style="shape=umlActor;verticalLabelPosition=bottom;
  fillColor=#0070F2;strokeColor=#0070F2;" />
```

### Storage (Passive Component)

```xml
<mxCell style="rounded=1;whiteSpace=wrap;html=1;arcSize=60;
  fillColor=#E5F0FF;strokeColor=#0070F2;strokeWidth=2;
  fontColor=#1E1E1E;fontSize=12;" />
```

### Channel (Communication)

```xml
<mxCell style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;
  fillColor=#FFFFFF;strokeColor=#0070F2;strokeWidth=2;
  fontColor=#1E1E1E;fontSize=10;" />
```

### Channel with Request Direction

```xml
<!-- Circle -->
<mxCell style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;
  fillColor=#FFFFFF;strokeColor=#0070F2;strokeWidth=2;" />
<!-- R label with arrow (separate cell) -->
<mxCell style="text;html=1;strokeColor=none;fillColor=none;
  fontSize=10;fontStyle=1;" value="R▶" />
```

### Multiple Agents (Stacked)

```xml
<mxCell style="rounded=0;whiteSpace=wrap;html=1;
  fillColor=#FFFFFF;strokeColor=#0070F2;strokeWidth=2;
  shadow=1;" />
<!-- Offset shadow creates stacked effect -->
```

---

## TAM-Specific Rules

1. **Agents cannot connect directly to agents** - must use channels
2. **Storages are passive** - cannot initiate actions
3. **Channels are volatile** - data does not persist
4. **Access arrows show data flow direction** - not control flow
5. **Request direction (R→) indicates who initiates** - response flows opposite
