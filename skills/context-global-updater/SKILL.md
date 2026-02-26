---
name: context-global-updater
description: Use this skill whenever requested to update, create, or refactor global rules, workflows, or agent skills in their respective global IDE directories. Ensures compliance with the agentic IDE architecture guidelines across all IDEs.
---

# Global Context Updater Skill

This skill ensures that all changes to global AI agent context files (user-level, across all projects) strictly follow the open standard architecture and stay synchronized across all supported IDE configurations.

## Context Prerequisites

Before executing, read from the context-builder knowledge base:
1. **Knowledge**: Read `knowledge/rules-architecture.md`, `knowledge/skills-architecture.md`, or `knowledge/workflows-architecture.md` depending on the artifact type
2. **IDE Targets**: Read ALL files in `ide-targets/` — global changes must sync across all IDEs
3. **Templates**: Read the matching template from `templates/` for correct formatting

The builder knowledge base location:
- **In-project**: `.agent/builders/agentic-ide-context-builder/`
- **Standalone repo**: `/home/paulox/Repositories/agentic-ide-context-builder/`

## Execution Steps

### 1. Analysis Phase
- Identify which global directories exist on this system
- Determine the artifact type (rule, workflow, skill) and scope

### 2. Write to Source of Truth
- Write the canonical version in the primary global directory first
- Use structured markdown with YAML frontmatter

### 3. Sync Across All IDEs
Replicate the change to all supported global directories, adapting format as needed:

| IDE | Global Path | Format Notes |
|-----|-------------|--------------|
| **Kilo Code** | `~/.kilocode/` | Standard `.md` — direct copy |
| **Antigravity** | `~/.gemini/antigravity/` | Standard `.md` — direct copy |
| **Cursor** | `~/.cursor/` | Convert `.md` → `.mdc` (add activation frontmatter) |
| **GitHub Copilot** | Settings-level | Aggregate into `copilot-instructions.md` |

### 4. Verification
- Confirm YAML frontmatter is present and correct in all copies
- Verify multi-IDE synchronization is complete
- Ensure format adaptations (`.mdc`, `paths:`, aggregated files) are correct

## AI Rules

- **MUST** sync global changes across ALL supported IDE directories
- **MUST** adapt format per IDE target requirements (see `ide-targets/`)
- **MUST** use templates from the builder for consistent formatting
- **MUST NOT** place stack-specific instructions in global scope
- **MUST NOT** touch project-level configurations — use `context-project-updater` for that
