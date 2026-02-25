# Agent Skills Open Standard

<system_context>
This is file `general/02-agent-skills.md`.
It is a comprehensive guide to understanding the Agent Skills open specification (https://agentskills.io).
</system_context>

## What Are Agent Skills?

Skills are **portable, version-controlled packages** that teach AI agents how to perform domain-specific tasks. A skill is a folder containing a `SKILL.md` file with metadata and instructions the agent follows when the skill is relevant.

Skills follow the [Agent Skills](https://agentskills.io) open standard, which works across multiple AI tools.

### Key Characteristics

- **Progressive disclosure**: Only metadata is loaded at startup; full instructions load on demand.
- **Portable**: Works across any agent that implements the Agent Skills specification.
- **Self-documenting**: A `SKILL.md` file is both the instruction and the documentation.
- **Extensible**: Can include scripts (`scripts/`), templates (`assets/`), and detailed docs (`references/`).

---

## Technical Integration Approaches

<integration-approaches>
There are two main approaches an IDE might take to integrate skills:

1. **Filesystem-based agents**: Operate within a computer environment (bash/unix) and represent the most capable option. Skills are activated when models issue shell commands like `cat /path/to/my-skill/SKILL.md`. Bundled resources are accessed through shell commands.
2. **Tool-based agents**: Function without a dedicated computer environment. Instead, they implement custom tools allowing models to trigger skills and access bundled assets.
</integration-approaches>

---

## SKILL.md Format

Every skill requires a `SKILL.md` file with **YAML frontmatter** followed by **Markdown content**.

> **Starter Files**: For complete skill packages utilizing the `<review_plan>` Think-Then-Do structure and the Orchestrator mode, see the `templates/global/skills/` and `templates/project/skills/` directories.

### Minimal Example

<example title="Minimal SKILL.md">
```yaml
---
name: code-review
description: Reviews code changes for bugs, style issues, and best practices. Use when reviewing PRs or checking code quality.
---

# Code Review

When reviewing code, follow these steps:

1. **Correctness**: Does the code do what it's supposed to?
2. **Edge cases**: Are error conditions handled?
3. **Style**: Does it follow project conventions?
4. **Performance**: Are there obvious inefficiencies?
```
</example>

### Frontmatter Fields

<frontmatter-reference>
#### Required Fields
| Field | Constraints | Description |
|-------|-------------|-------------|
| `name` | Max 64 chars. Lowercase, numbers, hyphens. Must match directory name. | Unique identifier for the skill. Cannot start/end with hyphen or have consecutive hyphens. |
| `description` | Max 1024 chars | What the skill does and when to use it. **This is what the agent sees to decide relevance.** |

#### Optional Fields
| Field | Description |
|-------|-------------|
| `license` | License name or reference to bundled file |
| `compatibility` | Max 500 chars. Environment requirements (e.g., "Requires Node.js 18+") |
| `metadata` | Arbitrary key-value pairs (author, version, etc.) |
| `allowed-tools` | Space-delimited list of pre-approved tools |
</frontmatter-reference>

---

## Skill Directory Structure

<example title="Full Skill Content Directory">
```
my-skill/
├── SKILL.md           # Required: instructions + metadata
├── scripts/           # Optional: executable code the agent can run
│   ├── deploy.sh
│   └── validate.py
├── references/        # Optional: detailed docs loaded on demand
│   └── REFERENCE.md
├── examples/          # Optional: reference implementations
│   └── sample.md
└── assets/            # Optional: templates, config files, data
    └── config-template.json
```
</example>

### Progressive Disclosure

Skills are optimized for context efficiency:
1. **Metadata** (~100 tokens): `name` and `description` loaded at startup for all skills.
2. **Instructions** (<5000 tokens recommended): Full `SKILL.md` body loaded when activated.
3. **Resources** (as needed): Files in `scripts/`, `references/`, `assets/` loaded only when needed via relative paths (e.g., `references/REFERENCE.md`).

> **Keep `SKILL.md` under 500 lines.** Move detailed reference material to separate files one-level deep.

<instruction>
Proceed to `general/03-rules-concepts.md` to understand persistent agent context.
</instruction>
