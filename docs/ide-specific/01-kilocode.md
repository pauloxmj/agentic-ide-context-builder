# Kilocode Code Implementation

<system_context>
This is file `ide-specific/01-kilocode.md`.
It details how Kilocode Code implements AI agent concepts like rules, workflows, and skills.
</system_context>

## Custom Rules

Kilocode supports both global and project-specific rules.

### Rule Storage

| Scope | Location |
|-------|----------|
| **Project Rules** | `.kilocode/rules/` |
| **Global Rules** | `~/.kilocode/rules/` |
| **Fallback Method** | Single file `.kilorules` in the root (legacy/fallback) |

**Note**: The directory approach (`.kilocode/rules/`) is heavily preferred. Files within the directory are evaluated recursively and concatenated in alphabetical order.

### Custom Modes & Orchestration

Kilocode allows users to create specialized "personas" called Custom Modes. This enables an **Orchestrator Mode** workflow, where a primary agent breaks down tasks and delegates them to specialized, locked-down sub-agents (e.g., passing architecture to an `architect` mode, and writing tests to a `testing` mode).

You can provide mode-specific rules by organizing them effectively:

<example title="Kilocode Code Custom Mode Structure">
```
.kilocode/
└── rules-docs-writer/       # Kilocode will only load when the user switches to 'docs-writer'
    ├── 01-style-guide.md
    └── 02-formatting.txt
```
</example>

Mode definitions themselves can be defined via YAML, creating powerful locked-down agents that only have access to specific scopes or tools.

## Workflows

Kilocode defines workflows as step-by-step instructions.

### Location

Workflows are generally stored in the `.kilocode/workflows/` directory.

### In-Workflow Capabilities

Kilocode workflows have robust native capabilities built-in for the LLM to call during execution:
- **Built-in tools**: `read_file()`, `search_files()`, `execute_command()`.
- **Mode Switching**: The `new_task()` tool can be used to spawn isolated tasks in specialized modes (e.g., launching an isolated `docs-writer` sub-agent).
- **Tool execution**: The LLM can be instructed to run `gh`, `docker`, or `npm` inside the workflow trajectory.

## Agent Skills

Kilocode fully supports the Agent Skills open standard.

| Scope | Location |
|-------|----------|
| Global (all modes) | `~/.kilocode/skills/` |
| Global (mode-specific) | `~/.kilocode/skills-${mode}/` |
| Project (all modes) | `<project>/.kilocode/skills/` |
| Project (mode-specific) | `<project>/.kilocode/skills-${mode}/` |

Kilocode operates as a **Filesystem-based agent**, meaning that if an LLM is in Kilocode, it has full ability to read the `SKILL.md` file and execute `./scripts/` locally using native terminal commands.

### Model Context Protocol (MCP)

Kilocode natively supports MCP servers. Using the standard configuration, you can attach open-source or proprietary MCP servers to grant the AI immediate, authenticated access to external tools like Jira, PostgreSQL, or your organization's internal APIs.
