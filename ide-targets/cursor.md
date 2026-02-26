---
description: IDE-specific path mappings, 4 rule activation types, .mdc format, and capabilities for Cursor.
category: ide-target
---

# Cursor

AI-native code editor with agent, composer, and inline editing modes. Uses a proprietary `.mdc` rule format with 4 activation types.

## Path Mapping

| Artifact | Project Path | Global Path |
|----------|-------------|-------------|
| **Rules** | `.cursor/rules/*.mdc` | `~/.cursor/rules/*.mdc` |
| **User Rules** | — | Settings → General → "Rules for AI" |
| **Team Rules** | `.cursor/rules/` (committed to repo) | — |
| **Context Files** | `AGENTS.md` (native support) | — |

## 4 Rule Activation Types

Cursor rules use `.mdc` files with YAML frontmatter controlling when they activate:

| Activation Type | Frontmatter | When Applied |
|----------------|-------------|-------------|
| **Always** | `alwaysApply: true` | Included in every AI request automatically |
| **Auto-Attach** | `globs: ["src/**/*.ts"]` | Applied when working on files matching the glob pattern |
| **Agent-Requested** | `description: "..."` (no `alwaysApply`, no `globs`) | AI reads the description and decides whether to apply |
| **Manual** | No frontmatter metadata | Only applied when user explicitly `@mentions` the rule |

### `.mdc` Frontmatter Examples

```markdown
---
description: Enforce React component patterns
alwaysApply: true
---
# React Component Rules
- Always use functional components
- Export as default
```

```markdown
---
description: TypeScript test patterns for Vitest
globs: ["**/*.test.ts", "**/*.spec.ts"]
---
# Test Rules
- Use describe/it blocks
- Always include assertions
```

## Format Requirements

- **File extension**: `.mdc` (Markdown with Cursor-specific metadata)
- **Frontmatter fields**: `description`, `alwaysApply`, `globs`
- **AGENTS.md**: Read natively as agent instructions
- **`.cursorrules`**: Legacy file — still supported but `.cursor/rules/` is preferred

## Unique Capabilities

- **Agent Mode**: Deep investigation, multi-file edits, shell execution, and MCP tool calls
- **Background Agent**: Runs in the cloud, creates commits and PRs autonomously
- **AGENTS.md**: Native support — reads agent instructions from project root and nested directories
- **Subagents**: Can delegate tasks to specialized sub-agents
- **MCP**: Configured via editor settings or `.cursor/mcp.json`
- **Skills**: Reads `.cursor/skills/` for specialized capabilities

## Sync from `.agent/`

| Source | Destination | Conversion |
|--------|------------|------------|
| `.agent/rules/` | `.cursor/rules/` | Convert `.md` → `.mdc` (add `alwaysApply`/`globs` frontmatter) |
| `.agent/skills/` | `.cursor/skills/` | Direct copy |
| `.agent/workflows/` | `.cursor/commands/` | Rename directory, keep `.md` format |

> **IMPORTANT**: When converting rules from `.md` to `.mdc`, determine the correct activation type:
> - Rules with `globs` → use `globs` frontmatter (Auto-Attach)
> - Rules without `globs` that should always apply → add `alwaysApply: true`
> - Rules without `globs` that are contextual → use `description` only (Agent-Requested)

## LLM-Friendly Documentation

- **LLM Docs**: `https://docs.cursor.com/llms.txt`
- **Usage**: Parse for the latest `.mdc` format syntax and rule activation patterns

## AI Rules

- **MUST** use `.mdc` file extension for rules (not `.md`)
- **MUST** use `.cursor/commands/` for workflow-equivalent automation
- **MUST** set `alwaysApply: true` for rules that should always be active
- **MUST** use `globs` for file-type-specific rules
- **IF** syncing from `.agent/` → convert `.md` rules to `.mdc` format with correct activation type
- **IF** unsure about syntax → parse `https://docs.cursor.com/llms.txt` for latest proprietary syntax
