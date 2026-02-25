---
description: IDE capabilities and path configurations for Kilocode.
---

<ide_target name="kilocode">
# Kilocode Specifics

## Paths & Storage

<ide_quirk type="rule">
- **Project Rules**: `.kilocode/rules/` (Preferred over legacy `.kilorules`)
- **Global Rules**: `~/.kilocode/rules/`
- **Mode-Specific Rules**: `.kilocode/rules-[mode-name]/` (e.g., `rules-docs-writer/`)
</ide_quirk>

<ide_quirk type="workflow">
- **Project Workflows**: `.kilocode/workflows/`
</ide_quirk>

<ide_quirk type="skill">
- **Global Skills**: `~/.kilocode/skills/`
- **Global Mode-Specific Skills**: `~/.kilocode/skills-[mode-name]/`
- **Project Skills**: `<project>/.kilocode/skills/`
- **Project Mode-Specific Skills**: `<project>/.kilocode/skills-[mode-name]/`
</ide_quirk>

## Native Capabilities

<ide_quirk type="architectural_pattern">
- **Custom Modes (Orchestration)**: Kilocode natively supports creating restricted sub-agents (modes) via YAML definitions. The primary agent can use the `new_task()` tool to spawn isolated tasks in these specialized modes (e.g., `architect`, `testing`).
</ide_quirk>

<ide_quirk type="tool_execution">
- **Filesystem Agent**: Kilocode agents have full native terminal access. They can execute bash/python scripts from a `SKILL.md` directly in the shell (e.g., `gh`, `docker`, `npm`).
- **Built-in Tools**: `read_file()`, `search_files()`, `execute_command()`, `new_task()`.
</ide_quirk>

<ide_quirk type="mcp">
- **Native MCP Support**: Kilocode fully supports MCP for external tool integration (Jira, DBs, etc.).
</ide_quirk>

<ide_quirk type="documentation">
- **Official AI Docs**: `https://kilo.ai/docs/llms.txt`
- **Usage**: Parse this URL to guarantee you are generating rules and skills compliant with the latest Kilocode orchestrator definitions.
</ide_quirk>
</ide_target>
