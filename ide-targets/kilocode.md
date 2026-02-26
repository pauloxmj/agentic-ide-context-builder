---
description: IDE-specific path mappings, rule activation modes, custom modes, and capabilities for Kilo Code (VS Code extension).
category: ide-target
---

# Kilo Code

VS Code extension providing multi-model AI coding assistance with native mode orchestration and full filesystem access.

## Path Mapping

| Artifact | Project Path | Global Path |
|----------|-------------|-------------|
| **Rules** | `.kilocode/rules/` | `~/.kilocode/rules/` |
| **Mode-specific Rules** | `.kilocode/rules-[mode-name]/` | `~/.kilocode/rules-[mode-name]/` |
| **Workflows** | `.kilocode/workflows/` | `~/.kilocode/workflows/` |
| **Skills** | `.kilocode/skills/` | `~/.kilocode/skills/` |
| **Mode-specific Skills** | `.kilocode/skills-[mode-name]/` | `~/.kilocode/skills-[mode-name]/` |
| **Custom Instructions** | Extension Settings UI | Extension Settings UI |

## Rule Activation

| Type | Mechanism |
|------|-----------|
| **Global Custom Instructions** | Text set in extension settings — always included in every prompt |
| **Mode-Specific Custom Instructions** | Instructions set per mode in extension settings |
| **Project Rules** | `.md` files in `.kilocode/rules/` — always loaded for the workspace |
| **Mode-Specific Rules** | `.md` files in `.kilocode/rules-[mode-name]/` — loaded only in matching mode |

Rules are standard `.md` files with YAML frontmatter. No proprietary format needed.

## Format Requirements

- **File extension**: `.md` (standard markdown)
- **Frontmatter**: `description` field (recommended for discoverability)
- **Mode-specific scoping**: Use `rules-[mode-name]/` and `skills-[mode-name]/` directories for mode-restricted artifacts

## Custom Modes (Orchestration)

Kilo Code natively supports creating restricted sub-agents (modes) via YAML definitions:

- Modes are defined in extension settings as JSON/YAML
- Each mode specifies: name, slug, allowed tools, role prompt, and task boundaries
- The primary agent uses `new_task()` to spawn isolated tasks in specialized modes
- Modes cascade rules: global → mode-specific → project → project-mode-specific

### Built-in Modes
- **Code** — default coding mode
- **Architect** — planning only, no file edits
- **Ask** — question answering, no tool use
- **Debug** — focused debugging with terminal access

## Workflow Support

- Workflows are `.md` files in `.kilocode/workflows/`
- Requires `description` in YAML frontmatter
- Supports `// turbo` and `// turbo-all` step annotations for auto-execution
- Invoked via slash commands matching the filename

## Sync from `.agent/`

| Source | Destination | Conversion |
|--------|------------|------------|
| `.agent/rules/` | `.kilocode/rules/` | Direct copy (no conversion needed) |
| `.agent/skills/` | `.kilocode/skills/` | Direct copy |
| `.agent/workflows/` | `.kilocode/workflows/` | Direct copy |

## LLM-Friendly Documentation

- **LLM Docs**: `https://kilo.ai/docs/llms.txt`
- **Usage**: Parse for the latest custom modes YAML syntax, API definitions, and tool references

## AI Rules

- **MUST** use `.md` file extension for all artifacts
- **MUST** use `rules-[mode-name]/` for mode-specific rules (e.g., `rules-docs-writer/`)
- **MUST** include `description` in YAML frontmatter for all workflow files
- **IF** syncing from `.agent/` → copy directly without format conversion
- **IF** creating a new mode → define its allowed tools, role prompt, and tool boundaries
- **IF** unsure about orchestrator syntax → parse `https://kilo.ai/docs/llms.txt`
