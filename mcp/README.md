# MCP Servers

Model Context Protocol servers extend AI agents with access to external tools and data.

Reference: https://modelcontextprotocol.io

---

## What is MCP?

MCP is an open standard by Anthropic for connecting tools to LLMs. Instead of custom code for each API — run an MCP server, and the agent connects automatically.

Adding a new service = add one MCP server config.

---

## Recommended Servers

### Context7 — Deep context management
```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```
**Use for:** large projects, maintaining consistency across sessions, structured memory.

---

### Serena — Codebase indexing
```json
{
  "mcpServers": {
    "serena": {
      "command": "uvx",
      "args": ["serena"]
    }
  }
}
```
**Use for:** large codebases where agent needs to navigate without loading entire files.
After splitting files into modules — always re-index with Serena.

---

### Playwright — Browser automation
```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```
**Use for:** web scraping, testing UI, screenshots, JS-rendered content.

---

### Filesystem — Local file access
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/dir"]
    }
  }
}
```

---

### GitHub — Repository operations
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<your-token>"
      }
    }
  }
}
```

---

## Claude Code Configuration

Add to `~/.claude/claude_desktop_config.json` or project `.claude/settings.json`:

```json
{
  "mcpServers": {
    "context7": { ... },
    "serena": { ... },
    "playwright": { ... }
  }
}
```

## Custom Server Template

See `mcp/custom-template.json` for building your own MCP server.

---

## MCP + LangGraph Stack

For building agents that use MCP programmatically (Python):

```python
from langchain_mcp_adapters.client import MultiServerMCPClient

client = MultiServerMCPClient({
    "your-server": {
        "url": "http://localhost:8000/sse",
        "transport": "sse"
    }
})
tools = await client.get_tools()
```

See `MCP + RAG + LangGraph` pattern in docs.
