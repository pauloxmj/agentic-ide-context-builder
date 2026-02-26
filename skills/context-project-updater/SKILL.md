---
name: context-project-updater
description: Use this skill whenever requested to update, create, or refactor project-level agent rules, workflows, or skills within folders like .agent, .github, .agents, _agent, or _agents. Ensures compliance with the agentic IDE architecture guidelines within a project's context.
---

# Project Context Updater Skill

This skill ensures that all changes to project-level AI agent context files (in `.agent/`, `.agents/`, etc.) strictly follow the open standard architecture, maintain correct YAML structures, and align with the project's specific requirements.

## Context Prerequisites

Before executing, read:
1. **Project entrypoint**: `[REPOSITORY]/AGENTS.md` — defines target project conventions
2. **Builder knowledge**: Relevant files from `.agent/builders/agentic-ide-context-builder/knowledge/`
3. **IDE targets**: The file in `ide-targets/` specific to the current IDE
4. **Templates**: The matching template from `templates/`

## Source of Truth: `.agent/` First

The `.agent/` folder is the **strict source of truth** for project-level configurations:
1. Write all changes to `.agent/` FIRST
2. Then sync outward to IDE-specific folders, adapting format as needed

## Sync Targets

This skill updates the following locations within the current project root:

| IDE | Project Path | Format Notes |
|-----|-------------|--------------|
| **Universal** | `.agent/rules/`, `.agent/skills/`, `.agent/workflows/` | Source of truth — standard `.md` |
| **Antigravity** | Reads from `.agent/` directly | No separate copy needed |
| **Kilo Code** | `.kilocode/rules/`, `.kilocode/skills/`, `.kilocode/workflows/` | Standard `.md` copies |
| **Cursor** | `.cursor/rules/*.mdc`, `.cursor/commands/` | Convert `.md` → `.mdc` format |
| **GitHub Copilot** | `.github/copilot-instructions.md`, `.github/instructions/` | Aggregate rules |

## Execution Steps

### 1. Identify Scope
- Determine the artifact type (rule, workflow, skill)
- Confirm this is a project-level change (not global)

### 2. Write to `.agent/`
- Create or modify the file in `.agent/rules/`, `.agent/skills/`, or `.agent/workflows/`
- Use the correct template and include YAML frontmatter

### 3. Sync to IDE-Specific Folders
- Replicate to downstream IDE folders, adapting format per `ide-targets/` requirements
- For Copilot: aggregate high-level rules into `.github/copilot-instructions.md` and mirror path-specific rules into `.github/instructions/`

### 4. Verify
- Confirm `.agent/` has the canonical version
- Check all synced copies have correct format for their target IDE
- Ensure frontmatter is present and valid

## AI Rules

- **MUST** write to `.agent/` first — it is the single source of truth
- **MUST** sync changes to all relevant IDE-specific folders in the project
- **MUST** follow existing project patterns found in the agent folder
- **MUST** include correct YAML frontmatter (`description`, `globs` for rules; `name`, `description` for skills)
- **MUST** keep rules under 500 lines
- **MUST NOT** sync `.agent/builders/` to other IDE folders — builders are reference-only knowledge bases exclusive to `.agent/`
- **MUST NOT** touch global user directories — use `context-global-updater` for that
- **MUST NOT** touch other projects on the system
- **IF** modifying rules → aggregate into `.github/copilot-instructions.md` for Copilot
- **IF** path-specific rules exist → mirror into `.github/instructions/` with `.instructions.md` suffix
