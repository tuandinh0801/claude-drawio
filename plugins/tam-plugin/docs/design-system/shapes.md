# TAM Official Stencils

This plugin uses **official TAM (Technical Architecture Modeling) stencils** from SAP.

---

## Block Diagram Stencils (TAM-BD)

| Stencil ID | Title | Dimensions | Purpose |
|------------|-------|------------|---------|
| `agent` | Agent | 120×60 | Active component (processes data) |
| `storage` | Storage | 120×60 | Passive data holder |
| `n-hor-channel` | N hor. Channel | 50×50 | Horizontal channel |
| `n-hor-channel-left` | N hor. Channel left | 50×50 | Horizontal channel (left variant) |
| `z-vert-channel` | Z vert. Channel | 50×50 | Vertical channel |
| `z-vert-channel-up` | Z vert. Channel up | 50×50 | Vertical channel (up variant) |
| `human-agent` | Human Agent | 60×60 | Human participant with stick figure |
| `mod-access-hor` | mod. Access hor. | 40×40 | Horizontal modify access |
| `mod-access-vert` | mod. Access vert. | 40×40 | Vertical modify access |
| `n-hor-arrow` | N hor. Arrow | 50×50 | Horizontal arrow |
| `z-vert-arrow` | Z vert. Arrow | 50×50 | Vertical arrow |
| `n-hor-connector` | N hor. Connector | 50×50 | Horizontal connector line |
| `z-vert-connector` | Z vert. Connector | 50×50 | Vertical connector line |
| `channel` | Channel | 20×20 | Small channel circle |
| `human` | Human | 20×40 | Human stick figure |
| `reqres-right` | ReqRes Right | 30×30 | Request/Response (right) |
| `reqres-left` | ReqRes Left | 10×~0 | Request/Response (left) |
| `reqres-up` | ReqRes Up | ~0×20 | Request/Response (up) |
| `reqres-down` | ReqRes Down | 30×30 | Request/Response (down) |
| `reqres-bi-vertical` | ReqRes Bi Vertical | 20×40 | Bidirectional vertical |
| `reqres-bi-horizontal` | ReqRes Bi Horizontal | 30×~0 | Bidirectional horizontal |
| `structure-variance` | Structure Variance | 150×90 | Structural variance |
| `queue` | Queue | 120×60 | Message queue |
| `l-shape` | L Shape | 240×240 | L-shaped container |
| `multiple-dots` | Multiple Dots | 45×5 | Multiplicity indicator |

---

## Activity Diagram Stencils (TAM-AD)

| Stencil ID | Title | Dimensions | Purpose |
|------------|-------|------------|---------|
| `action` | Action | 120×60 | Activity action node |
| `start-of-activity` | Start of Activity | 20×20 | Initial node |
| `end-of-activity` | End of Activity | 30×30 | Final node |
| `decision-or-merge` | Decision or Merge | 20×20 | Diamond decision/merge |
| `swimlane-vertical-lr` | Swimlane vertical l+r | 220×300 | Vertical swimlane |
| `swimlane-vertical-r` | Swimlane vertical r | 220×280 | Vertical swimlane (right) |
| `fork-or-join` | Fork or Join | 120×10 | Synchronization bar |
| `end-of-flow` | End of Flow | 30×30 | Flow termination |
| `object-node` | Object Node | 120×60 | Object/data node |

---

## Class Diagram Stencils (TAM-CD)

| Stencil ID | Title | Dimensions | Purpose |
|------------|-------|------------|---------|
| `class` | Class | 120×60 | UML class |
| `class-with-compartments` | Class with compartments | 140×70 | Class with attributes/operations |
| `association` | Association | 50×50 | Association relationship |
| `composition` | Composition | 50×50 | Composition (filled diamond) |
| `aggregation` | Aggregation | 50×50 | Aggregation (hollow diamond) |
| `specialization` | Specialization | 50×50 | Inheritance |
| `package` | Package | 200×100 | UML package |

---

## Sequence Diagram Stencils (TAM-SeqD)

| Stencil ID | Title | Dimensions | Purpose |
|------------|-------|------------|---------|
| `lifeline` | Lifeline | 120×360 | Object lifeline |
| `activation` | Activation | 20×120 | Activation bar |
| `no-focus` | No Focus | 20×120 | Inactive period |
| `sync-message-exchange` | Sync. Message Exchange | 160×60 | Synchronous call |
| `async-message-exchange` | Async. Message Exchange | 160×60 | Asynchronous call |
| `r2l-sync-message-exchange` | R2L Sync. Message Exchange | 160×60 | Right-to-left sync |
| `r2l-async-message-exchange` | R2L Async. Message Exchange | 160×60 | Right-to-left async |
| `self-call` | Self-Call | 20×120 | Self-referential message |

---

## Annotation Stencils (TAM-Ann)

| Stencil ID | Title | Dimensions | Purpose |
|------------|-------|------------|---------|
| `text` | Text | 40×20 | Text annotation |
| `area` | Area | 200×100 | Highlight area |
| `3-dots-hor` | 3 Dots hor. | 30×30 | Horizontal ellipsis |
| `3-dots-vert` | 3 Dots vert. | 30×30 | Vertical ellipsis |
| `border-vertical` | Border Vertical | 0×300 | Vertical border line |
| `border-horizontal` | Border Horizontal | 300×0 | Horizontal border line |
| `note` | Note | 100×100 | Note annotation |
| `curly-brace-*` | Curly Brace variants | various | Grouping braces |

---

## Usage

When creating TAM diagrams, use stencil IDs to specify exact shapes:

```yaml
nodes:
  - id: webServer
    stencil: agent
    label: Web Server

  - id: database
    stencil: storage
    label: PostgreSQL

  - id: httpChannel
    stencil: n-hor-channel

  - id: user
    stencil: human-agent
    label: User
```

---

## TAM Semantic Rules (Strictly Enforced)

1. **Agents cannot connect directly to agents** - use channels
2. **Storages are passive** - cannot initiate communication
3. **Channels are volatile** - no persistent data
4. **Access arrows show data flow direction**
5. **Request direction indicates initiator**
