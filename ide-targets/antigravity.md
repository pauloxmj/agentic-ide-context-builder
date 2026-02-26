---
description: IDE-specific path mappings, context file configuration, settings.json layers, and capabilities for Google Antigravity (Gemini).
category: ide-target
---

# Antigravity (Gemini)

Google's AI coding assistant integrated into VS Code, with deep filesystem access and layered settings configuration.

## Path Mapping

| Artifact | Project Path | Global Path |
|----------|-------------|-------------|
| **Rules** | `.agent/rules/` | `~/.gemini/antigravity/rules/` |
| **Workflows** | `.agent/workflows/` | `~/.gemini/antigravity/workflows/` |
| **Skills** | `.agent/skills/` | `~/.gemini/antigravity/skills/` |
| **Context File** | `GEMINI.md` (default) or `AGENTS.md` (configurable) | — |
| **Settings** | `.gemini/settings.json` | `~/.gemini/settings.json` |

## Context File Configuration

By default, Antigravity reads `GEMINI.md` in the project root. To use `AGENTS.md` instead:

```json
// .gemini/settings.json
{
  "contextFileName": "AGENTS.md"
}
```

This makes Antigravity compatible with the universal `AGENTS.md` standard used by Copilot and Cursor.

## Settings Precedence

Settings are resolved in order (highest to lowest):

| Level | Path | Purpose |
|-------|------|---------|
| **Project** | `.gemini/settings.json` | Workspace-specific config |
| **User** | `~/.gemini/settings.json` | Personal defaults |
| **System** | `/etc/gemini-cli/settings.json` | Organization-wide policies |

## Rule Activation

| Type | Mechanism |
|------|-----------|
| **Always** | Rules without `globs` in frontmatter — loaded for every request |
| **Glob-Scoped** | Rules with `globs` in frontmatter — applied only when matching files |

Rules are standard `.md` files with YAML frontmatter:

```yaml
---
description: Enforce Tailwind v4 patterns
globs: app/**/*.tsx
---
```

## Format Requirements

- **File extension**: `.md` (standard markdown)
- **Rule activation**: Conditional via YAML frontmatter `globs` field
- **Workflow activation**: Must have a `description` in YAML frontmatter
- **Supports**: `// turbo` and `// turbo-all` annotations in workflows

## Unique Capabilities

- **Deep Filesystem Access**: Full native terminal access — agents can traverse directories and run scripts
- **MCP Integration**: Configure MCP servers in `settings.json` under `mcpServers` key
- **Knowledge Items (KI)**: Persistent knowledge artifacts generated across sessions
- **Browser Subagent**: Can spawn browser interactions for testing
- **Artifacts System**: Structured task tracking with `task.md`, `implementation_plan.md`, `walkthrough.md`

## Sync from `.agent/`

| Source | Destination | Conversion |
|--------|------------|------------|
| `.agent/rules/` | Already in place | No sync needed (Antigravity reads `.agent/` natively) |
| `.agent/skills/` | Already in place | No sync needed |
| `.agent/workflows/` | Already in place | No sync needed |

> **NOTE**: Antigravity reads `.agent/` directly — no syncing required for project-level configurations.

## LLM-Friendly Documentation

- **Primary Docs**: The agentic-architecture repository README and AGENTS.md
- **Skills Guide**: Read `~/.gemini/antigravity/skills/*/SKILL.md` for available global skills

## AI Rules

- **MUST** use `.md` file extension for all rules, workflows, and skills
- **MUST** include `description` in YAML frontmatter for workflows
- **MUST** use `globs` in frontmatter for file-scoped rules
- **MUST** set `contextFileName: AGENTS.md` in `.gemini/settings.json` when using the universal standard
- **IF** syncing from `.agent/` → no conversion needed (Antigravity reads `.agent/` natively)
- **IF** configuring MCP → add server definitions to `settings.json` under `mcpServers`
