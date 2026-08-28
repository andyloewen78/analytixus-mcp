# Analytixus MCP Server

Analytixus is a metadata-driven development platform built around **DnAML** (Data and Analytics
Markup Language) — you model your data sources, transformations, and documentation once, and
generate SQL, pipelines, and docs from that single model instead of maintaining them by hand.

This MCP server exposes an Analytixus DnAML repository to any MCP-compatible client — Claude
Desktop, Cursor, VS Code Copilot Chat, or your own tooling — so an AI assistant can read and write
your metadata model directly.

> This repository hosts documentation and configuration guidance for the Analytixus MCP server.
> The server itself is distributed as a self-contained executable and as a .NET tool (see below).

## What it does

- **Browse the repository tree** — list solutions, sources, and objects in a DnAML model.
- **Read and write DnAML nodes** — fetch a single object's definition, create or update objects
  under a source or folder.
- **Solution management** — list available solutions, add/rename/delete them.

## Installation

**Option 1 — self-contained download (no runtime required).** Pre-built archives for Windows,
macOS, and Linux are available on request from the Analytixus team.

**Option 2 — .NET global tool** (requires the .NET 8 runtime):

```bash
dotnet tool install --global Analytixus.Mcp
```

This installs the `analytixus-mcp` command.

## Configuration

### Claude Desktop

Add to `claude_desktop_config.json`:

- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Linux: `~/.config/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "analytixus": {
      "command": "analytixus-mcp",
      "args": ["--stdio"],
      "env": {
        "ANALYTIXUS_SOLUTION_PATH": "/path/to/your/dnaml-solution",
        "ANALYTIXUS_SOLUTION_NAME": "YourSolutionName"
      }
    }
  }
}
```

(If you installed the self-contained archive instead of the .NET tool, use the full path to the
extracted `Analytixus.Mcp` executable as `command`.)

### VS Code / Claude Code

```bash
claude mcp add --env ANALYTIXUS_SOLUTION_PATH=/path/to/your/dnaml-solution \
  --env ANALYTIXUS_SOLUTION_NAME=YourSolutionName --scope user \
  analytixus -- analytixus-mcp --stdio
```

### Environment variables

| Variable | Purpose |
|---|---|
| `ANALYTIXUS_SOLUTION_PATH` | Path to the DnAML solution's root folder. |
| `ANALYTIXUS_SOLUTION_NAME` | Name of the solution — pins this server instance to it. |
| `ANALYTIXUS_LOG_LEVEL` | `Trace`\|`Debug`\|`Info`\|`Warn`\|`Error`\|`Fatal` (default `Info`). |

## Learn more

Visit [analytixus.de](https://analytixus.de) for more about the Analytixus platform.
