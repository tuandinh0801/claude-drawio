# TAM Connectors

TAM defines specific connector types for different relationships in technical architecture.

---

## Access Types (Agent ↔ Storage)

### Read Access

**Purpose**: Agent retrieves data from storage (non-destructive)

| Property | Value |
|----------|-------|
| Line | Solid, 1.5px |
| Arrow | Filled at agent end |
| Direction | Storage → Agent |
| Color | `#1E1E1E` (dark gray) |

```yaml
edges:
  - from: userStorage
    to: authAgent
    type: read
```

```xml
<mxCell style="endArrow=block;endFill=1;strokeWidth=1.5;
  strokeColor=#1E1E1E;exitX=0.5;exitY=0;entryX=0.5;entryY=1;" />
```

---

### Write Access

**Purpose**: Agent stores data (overwrites entire content)

| Property | Value |
|----------|-------|
| Line | Solid, 1.5px |
| Arrow | Filled at storage end |
| Direction | Agent → Storage |
| Color | `#1E1E1E` |

```yaml
edges:
  - from: orderAgent
    to: orderStorage
    type: write
```

```xml
<mxCell style="endArrow=block;endFill=1;strokeWidth=1.5;
  strokeColor=#1E1E1E;" />
```

---

### Modify Access

**Purpose**: Agent reads AND writes (selective changes)

| Property | Value |
|----------|-------|
| Line | Two curved lines |
| Arrows | One each direction |
| Color | `#1E1E1E` |

```yaml
edges:
  - from: updateAgent
    to: dataStorage
    type: modify
```

```xml
<!-- Two curved arrows forming a loop -->
<mxCell style="edgeStyle=orthogonalEdgeStyle;curved=1;
  endArrow=block;endFill=1;strokeWidth=1.5;strokeColor=#1E1E1E;" />
<mxCell style="edgeStyle=orthogonalEdgeStyle;curved=1;
  endArrow=block;endFill=1;strokeWidth=1.5;strokeColor=#1E1E1E;" />
```

---

## Channel Types (Agent ↔ Agent via Channel)

### Simple Channel

**Purpose**: Bidirectional communication, no request/response semantics

| Property | Value |
|----------|-------|
| Line | Solid, 1.5px |
| Arrow | None |
| Color | `#1E1E1E` |

```yaml
edges:
  - from: agent1
    to: channel1
    type: channel
  - from: channel1
    to: agent2
    type: channel
```

---

### Request/Response Channel

**Purpose**: One agent requests, other responds (e.g., HTTP)

| Property | Value |
|----------|-------|
| Request | R with filled triangle |
| Response | Implied opposite direction |
| Circle | Contains "R" with arrow |

```yaml
edges:
  - from: clientAgent
    to: httpChannel
    type: request
    direction: east  # R→ points east
  - from: httpChannel
    to: serverAgent
    type: response
```

**Request Direction Values:**
- `north` - R▲ (request goes up)
- `south` - R▼ (request goes down)
- `east` - R▶ (request goes right)
- `west` - R◀ (request goes left)

---

### Data Flow Channel

**Purpose**: Show direction of data (not request)

| Property | Value |
|----------|-------|
| Line | Solid, 1.5px |
| Arrow | At data destination |
| Color | `#1E1E1E` |

```yaml
edges:
  - from: producerAgent
    to: messageChannel
    type: dataflow
    direction: east
```

---

## UML Connector Types (Design Level)

### Assembly Connector

**Purpose**: Connect provided to required interface

```xml
<mxCell style="endArrow=none;startArrow=none;
  strokeWidth=1;strokeColor=#1E1E1E;" />
```

### Delegation Connector

**Purpose**: Forward from port to internal component

```xml
<mxCell style="endArrow=open;dashed=1;
  strokeWidth=1;strokeColor=#666666;" />
```

### Dependency

**Purpose**: UML dependency relationship

```xml
<mxCell style="endArrow=open;dashed=1;
  strokeWidth=1;strokeColor=#666666;" />
```

---

## Protocol Boundary

**Purpose**: Separate regions by protocol/interface

| Property | Value |
|----------|-------|
| Line | Dashed, 1px |
| Label | Protocol name |
| Color | `#666666` |

```yaml
boundaries:
  - label: HTTP
    position: horizontal
    y: 200
```

```xml
<mxCell style="line;strokeWidth=1;dashed=1;
  strokeColor=#666666;labelPosition=right;
  verticalLabelPosition=middle;" value="HTTP" />
```

---

## Best Practices

### TAM Rules

1. **Access arrows point in data flow direction** (not control flow)
2. **Channels always connect two agents** (never agent to storage)
3. **Request direction indicates initiator** (client → server = R▶)
4. **Storages have no outgoing arrows** (except read access)
5. **Agents have no direct arrows to agents** (use channels)

### Visual Hierarchy

| Priority | Connector Type | Line Weight |
|----------|---------------|-------------|
| 1 | Request/Response | 2px |
| 2 | Data Flow | 1.5px |
| 3 | Read/Write Access | 1.5px |
| 4 | Protocol Boundary | 1px dashed |
