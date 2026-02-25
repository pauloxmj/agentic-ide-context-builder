# Custom Rules Concepts

<system_context>
This is file `general/03-rules-concepts.md`.
It explains the concept of providing persistent context to AI coding agents. For exact directory paths and IDE-specific behaviors, refer to the files in `ide-specific/`.
</system_context>

## What Are Rules?

Rules are persistent, text-based instructions that guide AI agent behavior. They provide reusable context at the prompt level — since LLMs don't retain memory between completions naturally, rules give the AI consistent guidance for generating code, interpreting edits, and following conventions.

Rules act as **guardrails and conventions** that are consistently respected across interactions with the codebase.

## Relationship with AGENTS.md

As noted in `01-agents-md.md`, `AGENTS.md` is the universal, root-level entrypoint for giving an agent context. IDE-specific rules should be used to enforce *granular* instructions (like "React Component style") while `AGENTS.md` holds global repository context. When writing rules, you should never duplicate what's already in `AGENTS.md` or the local linters.

---

## Universal Context Management Architectures

To write effective rules, it is vital to understand how modern AI coding agents manage their context windows (the amount of text they can "remember" at once).

### 1. Repository Maps and AST Parsing
Advanced agents do not read every file in your project. Instead, they parse your codebase into Abstract Syntax Trees (ASTs) or "Repository Maps." This gives them a condensed, structural understanding of relationships (classes, functions, interfaces) without needing the full text. 
* **Implication for Rules**: Rules should assume the agent understands the *architecture* but may need explicit commands to look at specific *implementation details*.

### 2. Explicit Context Injection (Context Providers)
Modern IDEs often allow users to explicitly attach context (like specific files, terminal output, external docs, or git diffs) to a prompt, overriding the agent's auto-discovery.
* **Implication for Rules**: You can write rules that instruct the agent to *expect* explicit context. (e.g., "Always review the attached `@Terminal` output before suggesting a fix.")

### 3. Dynamic Context Truncation
To save tokens, agents routinely drop older chat messages or auto-condense file histories.
* **Implication for Rules**: Rules act as "pinned" context that never drops out of memory. This is why you must keep them concise; overly long rules will permanently eat into the context window and slow the agent down.

---

## Rule Types by Scope

| Scope | Description | Use Case |
|-------|-------------|----------|
| **Global / User** | Apply across all projects and workspaces | Personal coding style, security habits, communication preferences |
| **Project / Workspace** | Apply only to a specific project | Project conventions, architecture patterns, restricted files |
| **Team / Organization** | Enforced across entire teams (some IDEs) | Company coding standards, compliance requirements |
| **Mode-Specific** | Apply only in certain agent modes | Different rules for code vs. architect vs. debug modes |

---

## Rule File Format

Rules are **Markdown files** (`.md` or `.mdc`). Some IDEs support optional YAML frontmatter for metadata, allowing the agent to dynamically load the rule only when specific glob patterns or NLP conditions match. 

> **Starter Files**: For production-ready examples heavily optimized with AI-parseable XML tags (`<system_context>`, `<instruction>`), see the `templates/global/rules/` and `templates/project/rules/` directories.

<example title="Basic Conceptual Rule">
```markdown
# Code Style

- Use 2-space indentation
- Use camelCase for variable names
- Use PascalCase for class names
- Prefer `const` over `let`; never use `var`
```
</example>

---

## Best Practices for Architecting Rules

<best-practices>
### Do
- **Be specific**: "Use 2-space indentation" > "Format code properly"
- **Use Markdown structure**: Headers for categories, lists for items, code blocks for examples
- **Separate concerns**: One file per topic (`code-style.md`, `security.md`, `testing.md`)
- **Use descriptive filenames**: The filename should indicate what the rules cover
- **Include examples**: Show the expected behavior, not just describe it
- **Reference files, don't copy**: Point to canonical examples instead of inlining full code
- **Keep rules under 500 lines**: Move detailed reference material to separate files
- **Version control project rules**: Check rules into git for team consistency

### Don't
- **Don't copy entire style guides** — use a linter instead. The agent already knows common conventions.
- **Don't document every command** — the agent knows `npm`, `git`, `pytest`, etc.
- **Don't add edge-case instructions** — keep rules focused on frequent patterns.
- **Don't over-optimize early** — start simple, add rules when you notice repeated mistakes.

### Core Principles Checklist
When writing or reviewing any rule, verify it meets these criteria:
1. **Be Specific**: Clearly define the scope and intent of each rule.
2. **Use Categories**: Organize related rules under common headers.
3. **Separate Concerns**: Use different files for different types of rules.
4. **Use Examples**: Include examples to illustrate expected behavior.
5. **Keep It Simple**: Concise and easy to understand.
</best-practices>

<instruction>
Proceed to `general/04-workflows-concepts.md` to learn about sequencing LLM steps.
</instruction>
