---
description: Universal architecture for the Model Context Protocol (MCP) — the standard for AI agent integration with external data sources, with cross-IDE configuration locations.
category: knowledge
---

# Model Context Protocol (MCP) Architecture

An open standard (Client-Server model) facilitating normalized communication between AI agents and external data sources (APIs, databases). Solves the "N × M" integration problem — acting as a universal "USB-C port" for AI tools across IDEs.

## Architectural Hierarchy

| Layer | Role |
|-------|------|
| **Host** | IDE/Application running the LLM |
| **Client** | Module formatting request payloads, 1:1 mapping to a server |
| **Server** | Exposes capabilities, runs locally via `stdio` or remotely via HTTP (SSE) |

## MCP Primitives

| Primitive | Purpose | Example |
|-----------|---------|---------|
| **Tools** | Executable functions providing actionable power | Query database, create issue |
| **Resources** | Immutable/mutable data sources providing context | Logs, schema mappings |
| **Prompts** | Reusable JSON-RPC templates for repeating interactions | Structured query patterns |

## MCP vs. Agent Skills

| Aspect | Agent Skills (`SKILL.md`) | MCP Server |
|--------|--------------------------|------------|
| **Context** | Reusable prompt packages instructing "how to code" | Standardized data connectivity "access to data" |
| **Execution** | Agent runs bash/python scripts natively | Agent sends structured JSON-RPC payloads |
| **State** | Project-localized, stateless instructions | Stateful external system connections (Jira, DB, Slack) |

## Cross-IDE MCP Configuration

| IDE | MCP Config Location | Notes |
|-----|---------------------|-------|
| **Kilo Code** | Via extension settings | Full native MCP support |
| **Antigravity** | `~/.gemini/settings.json` or `.gemini/settings.json` | Under `mcpServers` key |
| **Cursor** | Editor settings → `mcp.json` | Global or project-level |
| **Copilot** | VS Code settings | Supports reading external data sources |

## AI Rules

- **MUST** use MCP for external data access (databases, APIs, issue trackers) — not custom scripts
- **MUST** configure MCP servers via IDE-specific settings (see `ide-targets/`)
- **MUST NOT** confuse MCP (data access) with Skills (instructions) — they are complementary
- **IF** a task requires live external data → use MCP tools, not hardcoded API calls
