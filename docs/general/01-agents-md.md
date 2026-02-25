# AGENTS.md Standard

<system_context>
This is file `general/01-agents-md.md`.
It explains the `AGENTS.md` open format, the universal standard for providing a single, predictable context entrypoint for code agents.
</system_context>

## What is AGENTS.md?

**AGENTS.md** is an open format designed to be a "README for agents." It provides a dedicated, predictable place in a repository to supply context and instructions intended specifically to help AI coding agents navigate and work within a project.

By placing an `AGENTS.md` file in the root of a project, the developer establishes the highest-level guardrails and tips that any AI agent should immediately process.

## Why Use AGENTS.md?

<rationale>
Before `AGENTS.md`, general project instructions were often scattered across IDE-specific files. `AGENTS.md` serves as the **universal entrypoint**, ensuring that regardless of whether the user is in Cursor, Claude Code, Kilo Code, Copilot, or Antigravity, the agent finds the core operational truths of the repository. Many IDE-specific rule configurations can simply point back to this root document.
</rationale>

## Example AGENTS.md Structure

<example title="Minimal AGENTS.md">

```markdown

# Sample AGENTS.md file

## Dev environment tips
- Use `pnpm dlx turbo run where <project_name>` to jump to a package instead of scanning with `ls`.
- Run `pnpm install --filter <project_name>` to add the package to your workspace so Vite, ESLint, and TypeScript can see it.

## Testing instructions
- Find the CI plan in the .github/workflows folder.
- Run `pnpm turbo run test --filter <project_name>` to run every check defined for that package.
- To focus on one step, add the Vitest pattern: `pnpm vitest run -t "<test name>"`.
- Fix any test or type errors until the whole suite is green.

## PR instructions
- Title format: [<project_name>] <Title>
- Always run `pnpm lint` and `pnpm test` before committing.

```
</example>

## Best Practices

<rules_for_agents_md>
1. **Keep it Root-Level**: The primary `AGENTS.md` should live at the root of the repository.
2. **Focus on Workflows & Tips**: Use it for environment quirks, build instructions, testing commands, and PR formatting.
3. **Avoid Boilerplate**: Do not copy standard generic rules (like "Write clean code"). Focus entirely on things unique to this codebase.
4. **Use Sub-directories if needed**: Large monorepos can place `AGENTS.md` files in subdirectories to provide localized context for specific packages.
</rules_for_agents_md>

<instruction>
Proceed to `general/02-agent-skills.md`.
</instruction>
