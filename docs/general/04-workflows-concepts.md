# Workflows Concept

<system_context>
This is file `general/04-workflows-concepts.md`.
It explains the core concept of creating AI agent workflows. For exact implementation details and invocation patterns, refer to the files in `ide-specific/`.
</system_context>

## What Are Workflows?

Workflows are **step-by-step instructions** that guide AI agents through repeatable, multi-step tasks. While rules provide persistent background context, workflows provide a **structured sequence of prompts** at the trajectory level, guiding the model through interconnected actions.

Think of them as runbooks that your AI agent can execute autonomously or with human checkpoints.

### Workflows vs. Rules vs. Skills

| | Rules | Workflows | Skills |
|---|---|---|---|
| **Purpose** | Persistent context and constraints | Step-by-step task automation | On-demand domain expertise |
| **When loaded** | Always or conditionally | On invocation (`/name`) | When agent decides or invoked |
| **Granularity** | Guidance | Action sequence | Capability package |
| **Analogy** | Coding standards doc | Runbook / playbook | Expert consultant |

---

## The "Think-Then-Do" (Planner/Executor) Pattern

The most robust architectural pattern for complex AI workflows is the separation of planning and execution, often referred to as "Architect vs. Editor" or "Think-Then-Do".

Instead of asking an agent to "build a feature" in one shot, a mature workflow explicitly forces the agent through isolated cognitive phases:

1. **The Planner (Architect)**: The agent analyzes the codebase, reads requirements, and writes a detailed implementation plan (often stored as an artifact like `plan.md`). It *does not write code*.
2. **The Executor (Editor)**: The agent reads the parsed plan and translates it into exact file diffs and terminal commands.
3. **The Reviewer**: The agent runs the tests or builds algorithms to verify the executor's work.

### 2. The Orchestrator / Sub-Agent Pattern

For massive codebases, modern workflows implement an **Orchestrator Agent**. Instead of managing the entire task directly, the orchestrator breaks the task into sub-components and dynamically summons specialized "Personas" or "Modes" (e.g., a restricted `Documentation Agent` or a `Testing Agent`) to handle specific pieces. 

* **Why this matters**: This prevents context pollution. The testing agent only receives context about the tests, saving tokens and vastly improving accuracy, while the Orchestrator maintains the high-level roadmap.

---

## Workflow Structure

Workflows are typically **Markdown files** containing a title, a description, and numbered sequential steps.

> **Starter Files**: For robust orchestrator-ready workflows utilizing XML boundaries, see the `templates/global/workflows/` and `templates/project/workflows/` directories.

<example title="Basic Conceptual Workflow">
```markdown
# Deploy to Staging

Deploy the current branch to the staging environment.

## Steps

1. Run the full test suite: `npm test`
2. If tests pass, build the production bundle: `npm run build`
3. Push the current branch to the remote
4. Deploy to staging: `./scripts/deploy.sh staging`
5. Verify the deployment by checking the health endpoint
6. Report the deployment status
```
</example>

---

## Technical Capabilities and Parameters

Depending on the IDE, workflows can leverage powerful capabilities inside their steps:

1. **Parameterized Substitution**: Injecting arguments (like `$1` or `$ARGUMENTS`) passed during invocation.
2. **Dynamic Context Shell Execution**: Running commands (like `git diff`) inline during prompt evaluation to inject live context.
3. **Native Tooling Hooks**: Direct calls to internal IDE tools like `read_file()`, `search()`, or installed MCP (Model Context Protocol) servers.
4. **Chaining**: Calling another workflow from within a workflow step.

---

## Best Practices

<best-practices>
### Design
- **Keep steps atomic**: Each step should do one thing.
- **Include verification**: Add steps to check that previous steps succeeded (e.g., check that the tests actually pass before deploying).
- **Add error handling**: Tell the agent what to do when a step fails.
- **Use human checkpoints**: For destructive actions, ask for confirmation.
- **Start with manual workflows**: Automate tasks you've done manually at least 3 times.

### Structure
- **Keep workflows under 500 lines**.
- **Group related workflows**: Use directory structures if supported by the IDE.
- **Document parameters**: If the workflow accepts input, document what's expected.
- **Include context**: Explain *why* each step exists, not just *what* it does.
</best-practices>

<instruction>
You have finished reading the core `general/` concepts. 
When writing configuration for a specific IDE or agent, proceed to the target IDE inside `ide-specific/` (e.g., `ide-specific/04-cursor.md`) to learn the specific directories and features required by that system.
</instruction>
