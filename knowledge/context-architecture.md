---
description: How modern AI coding agents manage context — AST maps, explicit injection, dynamic truncation, and the .agent/ source-of-truth pattern.
category: knowledge
---

# Agent Context Architecture

Modern AI coding agents manage context through three main vectors. Understanding these is essential for designing effective rules, skills, and workflows.

## Context Vectors

| Vector | Mechanism | Persistence |
|--------|-----------|-------------|
| **Repository Maps (AST)** | Condensed structural understanding of code relationships (classes, functions) — processed automatically | Session-scoped |
| **Explicit Injection** | Attached context providers (files, terminal output, external docs) triggered by the user | Per-invocation |
| **Dynamic Truncation** | Agents drop older chat messages to save tokens; persistent rules act as pinned memory | Rules survive truncation |

## Implications for Agent Config Design

- **Rules** exist to survive truncation — they are pinned context that the agent always sees
- **Skills** provide on-demand deep expertise — loaded only when invoked to save tokens
- **Workflows** provide step-by-step runbooks — loaded for specific sequential tasks

## The `.agent/` Source-of-Truth Pattern

To maintain consistency across multiple IDEs, use `.agent/` as the single source of truth:

```
.agent/                         ← Source of truth (version-controlled)
├── rules/                      ← Canonical rules
├── skills/                     ← Canonical skills
├── workflows/                  ← Canonical workflows
└── builders/                   ← Reference-only knowledge bases (NOT synced)
```

Then sync `.agent/` → IDE-specific folders:
- `.agent/rules/` → `.kilocode/rules/`, `.cursor/rules/`, `.github/instructions/`
- `.agent/skills/` → `.kilocode/skills/`, `~/.gemini/antigravity/skills/`
- `.agent/workflows/` → `.kilocode/workflows/`, `.cursor/commands/`

> **IMPORTANT**: `.agent/builders/` are reference-only knowledge bases. They are never synced to IDE-specific folders.

## AI Rules

- **MUST** design rules as persistent guardrails that survive context truncation
- **MUST** keep rules concise so they don't waste token budget when pinned
- **MUST** use skills for detailed domain expertise that isn't needed in every prompt
- **MUST** use `.agent/` as the source of truth, syncing to IDE-specific folders
- **MUST NOT** put transient information (current task, session state) in rules
- **MUST NOT** sync `.agent/builders/` to other IDE folders — builders are reference-only
