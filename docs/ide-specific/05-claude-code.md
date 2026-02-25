# Claude Code Implementation

<system_context>
This is file `ide-specific/05-claude-code.md`.
It details how Anthropic's Claude Code implements AI agent concepts like rules and skills.
</system_context>

## Custom Rules

Claude Code has a highly structured, strict approach to project memory.

| Scope | Location |
|-------|----------|
| **Project Rules** | `.claude/rules/*.md` |
| **Personal Rules** | `~/.claude/rules/*.md` |
| **Root Context** | `CLAUDE.md` (Alternative/Supplement to AGENTS.md) |

### Glob Matching

Unlike Cursor which uses `.mdc` and `globs:`, Claude uses standard `.md` files but parses a specific `paths:` YAML array in the frontmatter.

<example title="Claude Code Rule Structure">
```markdown
---
paths:
  - "src/api/**/*.ts"
  - "{src,lib}/**/*.ts"
---

# API Development Rules
- All API endpoints must include input validation.
- Use the standard error response format.
```
</example>

If the `paths:` frontmatter is omitted, the rule applies globally across the codebase whenever Claude is active. *Note: Community reports indicate `paths:` scoping can occasionally be inconsistent during file creation events unless a PostToolUse hook forces reading.*

## Claude Memory

Beyond raw text rules, Claude Code implements a powerful persistence layer called **Auto memory**. Designed for professional environments, this system records insights, patterns, and preferences automatically into a `MEMORY.md` file. This allows the agent to privately carry recurring knowledge across sessions and repositories without bloating the explicit text-based `.md` rules. Ensure it is enabled in your environment (it can be toggled via `CLAUDE_CODE_DISABLE_AUTO_MEMORY`).

## Agent Skills

Claude Code has first-class integration with the Agent Skills standard, and has actively championed the format.

| Scope | Location |
|-------|----------|
| Personal | `~/.claude/skills/` |
| Project | `<project>/.claude/skills/` |
| Plugin | `<plugin>/skills/` |

### Frontmatter Extensions

Claude introduces optional keys specifically for tool-based skill integration:

- `disable-model-invocation`: If `true`, the model cannot use the skill independently; the user must invoke it via `/name`.
- `user-invocable`: If `false`, the skill is hidden from the user's `/` menu and only the model can use it.
- `context`: If set to `fork`, the script runs in an isolated subagent context instead of the local terminal.

## Model Context Protocol (MCP) Integrations

Since Anthropic authored the open-source MCP standard, Claude Code features first-class MCP integration. Through the CLI or IDE interface, Claude can dynamically connect to external enterprise tools (Salesforce, Zendesk, PostgreSQL) by spinning up MCP servers. Rules in `CLAUDE.md` can explicitly guide the agent on *when* to execute specific MCP tools during a workflow.
