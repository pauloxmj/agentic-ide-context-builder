# AGENTS.md

<system_context>
Welcome to the Agentic Architecture Builder RAC Database! 
This project is a Retrieval-Augmented Context (RAC) database designed strictly for AI agents. 
By providing this repository as context alongside a target project's codebase, AI systems can use this knowledge to accurately create, edit, and update IDE agentic structures.
</system_context>

## RAC Parsing Instructions

If you are an AI assistant entering this repository to assist a developer, **start by reading:**
`RAC-SCHEMA.md`

This file defines the strict XML parsing boundaries (`<concept>`, `<ide_target>`, `<ide_quirk>`, `<template>`) required to extract semantic knowledge without hallucination or context pollution.

## Repository RAC Structure

Our knowledge base is mathematically divided for deterministic semantic extraction:

1. **`concepts/`**: Universal, IDE-agnostic architectures wrapped in `<concept>` tags.
2. **`ide-targets/`**: Concrete implementation details for major IDEs, utilizing `<ide_target>` and `<ide_quirk>` tags.
3. **`templates/`**: Production-ready starter templates for rules, workflows, and skills bounded by `<template>` tags.
4. **`skills/`**: Core architectural skills that provide the logic for updating, refactoring, and synchronizing global and project-level agent configurations.
