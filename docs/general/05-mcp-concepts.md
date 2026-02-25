# Model Context Protocol (MCP)

<system_context>
This is file `general/05-mcp-concepts.md`.
It explains the universal open-source architecture for how AI agents securely access external data and tools.
</system_context>

## What is MCP?

The **Model Context Protocol (MCP)** is an open standard introduced by Anthropic (but widely adopted by Cursor, Claude Code, Antigravity, and Kilo) that standardizes how AI agents communicate with data sources and tools.

Historically, connecting an AI to a Jira board, a PostgreSQL database, or a Slack channel required writing custom, hardcoded API integrations for every single IDE. MCP solves the "N x M" integration problem by acting as a universal "USB-C port" for AI tools.

## The Architecture

MCP operates on a strict Client-Server model, typically communicating via JSON-RPC 2.0 or secure STDIO over local processes:

1. **The Host**: The IDE or application running the LLM (e.g., Cursor, Claude Code).
2. **The Client**: A module inside the Host that strictly formats the LLM's requests (1:1 connection to server).
3. **The Server**: A standalone script or binary that exposes context, tools and resources to the client.

### MCP Primitives
MCP structures the data it provides into three main capabilities (Primitives):
1. **Tools**: Executable functions the AI can invoke to perform actions (e.g., executing a database query, fetching an API).
2. **Resources**: Data sources that provide contextual information (e.g., file contents, a live dashboard graph, database schemas).
3. **Prompts**: Reusable templates that structure interactions (e.g., a pre-defined system prompt asking the server to summarize specific data).

### Transport Layers
Communication between the Client and Server occurs via:
- **Stdio transport**: Direct process communication for local servers on the same machine.
- **HTTP transport (with SSE)**: Enables remote server communication with standard HTTP authentication (API keys, OAuth).

<example title="MCP in Action">
If you build an MCP server for your company's proprietary logging system, a developer using Claude Code and a developer using Cursor can both connect to that exact same server.
Both agents will suddenly gain the ability to use the `<query_logs>` tool during a debugging workflow.
</example>

## MCP vs. Agent Skills

While both expand agent capabilities, they serve different architectural roles:

| Feature | Agent Skills (`SKILL.md`) | Model Context Protocol (MCP) |
|---------|---------------------------|------------------------------|
| **Core Function** | Reusable, domain-specific prompt packages and shell scripts. | Standardized data connectivity and external API tool endpoints. |
| **Execution** | The agent reads the instructions and decides how to execute the attached bash/python scripts natively. | The agent sees exposed JSON schemas and sends structured JSON-RPC payloads to the server. |
| **State** | Generally stateless, project-localized context injections. | Can maintain persistent, secure connections to external systems (databases, CRM, Git providers). |

**Best Practice**: Use Agent Skills to teach an AI *how to code* complex tasks in your project. Use MCP servers to give the AI *access to data* it cannot reach via the local filesystem.

<instruction>
You have finished reading the core `general/` concepts. 
Proceed to the target IDE inside `ide-specific/` (e.g., `ide-specific/05-claude-code.md`) to learn the specific directories and features required by that system.
</instruction>
