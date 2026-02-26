---
description: The AGENTS.md convention — the universal root-level entrypoint for AI coding agents, with IDE compatibility and content guidelines.
category: knowledge
---

# AGENTS.md Standard

The universal root-level entrypoint ("README for agents") used to provide initial context for AI coding agents. Adopted by 60,000+ open-source projects as of late 2025.

## Specification

- **Location**: Project root (`/AGENTS.md`)
- **Purpose**: Defines highest-level guardrails, build commands, testing workflows, and PR instructions before routing to IDE-specific configurations
- **Format**: Structured markdown following the llms.txt H1 + blockquote pattern

## IDE Compatibility

| IDE | AGENTS.md Support | Fallback Files |
|-----|-------------------|---------------|
| **Cursor** | ✅ Native (reads AGENTS.md automatically) | `.cursor/rules/` |
| **GitHub Copilot** | ✅ Native (nearest in directory tree) | `CLAUDE.md`, `GEMINI.md` |
| **Kilo Code** | ✅ Via rules directory | Custom instructions UI |
| **Antigravity** | ✅ Via `contextFileName` setting | `GEMINI.md` (default) |

## Content Guidelines

An effective AGENTS.md should contain:
1. **System Context**: H1 + blockquote with project name, tech stack, and key constraint
2. **Knowledge Base Map**: Directory map linking to docs, rules, skills, and workflows
3. **Standard Operating Procedure**: Numbered steps the agent must follow for every task
4. **Non-Negotiable Guardrails**: Hard rules the agent must never violate

For a complete authoring guide, see the docs-builder's `knowledge/agents-md-authoring.md`.

## AI Rules

- **MUST** place AGENTS.md at the project root — nested files supplement but don't replace the root file
- **MUST** focus exclusively on project-unique configurations — no generic boilerplate ("write clean code")
- **MUST** include a directory map that tells the agent exactly where to find context
- **MUST** follow the llms.txt pattern (H1 + blockquote + sections)
- **MUST NOT** duplicate information that belongs in rules, skills, or docs
- **IF** a project also uses `CLAUDE.md` or `GEMINI.md` → `AGENTS.md` takes precedence as the universal standard
- **IF** an IDE doesn't read AGENTS.md natively → sync its content to the IDE-specific context file
