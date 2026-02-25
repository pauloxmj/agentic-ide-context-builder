---
name: agentic-ide-context-global-updater
description: Use this skill whenever requested to update, create, or refactor global rules, workflows, or agent skills in their respective global IDE directories. It ensures compliance with the core agentic IDE architecture guidelines globally.
---

# Global Agentic IDE Context Updater Skill

This skill ensures that all changes to global AI agent context files strictly follow the open standard architecture, maintaining correct YAML structures and synchronization across all global IDE configurations.

## Context Prerequisites

Before executing, identify the current IDE's global directory (e.g., `~/.gemini/antigravity`, `~/.kilocode`, `~/.copilot`). In these instructions, this is referred to as `[IDE_FOLDER]`.

Start gathering context by reading the entrypoints to the knowledge base within the `[IDE_FOLDER]`:
- `[IDE_FOLDER]/README.md`
- `[IDE_FOLDER]/AGENTS.md`
- `[IDE_FOLDER]/ide-targets/` (Consult the file specific to the current IDE)

## Source of Truth
- **Concepts**: Use `[IDE_FOLDER]/concepts/` for high-level architectural rules (Rules, Skills, Workflows).
- **Templates**: Use `[IDE_FOLDER]/templates/` as the drafting source for all new files.
- **IDE Quirks**: Consult `[IDE_FOLDER]/ide-targets/` to handle platform-specific formatting.

## Scope and RAC Integration
- **Strict Scope**: This skill MUST only be used to update **user-level global configurations**.
- **Path Resolution**: Always resolve `[IDE_FOLDER]` to the actual folder used by the current IDE.

## Multi-IDE Synchronization Constraint
The user relies on multiple global agentic IDE configurations. Therefore, it requires full synchronization. Whenever you make a change, you MUST replicate it across all environments while adhering to their platform-specific paradigms.

### Standard Targets
- **Antigravity**: `~/.gemini/antigravity/`
- **Kilo Code**: `~/.kilocode/`
- **GitHub Copilot**: `~/.copilot/`

### Global Rule Consolidation (Copilot)
GitHub Copilot uses a single `copilot-instructions.md` for global rules. When updating global rules, you must either concatenate them or provide a distilled summary including the latest changes into `~/.copilot/copilot-instructions.md`.

## Core Execution Invariants
1. **Always Sync Globally**: Never update one global IDE directory without immediately mirroring or consolidating the update to ALL other targets.
2. **Follow Architectural Standards**:
   - **Rules**: Keep under 500 lines. Focus on cognitive guardrails, not linter rules.
   - **Skills**: Must include `SKILL.md` with proper frontmatter. Identifier must match directory name.
   - **Workflows**: Sequence actions clearly. Focus on reproducibility.
3. **Always Include Frontmatter**: Ensure markdown files utilize the correct YAML frontmatter required by the open standard.
4. **Always Verify**: Verify your formatting and synchronization across ALL global directories before concluding the task.
