# Google Antigravity (Gemini) Implementation

<system_context>
This is file `ide-specific/02-antigravity.md`.
It details how the Antigravity agent implements concepts like rules, workflows, and skills.
</system_context>

## Custom Rules

Antigravity agentic capabilities are deeply tied to contextual memory and direct configuration.

### Rule Storage

| Scope | Location |
|-------|----------|
| **Project Rules** | `.agent/rules/` |
| **Global Rules** | `~/.gemini/antigravity/rules/` |

### Frontmatter

Antigravity rules can use YAML frontmatter to conditionally activate. If no frontmatter is provided, the rule applies globally across the codebase.

<example title="Antigravity Rule Structure">
```markdown
---
description: Next.js App Router rules
globs: app/**/*.tsx, app/**/*.ts
---

# Next.js Guidelines
- Always use server components by default.
- Add 'use client' only when hooks are required.
```
</example>

## Workflows

| Scope | Location |
|-------|----------|
| **Project** | `.agent/workflows/` |
| **Global** | `~/.gemini/antigravity/workflows/` |

Antigravity workflows allow you to define repeatable execution blueprints. Frontmatter such as `description` is required to display the workflow option correctly to the user.

## Agent Skills

Antigravity supports the standard Agent Skills specification.

| Scope | Location |
|-------|----------|
| Global | `~/.gemini/antigravity/skills/` |
| Workspace | `<project>/.agent/skills/` |

Antigravity provides deep filesystem access, meaning the model can manually traverse the skill directory and run attached Python or Bash scripts seamlessly.

### Model Context Protocol (MCP)

Antigravity deeply integrates with MCP. You can define MCP server connections within the configuration, allowing the agent to securely query external data sources or actuate workflows in third-party services via standardized JSON-RPC payloads.
