# TAM Connectors Reference

TAM uses specific connector shapes for different relationship types.

---

## Block Diagram Connectors

### Information Flow (Unidirectional)

Use `BD-InfoFlowArrow-Rect-N` (horizontal) or `BD-InfoFlowArrow-Rect-Z` (vertical) for unidirectional data flow.

**When to use:** Agent writes to Storage, Agent reads from Storage

### Information Flow (No Arrow)

Use `BD-InfoFlow-Rect-N` or `BD-InfoFlow-Rect-Z` for connections without direction indicator.

**When to use:** Simple connections between shapes

### Modify Access (Bidirectional)

Use `BD-modAccessHor` (horizontal) or `BD-modAccessVert` (vertical) for read+write access.

**When to use:** Agent both reads and writes to Storage

### Channel Connection

Use `BD-Channel-Rect-N` (horizontal) or `BD-Channel-Rect-Z` (vertical) for agent-to-agent communication via channel.

**When to use:** Two Agents communicate through a Channel

### Request Direction

Use `BD-ReqResRight`, `BD-ReqResLeft`, `BD-ReqResUp`, `BD-ReqResDown` to indicate request direction on channels.

**When to use:** Client-server patterns showing who initiates

---

## TAM Connection Rules

1. **Agent ↔ Agent**: Must use Channel (BD-Channel + BD-Channel-Rect-*)
2. **Agent → Storage**: Use BD-InfoFlowArrow (write access)
3. **Storage → Agent**: Use BD-InfoFlowArrow (read access)
4. **Agent ↔ Storage**: Use BD-modAccess (modify access)
