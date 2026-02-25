---
name: agentic-ide-architecture-project-updater
description: Use this skill whenever requested to update, create, or refactor project-level agent rules, workflows, or skills within folders like .agent, .github, .agents, _agent, or _agents. It ensures compliance with the core agentic IDE architecture guidelines within a project's context.
---

# Project Agentic IDE Architecture Updater Skill

This skill ensures that all changes to project-level AI agent context files (located in `.agent/`, `.agents/`, etc.) strictly follow the open standard architecture, maintain correct YAML structures, and align with the project's specific requirements.

## Context Prerequisites

Start gathering context by reading the entrypoints to the knowledge base. If you are in a different environment, resolve these paths relative to the current project root:
- `[PROJECT_ROOT]/README.md`
- `[PROJECT_ROOT]/AGENTS.md`
- `[PROJECT_ROOT]/docs/ide-specific/03-github-copilot.md`

## Environment Resolution
Before executing any file operations, you MUST:
1. Detect the current project root absolute path.
2. Replace `[PROJECT_ROOT]` in all instructions with this path.
3. Ensure you are working within the correct repository context (`agentic-ide-context-builder`).

## Targets
This skill targets the following locations within the current project:
- `.agent/`, `.agents/`, `_agent/`, or `_agents/`
- `.github/` (Copilot Specific)
- Specifically:
  - `rules/*.md` (Standard)
  - `.github/copilot-instructions.md` (Copilot Aggregate)
  - `.github/instructions/*.instructions.md` (Copilot Path-specific)
  - `workflows/*.md` (Standard)
  - `skills/*/SKILL.md` (Standard & Copilot)
  - `AGENTS.md`
  - `task.md`, `implementation_plan.md`, `walkthrough.md` (Architectural docs)

## Core Execution Invariants
1. **Follow Project Patterns**: Ensure all updates align with existing architectural patterns found in the project's agent folder.
2. **Always Include Frontmatter**: Ensure markdown files utilize the correct YAML frontmatter required by the open standard (e.g., `description` and `globs` for rules; `name` and `description` for skills).
3. **Copilot Mirroring Logic**: When modifying `.agent/rules/*.md`, ensure you mirror relevant instructions into `.github/instructions/` using the `.instructions.md` suffix for path-specific Copilot context. Aggregate high-level rules into `.github/copilot-instructions.md`.
4. **Sync with Global Guidelines**: While project-specific, ensure changes don't contradict the core agentic architecture principles defined in the `agentic-ide-context-builder` repository.
5. **Always Verify**: Verify your formatting and compliance before concluding the task.
