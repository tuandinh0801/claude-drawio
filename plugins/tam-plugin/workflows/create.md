# TAM Create Workflow

Detailed workflow for creating TAM diagrams using official stencils.

---

## Overview

The `/tam-create` command generates TAM-compliant diagrams using official SAP TAM stencils.

---

## Step 1: Start Session

```
start_session
```

Opens browser with real-time preview.

---

## Step 2: Analyze Request

Parse description and identify elements:
- Active components → `agent` stencil
- Human participants → `human-agent` stencil
- Data stores → `storage` stencil
- Communication → `n-hor-channel` / `z-vert-channel` stencils

---

## Step 3: Look Up Stencil XML

For each element, retrieve the **exact mxCell XML** from the official TAM stencil library located at `stencils/official/TAM-BD.xml`.

---

## Step 4: Generate Layout

Position elements using 8px grid:
- Human agents: top row (y=40)
- Agents: middle (y=160)
- Storages: bottom (y=280)
- Channels: between connected agents

---

## Step 5: Assemble mxGraphModel

Combine stencil XML into complete diagram:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0"/>
    <mxCell id="1" parent="0"/>
    <!-- Stencil cells with unique numeric IDs -->
  </root>
</mxGraphModel>
```

---

## Step 6: Create Diagram

```
create_new_diagram(xml)
```

---

## Stencil Mapping Table

| Keyword | Stencil ID |
|---------|------------|
| user, customer, person | `human-agent` |
| server, service, handler | `agent` |
| database, db, storage | `storage` |
| channel, api, http | `n-hor-channel` |
| queue, message | `queue` |
