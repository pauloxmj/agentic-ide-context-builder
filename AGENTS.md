# AGENTS.md

<system_context>
Welcome to the Agentic Architecture Builder repository! 
This project is a database and context provider designed to be fed to AI agents. By providing this repository as context alongside a target project's codebase, AI systems can use this knowledge—combined with the user's specific prompt instructions—to easily create, edit, and update IDE agentic structures to set up any target project.
</system_context>

## Repository Structure

Our documentation is strictly divided to ensure maximum clarity and reusability for AI agents:

1. **`docs/general/`**: Universal, IDE-agnostic architectures. This includes the Model Context Protocol (MCP), the Agent Skills standard, and abstract workflow routing strategies (e.g., the Orchestrator/Sub-Agent pattern).
2. **`docs/ide-specific/`**: Concrete implementation details for the 5 major supported IDEs/platforms:
   - Kilo Code
   - Google Antigravity (Gemini)
   - GitHub Copilot
   - Cursor
   - Claude Code
3. **`templates/`**: Production-ready starter templates for rules, workflows, and skills. These templates are heavily optimized with XML tags and advanced orchestrator patterns.

## Getting Started

If you are an AI assistant entering this repository to assist a developer, **start by reading:**
`docs/00-architecture-overview.md`

This file provides the necessary reading sequence to understand the entire documentation suite without suffering from context pollution.

## Documentation Standards

When modifying or adding documentation to this repository, you must adhere to the following rules:

1. **XML Tagging for Context**: Use explicit XML-like tags (e.g., `<system_context>`, `<instruction>`, `<example>`) to provide structural hints to other LLMs that will read these files in the future.
2. **Abstract First**: Never put IDE-specific quirks (like Cursor's `.mdc` file format) into the `general/` section. Keep `general/` completely agnostic.
3. **No Redundancy**: If a concept applies to multiple IDEs (like explicit `@` context injection), explain the theory in `general/03-rules-concepts.md` and only explain the *syntactical difference* in the specific IDE file.
4. **Machine-Parseable Tables**: Heavily utilize Markdown tables when comparing scopes, directories, and paths for quick scanning by indexing engines.

## Key Resources

If you need to verify links or external references to open standards (like the MCP Github or the Agent Skills spec), immediately check `docs/01-resources-index.md`.
