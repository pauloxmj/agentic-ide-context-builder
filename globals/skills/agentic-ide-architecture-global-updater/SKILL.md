---
name: agentic-ide-architecture-global-updater
description: Use this skill whenever requested to update, create, or refactor global rules, workflows, or agent skills in ~/.gemini/antigravity, ~/.kilocode, and ~/.copilot. It ensures compliance with the core agentic IDE architecture guidelines globally.
---

# Global Agentic IDE Architecture Updater Skill

This skill ensures that all changes to global AI agent context files strictly follow the open standard architecture, maintaining correct YAML structures and synchronization across global IDE configurations (~/.gemini/antigravity, ~/.kilocode, and ~/.copilot).

## Context Prerequisites

Start gathering context by reading the entrypoints to the knowledge base:
- `/home/paulo/Repositories/agentic-architecture-builder/README.md`
- `/home/paulo/Repositories/agentic-architecture-builder/AGENTS.md`
- `/home/paulo/Repositories/agentic-architecture-builder/docs/ide-specific/03-github-copilot.md`

## Multi-IDE Synchronization Constraint
The user relies on multiple global agentic IDE configurations. Therefore, it requires full synchronization. Whenever you make a change, you MUST replicate it across all environments while adhering to their platform-specific paradigms.

Read the platform mechanics for both IDEs before modifying directories:
- **Kilo Code**: `~/.kilocode/` (Rules, Workflows, Skills)
- **Antigravity**: `~/.gemini/antigravity/` (Rules, Workflows, Skills)
- **GitHub Copilot**: `~/.copilot/` (Instructions, Skills)

### Global Rule Consolidation (Copilot)
GitHub Copilot uses a single `copilot-instructions.md` for global rules. When updating global rules, you must either concatenate them or provide a distilled summary including the latest changes into `~/.copilot/copilot-instructions.md`.

## Core Execution Invariants
1. **Always Sync Globally**: Never update a global IDE directory without immediately mirroring or consolidating the update to ALL other targets (Antigravity, Kilo Code, Copilot).
2. **Always Include Frontmatter**: Ensure markdown files utilize the correct YAML frontmatter required by the open standard (e.g., `description` and `globs` for rules; `name` and `description` for skills).
3. **Always Verify**: Verify your formatting and synchronization across both global directories before concluding the task.
