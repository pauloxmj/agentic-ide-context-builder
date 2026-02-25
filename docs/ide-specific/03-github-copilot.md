# GitHub Copilot Implementation

<system_context>
This is file `ide-specific/03-github-copilot.md`.
It details how GitHub Copilot implements AI agent concepts like custom instructions and agent skills.
</system_context>

## Custom Instructions (Rules)

GitHub Copilot separates its instructions into three distinct tiers:

1. **Personal instructions**: Stored globally in the Copilot settings (usually via `.github/copilot-instructions.md` globally or IDE configs).
2. **Repository instructions**: Stored at the root of a specific repository.
3. **Organization instructions**: Set at the GitHub Organization level (for Copilot Enterprise).

### Repository File Location

To provide contextual, repository-wide rules, you define them in:

```
.github/copilot-instructions.md
```

If multiple files exist in `.github/`, they are parsed sequentially.

### Precedence

If rules contradict each other, Copilot resolves them in this order (highest priority first):
1. **Organization** instructions
2. **Repository** instructions
3. **Personal** instructions
4. Current chat prompt context

### Implicit vs. Explicit Context

Copilot manages context by distinguishing between:
1. **Implicit Context**: Automatically gathered background data (your currently open tabs, highlighted code snippets, and workspace structure).
2. **Explicit Context**: Actively pinned scopes. The user can explicitly guide the agent using commands like `@workspace` (forcing the agent to scan the entire solution) or `#file:utils.ts` (forcing focus on a specific file).

## Copilot Edits vs Copilot Chat

Currently, Copilot Chat (the sidebar) has different capabilities depending on whether the user is in VS Code, Visual Studio, or Jetbrains. However, the repository instructions (`copilot-instructions.md`) attach to all of them.

## Agent Skills

GitHub Copilot actively supports configuring and discovering **Agent Skills**. 
Similar to other implementations, a repository can store capabilities inside a folder and Copilot will parse the root `SKILL.md` to understand if it should invoke those specific instructions or terminal sequences when solving a task.

### Model Context Protocol (MCP)

GitHub Copilot environments also support MCP integrations, giving the workspace the ability to read from external, authenticated databases and issue trackers directly via the standardized server protocol.
