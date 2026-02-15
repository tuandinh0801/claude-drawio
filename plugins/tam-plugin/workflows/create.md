# TAM Create Workflow

Detailed workflow for creating TAM diagrams from natural language.

---

## Overview

The `/tam-create` command generates TAM-compliant block diagrams from natural language descriptions, following SAP's Technical Architecture Modeling standard.

---

## Step 1: Start Session

Call the MCP tool to open the browser preview:

```
start_session
```

This opens a browser window at `http://localhost:6002` with real-time diagram preview.

---

## Step 2: Analyze Request

Parse the user's description to identify TAM elements:

### Element Detection Keywords

| TAM Element | Keywords |
|-------------|----------|
| **Agent** | server, service, handler, processor, manager, controller, worker, gateway |
| **Human Agent** | user, person, human, actor, operator, customer, admin, client |
| **Storage** | database, db, storage, repository, cache, store, data, table, redis, mongo |
| **Channel** | channel, queue, message, event, topic, stream, bus, api, http, rest, kafka |

### Example Analysis

User says: "Create an online shop with customers, web server, order processor, and product catalog"

Extracted elements:
- Human Agent: customers
- Agent: web server, order processor
- Storage: product catalog (implied database)

---

## Step 3: Apply TAM Rules

Validate the extracted elements against TAM semantic rules:

1. **No direct agent-to-agent connections**
   - If two agents need to communicate, add a channel between them

2. **Storages are passive**
   - Data flows FROM agents TO storages (write)
   - Data flows FROM storages TO agents (read)
   - Storages cannot initiate actions

3. **Channels connect agents**
   - Channels are volatile (no persistent data)
   - Add request direction (R→) for client-server patterns

---

## Step 4: Generate XML

Create the Draw.io mxGraphModel XML with TAM styling:

### Shape Styles

**Agent (Rectangle)**
```xml
<mxCell style="rounded=0;whiteSpace=wrap;html=1;
  fillColor=#FFFFFF;strokeColor=#0070F2;strokeWidth=2;" />
```

**Storage (Rounded Rectangle)**
```xml
<mxCell style="rounded=1;arcSize=60;whiteSpace=wrap;html=1;
  fillColor=#E5F0FF;strokeColor=#0070F2;strokeWidth=2;" />
```

**Channel (Circle)**
```xml
<mxCell style="ellipse;aspect=fixed;whiteSpace=wrap;html=1;
  fillColor=#FFFFFF;strokeColor=#0070F2;strokeWidth=2;" />
```

### Important: Use Numeric IDs Only

Draw.io requires numeric IDs. String IDs cause errors:
- ✅ `id="2"`, `id="3"`, `id="4"`
- ❌ `id="webServer"`, `id="agent1"`

---

## Step 5: Create Diagram

Call the MCP tool with the generated XML:

```
create_new_diagram(xml)
```

The diagram appears in the browser in real-time.

---

## Step 6: Iterate

Based on user feedback:
- Use `edit_diagram` for modifications
- Use `get_diagram` to retrieve current state
- Regenerate if major changes needed

---

## Example Output

For input: "web app with user, server, and database"

```yaml
agents:
  - id: user
    label: User
    type: human-agent
  - id: server
    label: Web Server
    type: agent

storages:
  - id: db
    label: Database
    type: storage

channels:
  - id: http
    label: HTTP
    type: channel-request
    requestDirection: east
    between: [user, server]

accesses:
  - from: server
    to: db
    type: read
    label: Query
  - from: server
    to: db
    type: write
    label: Store
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Diagram not appearing | Check browser URL has `?mcp=` parameter |
| "d.setId" error | Use numeric IDs only |
| Elements overlapping | Increase spacing in layout |
| Missing arrows | Check access definitions |
