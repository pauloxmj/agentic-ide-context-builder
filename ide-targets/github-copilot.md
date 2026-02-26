---
description: IDE-specific path mappings, 3 instruction types, coding agent support, and capabilities for GitHub Copilot.
category: ide-target
---

# GitHub Copilot

GitHub's AI coding assistant integrated across VS Code, JetBrains, GitHub.com, and the CLI. Supports repository-wide, path-specific, and agent instructions.

## Path Mapping

| Artifact | Project Path | Global Path |
|----------|-------------|-------------|
| **Repository-wide Instructions** | `.github/copilot-instructions.md` | — |
| **Path-specific Instructions** | `.github/instructions/*.instructions.md` | — |
| **Agent Instructions** | `AGENTS.md` (anywhere in repo tree) | — |
| **Prompt Files** | `.github/prompts/*.prompt.md` | — |
| **Organization Instructions** | GitHub Organization settings → Copilot | — |

## 3 Instruction Types

| Type | File | Scope |
|------|------|-------|
| **Repository-wide** | `.github/copilot-instructions.md` | Applied to all Copilot requests in the repository |
| **Path-specific** | `.github/instructions/NAME.instructions.md` | Applied when working on files matching YAML frontmatter globs |
| **Agent** | `AGENTS.md` (nearest in directory tree) | Used by coding agents; supports `CLAUDE.md` and `GEMINI.md` fallbacks |

### Path-specific Instructions Format

```markdown
---
applyTo: "src/**/*.ts"
---
# TypeScript Guidelines
- Use strict mode
- Prefer interfaces over type aliases
```

The `applyTo` field accepts glob patterns. When Copilot works on matching files, these instructions supplement the repository-wide instructions.

## Rule Resolution Order

Instructions are applied in this order (highest to lowest priority):

1. Organization instructions (Copilot Enterprise)
2. Repository-wide instructions (`copilot-instructions.md`)
3. Path-specific instructions (matching `.instructions.md` files)
4. Personal instructions (user-level settings)
5. Chat prompt context

## Coding Agent (2025-2026)

Copilot's coding agent operates in a sandboxed environment and supports:

- **`AGENTS.md`**: Reads agent instructions from nearest file in directory tree
- **`CLAUDE.md` / `GEMINI.md`**: Alternative root-level instruction files
- **Prompt Files**: `.github/prompts/*.prompt.md` for reusable prompts (supports `#file` references)
- **Autonomous PR creation**: Creates commits and opens pull requests

## Prompt Files

Reusable prompt templates stored in `.github/prompts/`:

```markdown
---
description: Generate a React component with tests
---
Create a new React component at #file:src/components/
Include unit tests using Vitest
Follow the patterns in #file:src/components/Button.tsx
```

## Sync from `.agent/`

| Source | Destination | Conversion |
|--------|------------|------------|
| `.agent/rules/` | `.github/copilot-instructions.md` | Aggregate all rules into a single file |
| `.agent/rules/*.md` (with globs) | `.github/instructions/*.instructions.md` | Convert `globs` → `applyTo` frontmatter |
| `.agent/skills/` | Not directly supported | Reference via AGENTS.md |
| `.agent/workflows/` | `.github/prompts/*.prompt.md` | Convert workflows to prompt file format |

> **IMPORTANT**: Copilot aggregates rules into a single `copilot-instructions.md`. When syncing multiple rule files from `.agent/`, concatenate them with clear section headers.

## LLM-Friendly Documentation

- **Official Docs**: `https://docs.github.com/en/copilot`
- **No standardized `llms.txt`** — use the full docs URL above

## AI Rules

- **MUST** aggregate multiple rules into a single `copilot-instructions.md`
- **MUST** use `.instructions.md` suffix with `applyTo` frontmatter for path-specific instructions
- **MUST** use `AGENTS.md` for coding agent instructions
- **IF** syncing from `.agent/` → aggregate individual rule files into `copilot-instructions.md`
- **IF** path-specific rules exist → create corresponding `.instructions.md` files in `.github/instructions/`
- **IF** creating prompt files → store in `.github/prompts/` with `.prompt.md` extension
