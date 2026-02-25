---
description: Universal agent entrypoint and base architectural patterns.
---

<concept id="agents-md-entrypoint">
# AGENTS.md Standard

- **Definition**: The universal root-level entrypoint ("README for agents") used to provide initial context for AI coding agents.
- **Location**: Project root (`/AGENTS.md`).
- **Purpose**: Defines highest-level guardrails, build workflows, testing commands, and PR instructions before routing to IDE-specific configurations.
- **Constraints**: 
  - Do not place generic boilerplate (e.g., "write clean code") here. 
  - Focus exclusively on project-unique configurations.
</concept>

<concept id="context-architecture">
# Agent Context Architecture

Modern AI coding agents manage context through three main vectors:
1. **Repository Maps (AST)**: Condensed structural understanding of relationships (classes, functions) processed automatically.
2. **Explicit Injection**: Attached Context providers (files, terminal output, external docs) explicitly triggered by the user to override AST auto-discovery.
3. **Dynamic Truncation**: Agents drop older chat messages to save tokens. Persistent rules act as pinned memory.
</concept>
