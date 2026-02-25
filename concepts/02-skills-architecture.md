---
description: Architectural standard for Agent Skills (agentskills.io).
---

<concept id="skills-architecture">
# Agent Skills Architecture

- **Definition**: Portable, version-controlled capability packages that teach an agent how to perform domain-specific tasks. Follows `agentskills.io` standard.
- **Structure**: A folder containing a mandatory `SKILL.md` file (metadata + instructions) and optional subdirectories (`scripts/`, `references/`, `assets/`, `examples/`).
- **Progressive Disclosure**: Agents load metadata (~100 tokens) at startup, `SKILL.md` body (<5000 tokens) on invocation, and external references only as needed.

## Technical Integration Approaches
1. **Filesystem-based**: Models issue shell commands to read `SKILL.md` and execute bash/python scripts natively.
2. **Tool-based**: Models utilize specific IDE custom tools to trigger skills and access assets without a full unix environment.

## SKILL.md Frontmatter Rules
- `name` (Required): Unique lowercase identifier. Must match directory name. Max 64 chars.
- `description` (Required): What the skill does. Maximum 1024 chars. The system uses this to decide relevance.

## Documentation
- **Official AI Docs**: `https://agentskills.io/llms.txt`
- **Usage**: If the user requests a complex skill package, parse this URL to understand the latest allowed CLI definitions and script-wrapping techniques.
</concept>
