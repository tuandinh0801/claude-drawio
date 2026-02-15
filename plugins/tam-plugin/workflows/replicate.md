# TAM Replicate Workflow

Detailed workflow for replicating existing diagrams as TAM-compliant diagrams.

---

## Overview

The `/tam-replicate` command converts existing architecture diagrams to TAM-compliant notation.

---

## Step 1: Start Session

```
start_session
```

Opens browser with real-time preview.

---

## Step 2: Analyze Image

Identify visual elements and map to TAM:

| Visual Element | TAM Stencil |
|----------------|-------------|
| Rectangle (labeled service) | `agent` |
| Stick figure / Person | `human-agent` |
| Cylinder / Database | `storage` |
| Circle (message/event) | `channel` |
| Arrow with label | `n-hor-arrow` / `z-vert-arrow` |
| Dashed box | module boundary |

---

## Step 3: Apply TAM Rules

### Rule 1: No Direct Agent-to-Agent
Image shows: `Service A → Service B`
Convert to: `Service A → [Channel] → Service B`

### Rule 2: Proper Access Direction
- Data flowing TO storage = write access
- Data flowing FROM storage = read access
- Bidirectional = `mod-access-*` stencils

### Rule 3: Channel Request Direction
For client-server patterns, add request direction indicator.

---

## Step 4: Generate TAM Diagram

Use official stencil XML from `stencils/official/TAM-BD.xml`.

---

## Step 5: Create and Refine

1. Call `create_new_diagram` with generated XML
2. Compare with original image
3. Adjust positions/labels as needed
