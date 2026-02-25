---
name: agentic-ide-context-project-updater
description: Use this skill whenever requested to update, create, or refactor project-level agent rules, workflows, or skills within folders like .agent, .github, .agents, _agent, or _agents. It ensures compliance with the core agentic IDE architecture guidelines within a project's context.
---

# Project Agentic IDE Context Updater Skill

This skill ensures that all changes to project-level AI agent context files (located in `.agent/`, `.agents/`, etc.) strictly follow the open standard architecture, maintain correct YAML structures, and align with the project's specific requirements.

## Context Prerequisites

Before executing, identify the current IDE's global directory (e.g., `~/.gemini/antigravity`, `~/.kilocode`, `~/.copilot`). In these instructions, this is referred to as `[IDE_FOLDER]`.

Start gathering context by reading the project's entrypoint and the central knowledge base:
- `[REPOSITORY]/AGENTS.md` (Project Entrypoint - Defines target project conventions)
- `[GLOBAL_KB_REPO]/AGENTS.md` (Master Knowledge Base Entrypoint)
- `[GLOBAL_KB_REPO]/README.md` (Global Architecture Overview)
- `[GLOBAL_KB_REPO]/RAC-SCHEMA.md` (Strict XML parsing boundaries)
- `[GLOBAL_KB_REPO]/ide-targets/` (Consult the file specific to the current IDE for platform-specific quirks)

## Source of Truth
- **Schema Validation**: Parse `[GLOBAL_KB_REPO]/RAC-SCHEMA.md` for deterministic parsing of boundaries.
- **Concepts**: Use `[GLOBAL_KB_REPO]/concepts/` for universal architectural patterns.
- **Templates**: Use `[GLOBAL_KB_REPO]/templates/` for standard rule, workflow, and skill structures.
- **Project Structure**: Respect the local project's existing `.agent/` or `.agents/` folder structure.

## Scope and RAC Integration
- **Strict Scope**: This skill MUST only be used to update **project-level configurations** within the specific project repository the user is actively prompting you from. It should never touch global user directories or other projects on the system.
- **Project Context**: Ensure changes are tailored to the specific target project's tech stack and conventions defined in `[REPOSITORY]/AGENTS.md`.

## Targets
This skill targets the following locations within the current project root only (`[REPOSITORY]`):
- `.agent/`, `.agents/`, `_agent/`, or `_agents/`
- `.github/` (Copilot Specific)

Specifically updating:
- `rules/*.md` (Standard Rules)
- `workflows/*.md` (Standard Workflows)
- `skills/*/SKILL.md` (Standard & Copilot Skills)
- `.github/copilot-instructions.md` (Copilot Aggregate)
- `.github/instructions/*.instructions.md` (Copilot Path-specific)
- `AGENTS.md` (Core Entrypoint)

## Core Execution Invariants
1. **Follow Project Patterns**: Ensure all updates align with existing architectural patterns found in the project's agent folder.
2. **Mirror Rules for Copilot**: 
   - When modifying `rules/*.md`, aggregate high-level rules into `.github/copilot-instructions.md`.
   - Mirror relevant path-specific instructions into `.github/instructions/` using the `.instructions.md` suffix.
3. **Always Include Frontmatter**: Ensure markdown files utilize the correct YAML frontmatter required by the open standard (e.g., `description` and `globs` for rules; `name` and `description` for skills).
4. **Follow Constraints**:
   - **Rules**: Keep under 500 lines. Focus on project conventions.
   - **Skills**: Must be portable. Identifier must match directory name.
5. **Always Verify**: Verify your formatting and compliance within the project before concluding the task.
