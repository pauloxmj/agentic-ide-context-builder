# Agentic Context RAC Database

> A **Retrieval-Augmented Context (RAC)** database and template kit for governing AI coding agents with **rules**, **workflows**, and **skills**.

## What This Is

This project is a highly dense **context database designed strictly for AI agents**. It uses explicit XML tagging (`<concept>`, `<ide_quirk>`) to provide deterministic boundaries for AI parsers, eliminating conversational fluff and reducing hallucination.

The core workflow involves giving an AI agent three things:
1. The context from this repository (the RAC database).
2. The codebase of a target project you want to set up or modify.
3. Specific instructions provided in your manual prompt (e.g., "Set up this repository for Cursor").

Using this combination, the AI can effortlessly retrieve the exact architectural constraints from the RAC database and compose them into perfectly tailored agentic structures.

## The RAC Core Schema

Read `RAC-SCHEMA.md` to understand the XML boundaries. The repository is structured to separate concerns entirely:

| Directory | Tag Strategy | Purpose |
|-----------|--------------|---------|
| `concepts/` | `<concept>` | Universal, IDE-agnostic rules of engagement (SOLID, MCP, Agent Skills). |
| `ide-targets/` | `<ide_target>`, `<ide_quirk>` | Concrete structural paths and format overrides for specific IDEs. |
| `templates/` | `<template>` | Raw, copy-pasteable markdown/yaml structures for scaffolding. |

## Repository Structure

```
├── README.md                 ← You are here
├── AGENTS.md                 ← Project-level context injector
├── RAC-SCHEMA.md             ← The strict XML parsing ruleset
├── AGENT-INSTRUCTIONS.md     ← Paste into your AI Assistant prompt
│
├── concepts/             ← High-level architectural knowledge
├── ide-targets/              ← IDE-specific configuration quirks
├── templates/                ← Scaffolding structures
├── skills/                   ← Core architectural skills for agents
└── globals/                  ← Backup of personal global configurations
```

## Core Architectural Skills

This KB is designed to be used in tandem with the following core skills found in the `skills/` directory:

1. **`agentic-ide-architecture-global-updater`**: Handles user-level global configurations (e.g., `~/.gemini/antigravity`). Use this for changes that should persist across all your projects.
2. **`agentic-ide-architecture-project-updater`**: Handles project-specific configurations (e.g., `.agent/`). Use this for rules and workflows tailored to a specific codebase.

### How to Use Skills with this KB
When an AI agent is tasked with updating context, it should:
1. **Identify Scope**: Determine if the change is global or project-specific.
2. **Consult KB**: Use `concepts/` and `templates/` as the source of truth for the change.
3. **Execute Skill**: Use the corresponding Skill to apply the change following the standard architecture.

## How AI Agents Use This

If you are an AI:
1. Parse `RAC-SCHEMA.md` immediately.
2. Treat `concepts/` as your theoretical foundation.
3. Target `ide-targets/` based on the user's specific IDE request.
4. Extract `templates/` to output the final result.

If you are a Human:
1. Provide `AGENT-INSTRUCTIONS.md` to your custom assistant (Claude Project, Custom GPT, etc.).
2. Upload this entire repo as its knowledge base.
3. Ask it to build you workflows, rules, or skills!
