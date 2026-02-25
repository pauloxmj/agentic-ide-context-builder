---
name: agentic-ide-global-updater
description: Use this skill whenever requested to update, create, or refactor global rules, workflows, or agent skills in ~/.gemini/antigravity and ~/.kilocode. It ensures compliance with the core agentic IDE architecture guidelines globally.
---

# Global Agentic IDE Architecture Updater Skill

This skill ensures that all changes to global AI agent context files strictly follow the open standard architecture, maintaining correct YAML structures and synchronization across both global IDE configurations (`~/.gemini/antigravity` and `~/.kilocode`).

## Context Prerequisites

Start gathering context by reading the entrypoints to the knowledge base:
- `/home/paulox/Repositories/agentic-ide-architecture-builder/README.md`
- `/home/paulox/Repositories/agentic-ide-architecture-builder/AGENTS.md`

## Dual-IDE Synchronization Constraint
The user relies on multiple global agentic IDE configurations. Therefore, it requires full synchronization. Whenever you make a change, you MUST replicate it identically across both environments while adhering to their platform-specific paradigms.

Read the platform mechanics for both IDEs before modifying directories:
- **Kilo Code**: `/home/paulox/Repositories/agentic-ide-architecture-builder/docs/ide-specific/01-kilocode.md`
  - Targets: `~/.kilocode/rules/`, `~/.kilocode/workflows/`, `~/.kilocode/skills/`
- **Antigravity**: `/home/paulox/Repositories/agentic-ide-architecture-builder/docs/ide-specific/02-antigravity.md`
  - Targets: `~/.gemini/antigravity/rules/`, `~/.gemini/antigravity/workflows/`, `~/.gemini/antigravity/skills/`

## Core Execution Invariants
1. **Always Sync Globally**: Never update a `~/.gemini/antigravity` file without immediately mirroring the exact identical update to the corresponding `~/.kilocode` file (and vice versa).
2. **Always Include Frontmatter**: Ensure markdown files utilize the correct YAML frontmatter required by the open standard (e.g., `description` and `globs` for rules; `name` and `description` for skills).
3. **Always Verify**: Verify your formatting and synchronization across both global directories before concluding the task.
