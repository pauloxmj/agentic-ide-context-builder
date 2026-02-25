---
description: Semantic parser tags and formatting rules for the RAC Database.
---

# RAC Schema & Parser Guidelines

This database operates on the principles of **Retrieval-Augmented Context (RAC)**. The knowledge base is heavily optimized for zero-hallucination processing by an AI agent.

When searching this knowledge base, the AI must locate and extract information strictly bounded by the following XML tags:

## Core Schema Tags

### `<concept id="[unique-id]">`
- **Definition**: Fundamental concepts, architectural principles, or general knowledge.
- **Usage**: Used to establish the theoretical rules of engagement, independent of any specific IDE.
- **Example**: `<concept id="mcp-server">`

### `<ide_target name="[ide-name]">`
- **Definition**: The root container for quirks and configurations specific to a singular IDE (e.g., Cursor, GitHub Copilot).
- **Usage**: Encapsulates all knowledge necessary to configure agentic systems for a targeted IDE environment.

### `<ide_quirk type="[rule/skill/workflow/prompt]">`
- **Definition**: A specific mechanism, bug, or configuration requirement for an IDE. Must reside inside an `<ide_target>`.
- **Usage**: Describes *how* an IDE deviates from the standard or requires specific directory paths and file extensions.

### `<template scope="[global/project]" target="[file-type]">`
- **Definition**: A strictly formatted markdown/yaml template designed for copy-pasting.
- **Usage**: The exact structural foundation an AI should use when creating a new rule, skill, or workflow.

## Structural Constraints
1. **No Conversational Fluff**: Knowledge is presented in dense, hierarchical bullet points.
2. **YAML Frontmatter**: All nodes (`.md` files) use YAML frontmatter to index descriptions and metadata.
3. **Strict Bounds**: If information is not within one of the tags defined above, it is considered supplementary context and *not* authoritative RAC data.
