---
description: Architectural standard for AI workflow orchestration — step-by-step runbooks, execution models, turbo annotations, and best practices for writing effective workflows.
category: knowledge
---

# Workflows Architecture

Step-by-step instructions (runbooks) guiding AI agents through repeatable, multi-step sequential tasks at the trajectory level. Workflows focus on *action sequencing* rather than persistent constraints (that's what Rules are for).

## Core Execution Models

### Think-Then-Do (Architect vs. Editor)
1. **Planner Phase**: Agent writes a detailed plan artifact (no code written)
2. **Executor Phase**: Agent translates the plan into file diffs/shell commands
3. **Reviewer Phase**: Verifier algorithm/agent confirms correctness

### Orchestrator / Sub-Agent Pattern
For massive complex tasks, an Orchestrator agent breaks down tasks and spawns localized sub-agents (e.g., "Testing Agent") to prevent context pollution.

## Workflow File Format

```markdown
---
description: Short description of what this workflow does
---
[Specific steps on how to run this workflow]
```

## Step Annotation Patterns

Workflows support annotations that control execution behavior:

| Annotation | Scope | Effect |
|-----------|-------|--------|
| `// turbo` | Single step | Auto-runs the next step's command without user approval |
| `// turbo-all` | Entire workflow | Auto-runs ALL command steps in the workflow |

### Example

```markdown
1. Install dependencies
// turbo
2. Run `npm install`
3. Start dev server
// turbo
4. Run `npm run dev`
```

In this example, steps 2 and 4 auto-run because of the `// turbo` annotations above them.

## Advanced Step Capabilities

| Capability | Description |
|------------|-------------|
| **Parameterized Substitution** | Inject runtime arguments (e.g., `$1`) |
| **Dynamic Context Execution** | Run inline shell scripts (e.g., `git diff` injection) |
| **Native Tooling Hooks** | Trigger MCP tools directly (e.g., `read_file()`) |
| **Sub-workflow Chaining** | Recursively invoke other workflows |

## How to Write Effective Workflows

### Content Structure

A well-structured workflow file contains:
1. **YAML frontmatter** — `description` (required for IDE discoverability)
2. **Numbered steps** — Each step = one action, clear and copy-pasteable
3. **Turbo annotations** — Where safe, add `// turbo` for auto-execution
4. **Verification step** — Final step to confirm success

### When to Create a Workflow vs. a Rule vs. a Skill

| Create a Workflow | Create a Rule | Create a Skill |
|-------------------|---------------|----------------|
| Sequential procedure with specific order | Persistent constraint, no specific order | Reusable domain expertise |
| Triggered by slash command or explicit request | Always active, pinned to context | Invoked on-demand for complex tasks |
| Has specific terminal commands to run | Guides judgment, no commands | May include scripts and references |
| Repeatable across sessions | Permanent across sessions | Reusable across sessions |

### Cross-IDE Workflow Location

| IDE | Project Workflows | Global Workflows |
|-----|-------------------|-----------------|
| **Kilo Code** | `.kilocode/workflows/` | `~/.kilocode/workflows/` |
| **Antigravity** | `.agent/workflows/` | `~/.gemini/antigravity/workflows/` |
| **Cursor** | `.cursor/commands/` | — |
| **Copilot** | `.github/prompts/` | — |

## AI Rules

- **MUST** write workflows as numbered, sequential step lists
- **MUST** include a `description` in YAML frontmatter for IDE discoverability
- **MUST** separate planning and execution into distinct phases
- **MUST** use `// turbo` annotations for safe-to-auto-run steps
- **MUST NOT** use workflows for persistent constraints — use rules instead
- **MUST NOT** put multiple actions in a single step — one step = one action
- **IF** a task is complex → use the orchestrator pattern to spawn sub-agents
- **IF** a step is safe to auto-run → add `// turbo` annotation above it
