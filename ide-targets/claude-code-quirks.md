---
description: IDE capabilities and path configurations for Claude Code.
---

<ide_target name="claude-code">
# Claude Code Specifics

## Paths & Storage

<ide_quirk type="rule">
- **Project Rules**: `.claude/rules/*.md`
- **Global Rules**: `~/.claude/rules/*.md`
- **Root Context**: `CLAUDE.md` (Alternative/Supplement to AGENTS.md).
- **Activation**: Triggers conditionally via YAML frontmatter using the `paths:` array (e.g., `paths: ["src/**/*.ts"]`).
</ide_quirk>

<ide_quirk type="skill">
- **Global Skills**: `~/.claude/skills/`
- **Project Skills**: `<project>/.claude/skills/`
- **Plugin Skills**: `<plugin>/skills/`
- **Frontmatter Extensions**:
  - `disable-model-invocation`: If `true`, requires manual invoke via `/name`.
  - `user-invocable`: If `false`, hidden from user menus; model-only.
  - `context`: `fork` runs script in an isolated subagent instead of local terminal.
</ide_quirk>

## Native Capabilities

<ide_quirk type="context_memory">
- **Auto Memory**: Captures insights and patterns directly into `MEMORY.md`. Allows private carryover of knowledge across sessions without bloating explicit text-based rules.
</ide_quirk>

<ide_quirk type="mcp">
- **First-Class MCP**: Deep MCP integration defined locally/globally. Rules in `CLAUDE.md` can explicitly guide the agent on when to execute specific MCP tools.
</ide_quirk>

<ide_quirk type="documentation">
- **Official AI Docs**: `https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview` and `https://code.claude.com/docs/llms.txt`
- **Usage**: Use these as the source of truth for Claude Code specific CLI flags and tool use configurations.
</ide_quirk>
</ide_target>
