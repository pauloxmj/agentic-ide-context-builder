---
description: Architectural standard for AI Workflow Orchestration.
---

<concept id="workflows-architecture">
# Workflows Concepts

- **Definition**: Step-by-step instructions (runbooks) guiding AI agents through repeatable, multi-step sequential tasks at the trajectory level. Focuses on *action sequencing* rather than persistent constraints (like Rules).

## Core Execution Models

### Think-Then-Do (Architect vs. Editor)
1. **Planner Phase**: Agent writes a detailed `plan.md` artifact (no code written).
2. **Executor Phase**: Agent translates the plan into file diffs/shell commands.
3. **Reviewer Phase**: Verifier algorithm/agent confirms correctness.

### The Orchestrator / Sub-Agent Pattern
For massive complex tasks, an Orchestrator agent breaks down tasks to summon localized sub-agents (e.g., "Testing Agent") preventing context pollution.

## Advanced Step Capabilities
Depending on the specific IDE platform, a workflow step may trigger:
1. **Parameterized Substitution**: Inject runtime arguments (e.g., `$1`).
2. **Dynamic Context Execution**: Run inline shell scripts (e.g., `git diff` injection).
3. **Native Tooling Hooks**: Triggering MCP tools directly (e.g., `read_file()`).
4. **Sub-workflow Chaining**: Recursively invoking other workflows.
</concept>
