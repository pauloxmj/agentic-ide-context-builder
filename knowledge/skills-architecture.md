---
description: Architectural standard for portable Agent Skills — version-controlled capability packages, SKILL.md format, progressive disclosure, and best practices for writing effective skills.
category: knowledge
---

# Skills Architecture

Portable, version-controlled capability packages that teach an agent how to perform domain-specific tasks. Follows the `agentskills.io` standard. Skills provide on-demand deep expertise — loaded only when invoked, not pinned to every request like rules.

## Structure

A skill is a folder containing:

```
skill-name/
├── SKILL.md          ← Mandatory: metadata (frontmatter) + instructions
├── scripts/          ← Optional: bash/python automation scripts
├── references/       ← Optional: detailed reference docs loaded on-demand
├── assets/           ← Optional: images, configs, data files
└── examples/         ← Optional: sample implementations
```

## Progressive Disclosure

| Phase | Tokens | What's Loaded |
|-------|--------|---------------|
| **Startup** | ~100 | Frontmatter metadata only (name, description) |
| **Invocation** | <5000 | Full `SKILL.md` body |
| **Deep dive** | Variable | External references in subdirectories, only as needed |

## SKILL.md Frontmatter Rules

- `name` (Required): Unique lowercase identifier — must match directory name, max 64 chars
- `description` (Required): What the skill does — max 1024 chars, used by the system for relevance matching

## How to Write Effective Skills

### Content Structure

A well-structured SKILL.md contains:
1. **YAML frontmatter** — `name` and `description` (both required)
2. **Lead summary** — 1-2 sentences stating what this skill teaches
3. **Context Prerequisites** — What knowledge files or docs the agent should read first
4. **Execution Steps** — Numbered steps for performing the skill's task
5. **Validation Checklist** — How to verify the output is correct

### When to Create a Skill vs. a Rule vs. a Workflow

| Create a Skill | Create a Rule | Create a Workflow |
|----------------|---------------|-------------------|
| Reusable domain expertise | Persistent constraints | Sequential one-off procedure |
| Complex multi-step tasks with judgment | Simple yes/no enforcement | Step-by-step runbook |
| Needs reference material (scripts, examples) | Needs to survive context truncation | Needs `// turbo` auto-run annotations |
| Invoked on-demand, not always | Always loaded, pinned to every request | Triggered by slash command |

### Anti-Patterns to Avoid

| Anti-Pattern | Why It Fails |
|-------------|-------------|
| SKILL.md > 5000 tokens | Bloats context when invoked; use subdirectories for details |
| One-off tasks as skills | Skills should be reusable across sessions |
| Missing `description` in frontmatter | System can't match skill to relevant queries |
| Inlining full reference docs | Defeats progressive disclosure; put in `references/` |
| Directory name ≠ `name` field | Causes path resolution failures |

## Integration Approaches

1. **Filesystem-based**: Agent reads `SKILL.md` and executes bash/python scripts natively
2. **Tool-based**: Agent uses IDE-specific tools to trigger skills without a full unix environment

## Cross-IDE Skill Location

| IDE | Project Skills | Global Skills |
|-----|---------------|---------------|
| **Kilo Code** | `.kilocode/skills/` | `~/.kilocode/skills/` |
| **Antigravity** | `.agent/skills/` | `~/.gemini/antigravity/skills/` |
| **Cursor** | `.cursor/skills/` | `~/.cursor/skills/` |
| **Copilot** | `.github/skills/` | — |

## AI Rules

- **MUST** ensure the skill directory name matches the `name` frontmatter field
- **MUST** keep `SKILL.md` under 5000 tokens for efficient loading
- **MUST** use progressive disclosure — put detailed references in subdirectories, not in SKILL.md
- **MUST** include both `name` and `description` in YAML frontmatter
- **MUST** include execution steps and a validation checklist
- **MUST NOT** create skills for one-off tasks — skills should be reusable across sessions
- **IF** a skill has scripts → place them in `scripts/` subdirectory
- **IF** a skill has reference docs → place them in `references/` subdirectory
