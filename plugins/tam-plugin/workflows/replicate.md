# TAM Replicate Workflow

Detailed workflow for replicating existing diagrams as TAM-compliant diagrams.

---

## Overview

The `/tam-replicate` command converts existing architecture diagrams (images/screenshots) into TAM-compliant Draw.io diagrams.

---

## Step 1: Start Session

```
start_session
```

Opens browser with real-time preview.

---

## Step 2: Analyze Image

When user uploads an image, analyze it to identify:

### Visual Elements to TAM Mapping

| Visual Element | TAM Element |
|----------------|-------------|
| Rectangle (labeled as service/component) | Agent |
| Stick figure / Person icon | Human Agent |
| Cylinder / Database icon | Storage |
| Circle / Oval (message/event) | Channel |
| Cloud shape | External system (subsystem) |
| Arrow with label | Access (read/write) |
| Bidirectional arrow | Modify access or channel |
| Dashed box | Module/subsystem boundary |
| Horizontal line with label | Protocol boundary |

### Relationship Detection

- Arrows pointing TO database → Write access
- Arrows pointing FROM database → Read access
- Bidirectional curved arrows → Modify access
- Lines between services with circle → Channel communication

---

## Step 3: Extract Structure

Create a mental model of the diagram:

```yaml
# Example extraction from image
elements:
  - type: human-agent
    label: "Customer"
    position: top-left

  - type: agent
    label: "Web Server"
    position: center-left

  - type: agent
    label: "API Gateway"
    position: center

  - type: storage
    label: "User DB"
    position: bottom-center

connections:
  - from: Customer
    to: Web Server
    type: channel-request

  - from: API Gateway
    to: User DB
    type: read-write
```

---

## Step 4: Apply TAM Rules

Convert the extracted structure to valid TAM:

### Rule 1: No Direct Agent-to-Agent

If image shows: `Service A → Service B`

Convert to: `Service A → [Channel] → Service B`

### Rule 2: Proper Access Direction

- Data flowing TO storage = write access
- Data flowing FROM storage = read access
- Bidirectional = modify access (two curved arrows)

### Rule 3: Channel Request Direction

If image shows client-server pattern:
- Add `R→` indicator pointing toward server
- Request direction indicates initiator

---

## Step 5: Generate TAM Diagram

Create the XML following TAM conventions:

### Layout Guidelines

- Human agents at top
- Active agents in middle
- Storages at bottom
- Channels between communicating agents
- Protocol boundaries as horizontal dashed lines

### Spacing

- 200px horizontal spacing between elements
- 150px vertical spacing between layers
- All positions on 8px grid

---

## Step 6: Create and Refine

1. Call `create_new_diagram` with generated XML
2. Compare with original image
3. Adjust positions/labels as needed
4. Apply user feedback

---

## Example Transformation

### Original Image Description
"Architecture showing User connecting to Frontend, Frontend calling Backend API, Backend reading from PostgreSQL"

### TAM Output

```yaml
agents:
  - id: user
    type: human-agent
    label: User

  - id: frontend
    type: agent
    label: Frontend

  - id: backend
    type: agent
    label: Backend API

storages:
  - id: postgres
    type: storage
    label: PostgreSQL

channels:
  - id: httpFrontend
    type: channel-request
    requestDirection: east
    between: [user, frontend]

  - id: httpBackend
    type: channel-request
    requestDirection: east
    between: [frontend, backend]

accesses:
  - from: backend
    to: postgres
    type: read
    label: Query
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Can't identify element type | Ask user for clarification |
| Complex nested structures | Use modules/subsystems |
| Too many connections | Simplify or use protocol boundaries |
| Image too blurry | Request clearer image |
