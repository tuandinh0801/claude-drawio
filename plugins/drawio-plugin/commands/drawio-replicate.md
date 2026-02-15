---
description: Replicate an image as a Draw.io diagram using structured extraction
---

# /drawio-replicate

Replicate existing images or diagrams using structured extraction with Design System styling.

## Usage

```
/drawio-replicate
[Upload image]
```

```
/drawio-replicate --theme academic
【领域】软件架构
[Upload image]
```

## Procedure

1. **Receive Input** - Image upload (required)
2. **Configuration** - Select domain, theme, language
3. **Structured Extraction** - Analyze and extract to YAML specification
4. **Quality Validation** - Check complexity constraints
5. **Convert to Diagram** - Apply theme, create diagram
6. **Review and Refine** - Compare, use /drawio-edit for adjustments

## Domain Options

| Domain | Recommended Theme |
|--------|-------------------|
| 软件架构 (Software Architecture) | tech-blue |
| 商业流程 (Business Process) | tech-blue |
| 科研流程 (Research Workflow) | academic |
| 工业流程 (Industrial Process) | tech-blue |
| 教学设计 (Teaching Design) | nature |

## Shape Mapping

| Visual Element | Semantic Type |
|----------------|---------------|
| Rectangle/Box | `service` |
| Cylinder/Drum | `database` |
| Diamond | `decision` |
| Oval/Rounded rect | `terminal` |
| Parallelogram | `queue` |
| Person figure | `user` |
| Document shape | `document` |

## Examples

### From Flowchart Image
```
/drawio-replicate
【领域】商业流程
[Upload expense approval flowchart]
请复刻这个费用审批流程图
```

### From Architecture Screenshot
```
/drawio-replicate --theme tech-blue
【领域】软件架构
[Upload architecture diagram]
Recreate this microservices architecture
```

### From Research Paper Figure
```
/drawio-replicate --theme academic
【领域】科研流程
[Upload paper figure]
重绘论文实验流程图
```

## Complexity Limits

- **Modules** ≤ 5
- **Nodes per module** 3-7
- **Total nodes** ≤ 30
- **Labels** ≤ 14 characters

If exceeded, split into multiple diagrams.

## Full Documentation

See [workflows/replicate.md](workflows/replicate.md) for complete workflow details.
