# Claude Draw.io Plugin Marketplace

AI-powered Draw.io diagram generation with Design System, real-time browser preview, and 3 workflows for Claude Code.

## Installation

### 1. Add the Marketplace

```shell
/plugin marketplace add tuandinh0801/claude-drawio
```

### 2. Install the Plugin

```shell
/plugin install drawio-plugin@claude-drawio
```

### 3. Start Creating

```shell
/drawio-create a login flowchart with validation
```

## Commands

| Command | Description |
|---------|-------------|
| `/drawio` | Main skill entry point |
| `/drawio-create` | Create diagrams from natural language |
| `/drawio-edit` | Edit existing diagrams |
| `/drawio-replicate` | Recreate images as diagrams |

## Features

- **Real-time Preview** - Diagrams update in browser as Claude creates them
- **Design System** - Unified visual language with themes, tokens, and semantic shapes
- **Natural Language** - Describe diagrams in plain text
- **Cloud Architecture** - AWS, GCP, Azure with official icons
- **Math Typesetting** - LaTeX/AsciiMath equations in labels
- **IEEE Academic Style** - Publication-ready diagrams

## Themes

| Theme | Use Case |
|-------|----------|
| **tech-blue** (default) | Software architecture, DevOps |
| **academic-color** | Academic papers with color |
| **academic** | IEEE grayscale print |
| **nature** | Environmental, lifecycle |
| **dark** | Presentations, slides |

## Quick Examples

### Create a Flowchart
```
/drawio-create
A user authentication flow:
- Login form
- Validate credentials (decision)
- Success → Dashboard
- Failure → Error message → Login form
```

### Create AWS Architecture
```
/drawio-create --theme tech-blue
AWS serverless API:
- API Gateway (service)
- Lambda functions (service)
- DynamoDB (database)
- S3 bucket (storage)
```

### Replicate an Image
```
/drawio-replicate --theme academic
[Upload image]
Recreate this research paper figure
```

### Edit Existing Diagram
```
/drawio-edit
Change "User Service" to "Auth Service"
Add a Cache node between API and Database
```

## Architecture

```
Claude Code <--stdio--> MCP Server <--http--> Browser (draw.io)
```

1. Ask Claude to create a diagram
2. Claude calls `start_session` to open browser
3. Claude generates diagram XML
4. Diagram appears in real-time!

## Requirements

- Node.js 18+ (for npx)
- Modern browser (Chrome, Firefox, Safari, Edge)

## MCP Server

The plugin automatically configures the MCP server:

```json
{
  "command": "npx",
  "args": ["--yes", "@next-ai-drawio/mcp-server@latest"]
}
```

Default port: `6002` (auto-increments if in use)

## Links

- [MCP Server Repository](https://github.com/DayuanJiang/next-ai-draw-io)
- [Homepage](https://next-ai-drawio.jiang.jp)

## License

MIT License - See [LICENSE](LICENSE)

## Author

- **Plugin Author**: Tuan Dinh
- **MCP Server Author**: DayuanJiang
