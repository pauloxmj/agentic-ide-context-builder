# Cursor Implementation

<system_context>
This is file `ide-specific/04-cursor.md`.
It details how the Cursor IDE implements AI agent concepts like rules, commands, and skills.
</system_context>

## Custom Rules (.mdc)

Cursor distinguishes its rule system by using the proprietary `.mdc` file extension along with YAML frontmatter to provide conditional matching.

| Scope | Location |
|-------|----------|
| **Project Rules** | `.cursor/rules/*.mdc` |
| **User (Global) Rules** | `~/.cursor/rules/*.mdc` |

### Frontmatter

<example title="Cursor Rule Structure">
```yaml
---
description: Applies React testing standards
globs: src/components/**/*.{ts,tsx}
alwaysApply: false
---

# React Testing Rules
- Use Testing Library over Enzyme.
- Ensure all custom hooks are mocked using `vi.mock()`.
```
</example>

## Modes & Context Memory

Before defining rules, understand Cursor's two primary operational environments:
1. **Composer Mode**: Optimized for rapid, multi-file code scaffolding, initial boilerplate generation, and turning designs into implementations.
2. **Agent Mode**: Optimized for deep investigation, bug fixing, and complex architectural changes requiring shell execution and extensive context gathering.

### Deprecation of Notepads
Historically, Cursor used a feature called "Notepads" to store reusable context packages. **Notepads have been deprecated**. Context should now be stored using Git-tracked project `.cursorrules`, `Memories` (to store recurring solutions mapping to specific prompts), and `.cursor/commands/`.

## Commands & Workflows

Cursor implements workflows primarily as built-in **Agent Hooks** and **Commands**. While they do not use the explicit `workflows/` directory seen in other tools, the concepts map to `.cursor/commands/`.

## Agent Skills

Cursor natively supports Agent Skills packages.

| Scope | Location |
|-------|----------|
| User (global) | `~/.cursor/skills/` |
| Project | `<project>/.cursor/skills/` |

Cursor operates as an advanced filesystem-based agent, so placing valid Agent Skills directories inside these locations grants the Cursor agent immediate access to the metadata and execution capabilities contained within.

### Model Context Protocol (MCP)

Cursor allows users to explicitly configure MCP servers in the editor settings. This generates an `mcp.json` file, which can be stored globally (`~/.cursor/mcp.json`) for the user or locally at the project root (`.cursor/mcp.json`). The Cursor agent can then evaluate a task and autonomously decide to call an active MCP tool (like searching a secure Confluence database) rather than just reading local files.
