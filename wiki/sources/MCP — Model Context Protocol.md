---
title: MCP — Model Context Protocol
type: source
raw: raw/notes/MCP.md
date_ingested: 2026-05-04
tags: [ai, tooling, mcp, cursor, figma]
---

## Summary
MCP (Model Context Protocol) is an open standard from Anthropic (announced late 2024) that lets AI models interact with external systems — Figma, Git, databases, and more. The note focuses on Figma + Cursor integration as the main example.

## Key takeaways
- MCP gives AI models structured access to external context and tools
- Large ecosystem of MCP servers at mcp.so and pulsemcp.com
- **Figma + Cursor** via `figma-developer-mcp`: get Figma API token → add server config → paste Figma frame URL → Cursor lays out the design
- **Reverse** (Cursor → Figma): `cursor-talk-to-figma-mcp`
- **Zapier MCP**: integrations with hundreds of services
- Security caveat: MCP servers get access to local files — only use trusted servers

## Setup snippet (Figma)
```json
{
  "mcpServers": {
    "Framelink Figma MCP": {
      "command": "npx",
      "args": ["-y", "figma-developer-mcp", "--figma-api-key=<token>", "--stdio"]
    }
  }
}
```

## Connections
[[Dev Setup & Tools]] [[Software Development]]
