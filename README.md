# Agentic Architecture

> A knowledge base and template kit for governing AI coding agents with **rules**, **workflows**, and **skills** — at both global and project levels.

## What This Is

This project is a **context database designed to be fed into AI agents**. The core workflow involves giving an AI agent three things:
1. The context from this repository (the architectural rules and templates).
2. The codebase of a target project you want to set up or modify.
3. Specific instructions provided in your manual prompt (e.g., "Set up this repository for Kilo Code, Cursor, Claude Code, Antigravity, or GitHub Copilot").

Using this combination, the AI can effortlessly create, edit, and update IDE agentic structures perfectly tailored to set up your destination project. If your prompt states which IDE is being used, the AI will automatically read the corresponding documentation in `docs/ide-specific/` and apply its unique particularities.

1. **Agent Instructions** — A ready-to-use instruction set for an AI Assistant (e.g., Gemini Gem, ChatGPT Custom GPT, Claude Project) that acts as an Agentic AI Architecture Expert
2. **Reference Documentation** — Condensed, AI-parsable guides synthesized from Kilo Code, Antigravity (Gemini), GitHub Copilot, Cursor, Claude Code, and the Agent Skills specification
3. **Starter Templates (`templates/`)** — Production-ready templates heavily optimized with AI-parsable XML tags (`<system_context>`, `<instruction>`) and advanced Orchestrator prompts for both global and project levels

## The Four Pillars

| Pillar | Purpose | Analogy |
|--------|---------|---------|
| **AGENTS.md** | Universal project entrypoint | The Entryway / Front Desk |
| **Rules** | Persistent constraints and context | Coding standards document |
| **Workflows** | Step-by-step task automation | Runbook / playbook |
| **Skills** | On-demand domain expertise packages | Expert consultant |

## Two Scopes

| Scope | Where | Who Benefits |
|-------|-------|--------------|
| **Global** | User home directory (`~/`) | You, across all projects |
| **Project** | Project root (`.cursor/`, `.claude/`, etc.) | Your team, version-controlled |

## Repository Structure

```
agentic-architecture/
├── README.md                           ← You are here
├── agent-instructions.md               ← Paste into your AI Assistant
│
├── docs/
│   ├── 00-architecture-overview.md     ← Start here
│   ├── 01-resources-index.md           ← Curated IDE doc links
│   ├── general/                        ← Universal concepts (Rules, Workflows, MCP)
│   └── ide-specific/                   ← Concrete instructions for the 5 supported IDEs
│
├── templates/
│   ├── AGENTS.md                       ← Copy to project root
│   ├── global/                        ← Copy to ~/.kilocode/, ~/.cursor/, ~/.claude/, or ~/.gemini/
│   │   ├── rules/
│   │   │   ├── coding-standards.md        ← (Rename to .mdc for Cursor)
│   │   │   ├── documentation-style.md
│   │   │   └── security-guidelines.md
│   │   ├── workflows/
│   │   │   ├── pr-submission.md
│   │   │   └── code-review-prep.md
│   │   └── skills/
│   │       ├── api-design/SKILL.md
│   │       └── code-review/SKILL.md
│   │
│   └── project/                       ← Copy to project .kilocode/, .cursor/, .claude/, .agent/, or .github/
│       ├── rules/                         ← (Or single .github/copilot-instructions.md)
│       │   ├── project-conventions.md     ← (Rename to .mdc for Cursor)
│       │   ├── architecture-guidelines.md
│       │   └── restricted-files.md
│       ├── workflows/
│       │   ├── setup-environment.md
│       │   ├── mcp-server-setup.md
│       │   └── release-management.md
│       └── skills/
│           ├── project-onboarding/SKILL.md
│           └── feature-implementation/SKILL.md
```

## How to Use

### 1. Set Up Your AI Assistant

You can use `agent-instructions.md` to create a custom AI assistant (like a Gemini Gem, ChatGPT Custom GPT, or Claude Project).

1. Create a new custom assistant in your preferred AI platform
2. Paste the contents of [`agent-instructions.md`](agent-instructions.md) into the system prompt or instructions field
3. Upload all files from `docs/` as context files or knowledge base for the assistant
4. Save and start using it

### 2. Install Global Templates

Copy templates to your IDE's global config directory:

```bash
# For Kilo Code
cp -r templates/global/rules/ ~/.kilocode/rules/
cp -r templates/global/workflows/ ~/.kilocode/workflows/
cp -r templates/global/skills/ ~/.kilocode/skills/

# For Cursor
# Copy templates and rename rules from .md to .mdc
mkdir -p ~/.cursor/rules ~/.cursor/skills
for f in templates/global/rules/*; do cp "$f" ~/.cursor/rules/$(basename "$f" .md).mdc; done
cp -r templates/global/skills/ ~/.cursor/skills/

# For Claude Code
cp -r templates/global/rules/ ~/.claude/rules/
cp -r templates/global/skills/ ~/.claude/skills/

# For Antigravity (Gemini)
# Global rules go in ~/.gemini/antigravity/rules/
# Skills go in ~/.gemini/antigravity/skills/
```

### 3. Set Up Project Templates

Copy templates into your project and customize:

```bash
# Universal Entrypoint (All IDEs)
cp templates/AGENTS.md .
# For Kilo Code
cp -r templates/project/rules/ .kilocode/rules/
cp -r templates/project/workflows/ .kilocode/workflows/
cp -r templates/project/skills/ .kilocode/skills/

# For Cursor
# Copy templates and rename rules from .md to .mdc
mkdir -p .cursor/rules .cursor/skills
for f in templates/project/rules/*; do cp "$f" .cursor/rules/$(basename "$f" .md).mdc; done
cp -r templates/project/skills/ .cursor/skills/

# For Claude Code
cp -r templates/project/rules/ .claude/rules/
cp -r templates/project/skills/ .claude/skills/
# Note: Claude also supports a root CLAUDE.md file for base context

# For Antigravity (Gemini)
cp -r templates/project/rules/ .agent/rules/
cp -r templates/project/skills/ .agent/skills/

# For GitHub Copilot
# Project rules go in .github/copilot-instructions.md
```

### 4. Ask the Assistant for Help

Use your AI Assistant to generate more rules, workflows, and skills:

- *"Create a global rule for TypeScript strict typing"*
- *"Design a deployment workflow for a Next.js app on Vercel"*
- *"Build a skill for database migration management"*
- *"Set up our project rules for Cursor — we use React, TypeScript, and Tailwind"*

## Supported IDEs

| IDE | Rules | Workflows | Skills |
|-----|-------|-----------|--------|
| Kilo Code | ✅ | ✅ | ✅ |
| Cursor | ✅ | ✅ (Commands) | ✅ |
| Claude Code | ✅ | ✅ (Skills) | ✅ |
| Antigravity (Gemini) | ✅ | ✅ | ✅ |
| GitHub Copilot | ✅ (limited) | — | — |

## License

This is a knowledge base — use it however you like. The templates are starting points meant to be customized.
