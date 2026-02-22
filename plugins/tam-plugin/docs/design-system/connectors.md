# TAM Connectors Reference

TAM uses specific connector styles for different relationship types based on FMC methodology.

> **Note:** For construction patterns and rules, see [SKILL.md](../../skills/tam/SKILL.md).

---

## Access Type Semantics

Arrow direction indicates **data flow direction**, not request direction:

| Access Type | Arrow | Meaning |
|-------------|-------|---------|
| **Read** | Storage → Agent | Agent reads from storage |
| **Write** | Agent → Storage | Agent writes to storage |
| **Modify** | Agent ↔ Storage | Agent reads AND writes |
| **Channel** | No arrow | Communication link between agents |

---

## Block Diagram Connectors

### Read Access (Storage → Agent)

Data flows FROM storage TO requesting agent.

```xml
<mxCell id="5" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="storage" target="agent">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

**When to use:** Agent retrieves data from storage.

### Write Access (Agent → Storage)

Data flows FROM agent TO storage.

```xml
<mxCell id="5" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="agent" target="storage">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

**When to use:** Agent persists data to storage.

### Modify Access (Bidirectional)

Data flows both directions - agent reads AND writes.

```xml
<mxCell id="5" style="endArrow=classic;startArrow=classic;strokeWidth=2;" edge="1" parent="1" source="agent" target="storage">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

**When to use:** Agent both reads and writes to storage.

### Channel Connection (No Arrow)

Simple connection without direction - used for agent-channel links.

```xml
<mxCell id="5" style="endArrow=none;strokeWidth=2;" edge="1" parent="1" source="agent" target="channel">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

**When to use:** Connecting agents to channels.

---

## Request-Response Pattern

For API/HTTP patterns, add protocol labels to edges:

```
┌──────────┐  [SCIM2]  ┌───┐     ┌──────────┐
│  Client  │──────────►│ R │────►│  Server  │
└──────────┘           └───┘     └──────────┘
```

**XML with Protocol Label:**
```xml
<mxCell id="5" value="SCIM2" style="endArrow=classic;strokeWidth=2;" edge="1" parent="1" source="client" target="channel">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

Common protocol labels: `HTTP`, `SCIM2`, `X.509`, `Federation`, `REST`, `SOAP`

---

## TAM Connection Rules (FMC Bipartite)

**FUNDAMENTAL:** Active shapes (agents) connect ONLY to passive shapes (storages/channels).

| Connection | Valid? | Pattern |
|------------|--------|---------|
| Agent → Storage | ✓ | Write access |
| Storage → Agent | ✓ | Read access |
| Agent ↔ Storage | ✓ | Modify access |
| Agent ─ Channel ─ Agent | ✓ | Communication via channel |
| Agent → Agent | ✗ | **FORBIDDEN** - must use channel |
| Storage → Storage | ✗ | Invalid |

---

## Edge Style Reference

| Connector Type | Style |
|---------------|-------|
| Read/Write (arrow) | `endArrow=classic;strokeWidth=2;` |
| Modify (bidirectional) | `endArrow=classic;startArrow=classic;strokeWidth=2;` |
| Channel link (no arrow) | `endArrow=none;strokeWidth=2;` |
| With label | Add `value="Protocol"` attribute |

---

## Visual Patterns

### Agent-to-Agent via Channel

```
┌──────────┐     ┌───┐     ┌──────────┐
│  Agent1  │─────│   │─────│  Agent2  │
└──────────┘     └───┘     └──────────┘
              (channel)
```

### External Access via Boundary Channel

```
External ──[Protocol]──► ○ ──► Agent (inside boundary)
                        (R)
```

### Storage Access Pattern

```
┌──────────┐              ┌──────────┐
│  Agent   │──────────────│ Storage  │
└──────────┘      ↑       └──────────┘
                  │
         Arrow direction indicates
         data flow (write = →, read = ←)
```
