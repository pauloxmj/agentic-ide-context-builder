---
description: Architectural standard for persistent text-based rules that guide AI agent behavior — scope types, activation modes, formatting constraints, and best practices for writing effective rules.
category: knowledge
---

# Rules Architecture

Persistent, text-based instructions acting as pinned guardrails and conventions guiding AI agent behavior at the prompt level. They minimize context truncation — essential context stays in memory even as chat history is dropped.

## Scope Types

| Scope | Description | Example |
|-------|-------------|---------|
| **Global/User** | Spans all projects — personal code style, security habits | "Always use explicit return types" |
| **Project/Workspace** | Tied to a specific codebase — architecture patterns, conventions | "Use Bulletproof React feature-sliced design" |
| **Team/Organization** | Policy enforcement across a company | "All PRs require 2 approvals" |
| **Mode-Specific** | Triggered only in specific agent modes (Architect, Editor, etc.) | "In Architect mode, never write code directly" |
| **Path-Specific** | Applied only when working on files matching a glob pattern | "For `*.test.ts`, use Vitest with describe/it blocks" |

## Rule Activation Types

Different IDEs support different activation modes. An agent writing rules must know which type to use:

| Activation | When Applied | IDE Support |
|------------|-------------|-------------|
| **Always** | Included in every AI request automatically | Cursor, Kilo Code, Antigravity |
| **Auto-Attach (Glob)** | Applied when working on files matching a glob pattern | Cursor (`.mdc` globs), Antigravity (frontmatter `globs`), Copilot (`.instructions.md`) |
| **Agent-Requested** | AI decides whether to apply based on the rule's description | Cursor |
| **Manual** | Only applied when explicitly referenced by user | Cursor, Windsurf |
| **Mode-Specific** | Triggered only in a specific agent mode | Kilo Code (`rules-[mode-name]/`) |

## Formatting Constraints

- **Under 500 lines**: Keep rules concise; move detailed references to separate files
- **Reference existing examples**: Point to canonical repository files instead of inlining full code snippets
- **Linter deferral**: Never duplicate a rule that a linter/formatter can enforce autonomously — focus on cognitive judgment

## How to Write Effective Rules

### Content Structure

A well-structured rule file contains:
1. **YAML frontmatter** — `description` (required), optionally `globs` for file-scoped activation
2. **Lead summary** — 1-2 sentences stating what this rule enforces
3. **Rules body** — Dense bullet points or tables, never narrative paragraphs
4. **Examples** — Show correct patterns, not just prohibitions

### What Belongs in a Rule vs. Elsewhere

| Put in a Rule | Put in a Skill | Put in a Workflow |
|---------------|----------------|-------------------|
| Persistent constraints (naming, patterns) | Domain expertise (how to build X) | Sequential procedures (deploy, release) |
| Style decisions requiring judgment | Complex multi-step tasks | Step-by-step runbooks |
| Architecture guardrails | Reference material loaded on-demand | Commands with `// turbo` annotations |
| Security policies | Scripts and automation | One-time or periodic procedures |

### Anti-Patterns to Avoid

| Anti-Pattern | Why It Fails |
|-------------|-------------|
| Duplicating linter rules | Wastes tokens — linters enforce these automatically |
| Generic boilerplate ("write clean code") | Provides no actionable context |
| Stack-specific rules in global scope | Contaminates unrelated projects |
| Long narrative paragraphs | AI parses bullets/tables 3-5x more accurately |
| Rules > 500 lines | Exceeds token budget when pinned to every request |

## AI Rules

- **MUST** keep rules under 500 lines per file
- **MUST** separate global and project scope into distinct files
- **MUST** use YAML frontmatter with `description` (and optionally `globs` for file-scoped rules)
- **MUST** use dense bullet points or tables — never narrative paragraphs for constraint lists
- **MUST NOT** duplicate linter/formatter rules — focus on decisions requiring human/AI judgment
- **MUST NOT** place stack-specific instructions (e.g., React patterns) in global scope
- **IF** a rule applies to specific file types → use `globs` in frontmatter to scope it
- **IF** unsure whether to create a rule or skill → rules are for constraints, skills are for expertise
