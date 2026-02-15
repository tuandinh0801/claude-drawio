# TAM Specification Format

YAML-based specification for TAM diagrams.

---

## Complete Structure

```yaml
meta:
  theme: sap-blue              # sap-blue | sap-grayscale | tam-classic
  diagramType: block           # block | class | usecase | activity | sequence | state | package
  level: conceptual            # conceptual | design
  layout: auto                 # auto | horizontal | vertical | hierarchical
  canvas: auto                 # auto | 800x600 | 1200x800
  title: System Architecture
  description: Overview of the system

agents:                        # Active components (Block Diagram)
  - id: webServer
    label: Web Server
    type: agent                # agent | human-agent
    multiple: false            # Show as stacked?
    module: frontend           # Parent module
    position:                  # Optional manual position
      x: 100
      y: 100
    nested:                    # Nested components
      - id: requestHandler
        label: Request Handler
        type: agent

storages:                      # Passive components (Block Diagram)
  - id: userDB
    label: User Database
    type: storage
    module: persistence
    nested:
      - id: userTable
        label: Users
      - id: sessionTable
        label: Sessions

channels:                      # Communication points (Block Diagram)
  - id: httpChannel
    label: HTTP
    type: channel              # channel | channel-request
    requestDirection: east     # north | south | east | west
    between:
      - webServer
      - appServer

accesses:                      # Data flow (Block Diagram)
  - from: appServer
    to: userDB
    type: read                 # read | write | modify
    label: Query Users

  - from: appServer
    to: sessionDB
    type: modify
    label: Session CRUD

modules:                       # Grouping containers
  - id: frontend
    label: Frontend Layer
  - id: backend
    label: Backend Layer
  - id: persistence
    label: Persistence Layer

boundaries:                    # Protocol boundaries
  - label: HTTP/REST
    position: horizontal
    y: 200
  - label: JDBC
    position: horizontal
    y: 400

# UML Elements (Design Level)
components:                    # For design level
  - id: authComponent
    label: Authentication
    interfaces:
      provided:
        - IAuthenticate
      required:
        - IUserRepository

classes:                       # For class diagrams
  - id: userClass
    label: User
    attributes:
      - name: id
        type: String
      - name: email
        type: String
    operations:
      - name: authenticate
        parameters: [password: String]
        returnType: Boolean

useCases:                      # For use case diagrams
  - id: loginUC
    label: Login
    actors:
      - endUser
    includes:
      - validateCredentials

activities:                    # For activity diagrams
  - id: loginFlow
    label: Login Flow
    actions:
      - id: enterCredentials
        label: Enter Credentials
        type: action
      - id: validateInput
        label: Valid?
        type: decision
```

---

## Block Diagram Specific

### Agents

```yaml
agents:
  - id: orderProcessor
    label: Order Processor
    type: agent
    multiple: true             # Shows stacked agents

  - id: operator
    label: Operator
    type: human-agent          # Shows stick figure
```

### Storages

```yaml
storages:
  - id: orderDB
    label: Orders
    type: storage
    nested:
      - id: pendingOrders
        label: Pending
      - id: completedOrders
        label: Completed
```

### Channels

```yaml
channels:
  - id: httpAPI
    label: REST API
    type: channel-request
    requestDirection: east     # R▶ shows request goes right
    dataflowDirection: both    # Data flows both ways
    between:
      - clientAgent
      - serverAgent
```

### Accesses

```yaml
accesses:
  # Read: Storage → Agent
  - from: dataStorage
    to: readAgent
    type: read

  # Write: Agent → Storage
  - from: writeAgent
    to: dataStorage
    type: write

  # Modify: Both directions (two curved arrows)
  - from: updateAgent
    to: dataStorage
    type: modify
```

---

## Validation Rules

1. **Agents cannot have direct accesses to other agents**
2. **Storages cannot have outgoing write accesses**
3. **Channels must connect exactly 2 agents**
4. **Request direction required for channel-request type**
5. **Human agents cannot contain nested components**
6. **Conceptual level: only agents, storages, channels allowed**
7. **Design level: components, interfaces, ports allowed**
