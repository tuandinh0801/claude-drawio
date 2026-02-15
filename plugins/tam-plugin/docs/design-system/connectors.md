# TAM Connectors

TAM uses specific stencils for connectors rather than generic arrows.

---

## Access Types (Agent ↔ Storage)

### Read Access
Use `n-hor-arrow` or `z-vert-arrow` stencil pointing FROM storage TO agent.

### Write Access
Use `n-hor-arrow` or `z-vert-arrow` stencil pointing FROM agent TO storage.

### Modify Access
Use `mod-access-hor` or `mod-access-vert` stencil for bidirectional read/write.

---

## Channel Connectors (Agent ↔ Agent via Channel)

### Simple Connector
Use `n-hor-connector` or `z-vert-connector` to connect agents to channels.

### Request/Response Direction
Use `reqres-right`, `reqres-left`, `reqres-up`, `reqres-down` stencils to indicate request direction.

For bidirectional:
- `reqres-bi-vertical` - vertical bidirectional
- `reqres-bi-horizontal` - horizontal bidirectional

---

## Stencil-Based Connectors

| Purpose | Horizontal Stencil | Vertical Stencil |
|---------|-------------------|------------------|
| Data flow arrow | `n-hor-arrow` | `z-vert-arrow` |
| Simple connector | `n-hor-connector` | `z-vert-connector` |
| Modify access | `mod-access-hor` | `mod-access-vert` |
| Request direction | `reqres-right`/`reqres-left` | `reqres-up`/`reqres-down` |

---

## Generic Edge Style

When TAM stencils are not applicable, use standard Draw.io edges:

```xml
<mxCell style="edgeStyle=orthogonalEdgeStyle;rounded=0;
  strokeColor=#000000;strokeWidth=1;
  endArrow=block;endFill=1;" edge="1" />
```

---

## TAM Connector Rules

1. **Access arrows show data flow direction** - not control flow
2. **Request direction indicates initiator** - response flows opposite
3. **Channels connect exactly 2 agents** - never agent to storage
4. **Use appropriate stencil orientation** - N hor. for horizontal, Z vert. for vertical
