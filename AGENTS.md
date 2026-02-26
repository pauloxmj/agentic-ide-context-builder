---
description: AI-first knowledge base for creating, managing, and synchronizing AI agent configurations (rules, workflows, skills) across IDEs.
---

# Agentic IDE Context Builder

> AI Architecture Expert knowledge base for creating, modifying, and synchronizing agent configurations — rules, workflows, and skills — across Kilo Code, Antigravity (Gemini), GitHub Copilot, and Cursor.

## Knowledge Base Map

Use this map to locate the context you need. Read files in order of relevance to your current task.

| Directory | Purpose | When to Read |
|-----------|---------|--------------|-
| `knowledge/` | Universal concepts — rules, skills, workflows, context, MCP, AGENTS.md | Before creating or modifying any agent configs |
| `ide-targets/` | IDE-specific paths, activation modes, formats, sync quirks | When targeting a specific IDE |
| `templates/` | Production-ready scaffolds for rules, workflows, and skills | When creating new agent config files |
| `skills/` | Builder-specific skills for global and project-level updates | When invoked as an agent skill |

### Knowledge Files
- [rules-architecture.md](knowledge/rules-architecture.md) → Rules: scope types, activation modes, formatting, best practices
- [skills-architecture.md](knowledge/skills-architecture.md) → Skills: SKILL.md standard, progressive disclosure, decision matrix
- [workflows-architecture.md](knowledge/workflows-architecture.md) → Workflows: runbooks, turbo annotations, orchestrator patterns
- [context-architecture.md](knowledge/context-architecture.md) → Context vectors, truncation, `.agent/` source-of-truth pattern
- [agents-md-standard.md](knowledge/agents-md-standard.md) → AGENTS.md convention, IDE compatibility
- [mcp-integration.md](knowledge/mcp-integration.md) → MCP architecture, primitives, cross-IDE config

### IDE Targets
- [kilocode.md](ide-targets/kilocode.md) → Kilo Code: custom modes, orchestration, mode-specific rules
- [antigravity.md](ide-targets/antigravity.md) → Antigravity (Gemini): settings.json layers, context file config
- [cursor.md](ide-targets/cursor.md) → Cursor: 4 rule activation types, .mdc format, background agents
- [github-copilot.md](ide-targets/github-copilot.md) → Copilot: 3 instruction types, prompt files, coding agent

### Templates
- [global-rule.md](templates/global-rule.md) → Scaffold for global rules
- [project-rule.md](templates/project-rule.md) → Scaffold for project rules
- [workflow.md](templates/workflow.md) → Scaffold for workflows
- [skill/SKILL.md](templates/skill/SKILL.md) → Scaffold for agent skills

---

## When to Create Rules vs. Skills vs. Workflows

| Situation | Create |
|-----------|--------|
| Persistent constraint, naming convention, guardrail | **Rule** |
| Reusable domain expertise, complex multi-step tasks | **Skill** |
| Sequential procedure with specific commands | **Workflow** |
| Linter/formatter can enforce it | **Nothing** — defer to tooling |

---

## Standard Operating Procedures

This builder supports three workflows. Use the decision table to pick the right one.

### When to Use Which Workflow

| Situation | Workflow |
|-----------|----------|
| No agent configs exist for this IDE yet | **Implement** — scaffold from scratch |
| Configs exist but a rule/skill/workflow is wrong or outdated | **Modify** — edit specific files |
| Codebase changed (new deps, architecture changes) | **Update** — sync configs to match code |

### Workflow 1: Implement (Scaffold New Configs)

1. **Read Knowledge** — Read relevant files in `knowledge/` for the artifact type (rule, skill, workflow)
2. **Identify IDE Target** — Read the corresponding file in `ide-targets/` for paths, formats, and quirks
3. **Identify Scope** — Global (user-level, all projects) or project (codebase-specific)
4. **Select Template** — Read the matching template from `templates/`
5. **Execute** — Create files following the template structure and IDE-specific requirements
6. **Sync** — If global, replicate across all IDE directories. If project, ensure `.agent/` is the source of truth

### Workflow 2: Modify (Edit Existing Configs)

1. **Read the target file** — Understand its current content and structure
2. **Read `knowledge/`** — Ensure edits follow architectural standards
3. **Make targeted edits** — Change only the sections that are incorrect or outdated
4. **Preserve structure** — Do not reorganize unless explicitly asked
5. **Sync** — Propagate changes to IDE-specific folders

### Workflow 3: Update (Sync Configs to Code Changes)

1. **Identify what changed** — Architecture? Dependencies? Conventions?
2. **Update the matching config** — Rule, skill, or workflow
3. **Check for cascading changes** — If a rule changed, do skills or workflows also need updating?
4. **Sync** — Propagate changes to IDE-specific folders
5. **Flag ambiguity** — If the code change is unclear, flag to human rather than guessing

---

## AI Rules

- **MUST** read relevant `knowledge/` files before creating any agent artifact
- **MUST** consult `ide-targets/` when targeting a specific IDE
- **MUST** use template structures from `templates/` — never invent artifact formats
- **MUST** use YAML frontmatter on every generated `.md` file
- **MUST** keep rules under 500 lines — move detailed references to separate files
- **MUST** ensure skill directory names match the `name` field in SKILL.md frontmatter
- **MUST** use `.agent/` as the source of truth for project-level configs
- **MUST NOT** place stack-specific instructions in global scope
- **MUST NOT** duplicate rules that a linter/formatter can enforce autonomously
- **MUST NOT** hallucinate IDE paths — only use paths defined in `ide-targets/`
- **MUST NOT** mix global and project scope in a single file
- **MUST NOT** sync `.agent/builders/` to other IDE folders — builders are reference-only
- **IF** change is global → sync across all IDE directories (Kilo Code, Antigravity, Cursor)
- **IF** change is project-level → write to `.agent/` first, then sync to IDE-specific folders
- **IF** an IDE has a unique format requirement (e.g., Cursor `.mdc`) → adapt the content accordingly
- **IF** unsure about an IDE's capability → read its official docs URL from the ide-target file
