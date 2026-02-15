# TAM Specification Format

YAML-based specification using official TAM stencils.

---

## Structure

```yaml
meta:
  diagramType: block    # block | activity | class | sequence
  title: System Architecture
  description: Overview

nodes:
  - id: unique-id
    stencil: agent      # TAM stencil ID (required)
    label: Display Name
    position:           # Optional manual position
      x: 100
      y: 100

edges:
  - from: source-id
    to: target-id
    stencil: n-hor-arrow  # Optional: use specific TAM stencil
    label: Optional Label
```

---

## Block Diagram Specification

```yaml
meta:
  diagramType: block
  title: Web Application

nodes:
  # Active components
  - id: user
    stencil: human-agent
    label: User

  - id: webServer
    stencil: agent
    label: Web Server

  - id: apiServer
    stencil: agent
    label: API Server

  # Passive components
  - id: database
    stencil: storage
    label: PostgreSQL

  # Communication
  - id: httpChannel
    stencil: n-hor-channel

edges:
  - from: user
    to: httpChannel
    stencil: n-hor-connector

  - from: httpChannel
    to: webServer
    stencil: n-hor-connector

  - from: webServer
    to: database
    stencil: z-vert-arrow
    label: Query
```

---

## Activity Diagram Specification

```yaml
meta:
  diagramType: activity
  title: Login Flow

nodes:
  - id: start
    stencil: start-of-activity

  - id: enterCreds
    stencil: action
    label: Enter Credentials

  - id: validate
    stencil: decision-or-merge
    label: Valid?

  - id: success
    stencil: action
    label: Show Dashboard

  - id: error
    stencil: action
    label: Show Error

  - id: end
    stencil: end-of-activity

edges:
  - from: start
    to: enterCreds
  - from: enterCreds
    to: validate
  - from: validate
    to: success
    label: Yes
  - from: validate
    to: error
    label: No
```

---

## Validation Rules

1. `stencil` must be a valid TAM stencil ID from the official library
2. Block diagrams: agents cannot connect directly (use channels)
3. Block diagrams: storages cannot initiate (passive only)
4. Sequence diagrams: lifelines required for all participants
5. All positions snap to 8px grid
