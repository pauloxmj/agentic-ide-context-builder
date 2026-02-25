---
description: Universal architecture for the Model Context Protocol (MCP).
---

<concept id="mcp-integration">
# Model Context Protocol (MCP) Architecture

- **Definition**: An open standard (Client-Server model) facilitating normalized communication between AI agents and external data sources (APIs, databases).
- **Goal**: Solves the "N x M" integration problem, acting as a universal "USB-C port" for AI tools across IDEs (Cursor, Claude Code, Antigravity, Github Copilot).

## Architectural Hierarchy
1. **The Host**: IDE/Application running the LLM.
2. **The Client**: Module strictly formatting request payloads corresponding 1:1 to a server.
3. **The Server**: Exposes capabilities, runs locally via `stdio` or remotely via HTTP (SSE) authorized by standard tokens.

## MCP Primitives
- **Tools**: Executable functions providing actionable power (e.g., query database).
- **Resources**: Immutable/mutable data sources proving context (e.g., logs, schema mappings).
- **Prompts**: Reusable JSON-RPC templates structuring repeating interactions.

## MCP vs Agent Skills Reference
| Aspect | Agent Skills (`SKILL.md`) | MCP Server |
|--------|--------------------------|------------|
| Context | Reusable, domain-specific prompt packages instructing "how to code". | Standardized data connectivity and endpoints proving "access to data". |
| Execution | Agent synthesizes bash/python scripts natively in the console. | Agent transmits structured JSON-RPC payloads mapping to exposed server schemas. |
| State | Project-localized, stateless instructions. | Stateful external system connections (e.g., Jira, PG, Slack). |
</concept>
