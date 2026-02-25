---
description: IDE capabilities and path configurations for Google Antigravity (Gemini).
---

<ide_target name="antigravity">
# Antigravity Specifics

## Paths & Storage

<ide_quirk type="rule">
- **Project Rules**: `.agent/rules/`
- **Global Rules**: `~/.gemini/antigravity/rules/`
- **Activation**: Triggers conditionally via YAML frontmatter (`globs: app/**/*.tsx`). Without `globs`, the rule is global within the workspace.
</ide_quirk>

<ide_quirk type="workflow">
- **Project Workflows**: `.agent/workflows/`
- **Global Workflows**: `~/.gemini/antigravity/workflows/`
- **Requirement**: Must have a `description` in YAML frontmatter to display properly in the UI.
</ide_quirk>

<ide_quirk type="skill">
- **Global Skills**: `~/.gemini/antigravity/skills/`
- **Project Skills**: `<project>/.agent/skills/`
</ide_quirk>

## Native Capabilities

<ide_quirk type="filesystem">
- **Deep Filesystem Access**: The model can manually traverse the skill directory and run Python or Bash scripts seamlessly.
</ide_quirk>

<ide_quirk type="mcp">
- **Deep MCP Integration**: Define MCP server connections within the configuration to securely query external data sources or actuate workflows via JSON-RPC.
</ide_quirk>

<ide_quirk type="documentation">
- **Official AI Docs**: Read the resources in the primary `agentic-architecture` repository.
- **Usage**: Antigravity is highly integrated; use its base system instructions to understand edge-case behaviors.
</ide_quirk>
</ide_target>
