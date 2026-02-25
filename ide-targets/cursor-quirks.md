---
description: IDE capabilities and path configurations for Cursor.
---

<ide_target name="cursor">
# Cursor Specifics

## Paths & Storage

<ide_quirk type="rule">
- **Project Rules**: `.cursor/rules/*.mdc`
- **Global Rules**: `~/.cursor/rules/*.mdc`
- **Format**: Proprietary `.mdc` file extension.
- **Activation**: Triggers conditionally via YAML frontmatter (`globs: src/**/*.{ts,tsx}`).
</ide_quirk>

<ide_quirk type="workflow">
- **Commands**: Cursor maps workflow concepts to `.cursor/commands/` rather than explicit workflows.
</ide_quirk>

<ide_quirk type="skill">
- **Global Skills**: `~/.cursor/skills/`
- **Project Skills**: `<project>/.cursor/skills/`
</ide_quirk>

## Native Capabilities

<ide_quirk type="modes">
- **Composer Mode**: Optimized for rapid, multi-file code scaffolding and initial boilerplate generation.
- **Agent Mode**: Optimized for deep investigation, bug fixing, and complex architectural changes requiring shell execution and extensive context gathering.
</ide_quirk>

<ide_quirk type="context_memory">
- **Notepads**: Historically used for context packages, now **deprecated**. Use Git-tracked `.cursorrules`, Memories, and `.cursor/commands/` instead.
</ide_quirk>

<ide_quirk type="mcp">
- **MCP**: Configured via editor settings, generating `mcp.json` globally or locally. The agent autonomously decides to call active MCP tools.
</ide_quirk>

<ide_quirk type="documentation">
- **Official AI Docs**: `https://docs.cursor.com/llms.txt`
- **Usage**: When preparing Cursor rules or modifying configurations, parse this URL to ensure you are using the latest proprietary syntax.
</ide_quirk>
</ide_target>
