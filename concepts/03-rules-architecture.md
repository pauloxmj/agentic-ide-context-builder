---
description: Semantic rules architecture and scope distinction.
---

<concept id="rules-architecture">
# Rules Concepts

- **Definition**: Persistent, text-based instructions acting as pinned guardrails and conventions guiding AI agent behavior at the prompt level.
- **Goal**: Minimize context truncation. AI agents automatically condense file histories over time. Rules prevent essential context from dropping out of memory. 

## Scope Types
1. **Global/User Scope**: Spans across all projects (e.g., security habits, personal code style). Must not contain stack-specific instructions.
2. **Project/Workspace Scope**: Strictly tied to the directory codebase (e.g., project conventions, architecture patterns).
3. **Team/Organization Scope**: Policy enforcement across a company.
4. **Mode-Specific Scope**: Rules triggered only when the agent changes modes (e.g., Architect vs. Editor).

## Formatting Constraints
- **Under 500 lines**: Keep rules concise. Move detailed references out of the core rule file.
- **Reference existing examples**: Do not inline full code snippets; point to canonical repository files.
- **Linter Deferral**: Never duplicate a rule that a linter/formatter can enforce autonomously. Focus on cognitive processes a human or AI must judge.
</concept>
