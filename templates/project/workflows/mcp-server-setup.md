# MCP Server Setup

<system_context>
> Project workflow — A standardized workflow for connecting this workspace to a local or remote Model Context Protocol (MCP) server.
</system_context>

<instruction>
When the user requests to attach an external data source or tool (like a database or JIRA) to this workspace, act as the Orchestrator and execute the following steps to establish the MCP connection.
</instruction>

## Steps

1. **Identify the Data Source**: Ask the user what service they want to connect to via MCP (e.g., PostgreSQL, internal REST API, Jira).
2. **Locate the Server**: Query the official `modelcontextprotocol/servers` repository to find if an official or community server exists for the destination. If so, output the npx/docker run command.
3. **Configure the Host IDE**:
   - For **Cursor**: Guide the user to edit `.cursor/mcp.json` or add the tool via the Cursor Settings UI.
   - For **Claude Code**: Provide the exact CLI command to add the server (e.g., `claude mcp add db -- npx -y @modelcontextprotocol/server-postgres postgresql://...`).
   - For **Kilo Code**: Guide the user to configure `.kilocode/mcp.json`.
4. **Test the Connection**: Ask the user to restart their IDE/agent and use a simple prompt (e.g., "List all tables in the database") to verify the MCP tools are actively exposed to the context window.
5. **Document the Primitives**: Once connected, document the new **Tools** and **Resources** exposed by the server in the project's architecture documentation.
