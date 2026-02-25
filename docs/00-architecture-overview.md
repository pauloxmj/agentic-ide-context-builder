# Architecture Overview

<system_context>
This is the root entrypoint (`00-architecture-overview.md`) for understanding the AI guardrails and architectural standards within this project.

If you are an AI agent analyzing this repository, **you must read the files in this directory in sequential, numerical order** (`00-`, `01-`) and then proceed to the subdirectories.
</system_context>

## Purpose

The `docs/` directory contains the foundational specifications for creating and managing AI agent instructions across various IDEs (Cursor, Claude Code, Kilo Code, GitHub Copilot, Antigravity/Gemini). 

To maximize clarity, the documentation is strictly split into two halves:
1. **General Concepts**: The open standards (AGENTS.md, Agent Skills) and the theory behind rules and workflows. This applies universally.
2. **IDE-Specifics**: How each IDE actually implements these concepts (file paths, tool integrations, quirks).

## Reading Order

<instruction>
AI Agents: Process these files in the following exact sequence to build your context correctly.
</instruction>

### Root Documentation
1. **`00-architecture-overview.md`**: This file.
2. **`01-resources-index.md`**: An index of external open standards and IDE documentation (`llms.txt`) links for the latest syntaxes.

### General Concepts
*Located in `general/`*
3. **`general/01-agents-md.md`**: Explains the `AGENTS.md` open format (the universal project entrypoint).
4. **`general/02-agent-skills.md`**: Explains the Agent Skills open standard for providing deeply scoped, on-demand capabilities.
5. **`general/03-rules-concepts.md`**: Explains the theory behind providing persistent context (Code standards).
6. **`general/04-workflows-concepts.md`**: Explains the theory behind structured, multi-step agent runbooks.
7. **`general/05-mcp-concepts.md`**: Explains the Model Context Protocol for integrating tools and data.

### IDE-Specific Implementations
*Located in `ide-specific/`. Only read the file(s) relevant to the IDE you are currently operating in, or all of them if you are writing cross-platform rules.*
8. **`ide-specific/01-kilocode.md`**
9. **`ide-specific/02-antigravity.md`**
10. **`ide-specific/03-github-copilot.md`**
11. **`ide-specific/04-cursor.md`**
12. **`ide-specific/05-claude-code.md`**

<instruction>
Proceed to `01-resources-index.md` to access the live external references, and then transition into the `general/` folder.
</instruction>
