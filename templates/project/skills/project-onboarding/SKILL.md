---
name: project-onboarding
description: Walk through the codebase architecture and key modules for new team members. Use when onboarding someone, when asked about the project structure, or when explaining how the codebase works.
---

# Project Onboarding

Help new team members understand the codebase structure, key patterns, and development workflows.

## When to Use

- A new developer joins the team
- Someone asks "how does this project work?"
- A contributor needs to understand a specific module

## Onboarding Steps

### 1. High-Level Overview

Start by explaining:
- What the project does (purpose and users)
- The tech stack (language, framework, database, etc.)
- The deployment model (where and how it runs)

### 2. Architecture Walkthrough

Explain the project structure:
- Show the directory layout and what each top-level directory contains
- Explain the architectural pattern (MVC, Clean Architecture, etc.)
- Identify the entry points (main files, route definitions)
- Trace a typical request from user action to database and back

### 3. Key Modules

For each major module, explain:
- **What it does**: One-sentence purpose
- **How it's structured**: Key files and their roles
- **How it interacts**: Dependencies and data flow
- **Common patterns**: Patterns used within the module

### 4. Development Workflow

Cover:
- How to run the project locally
- How to run tests
- How to create a PR
- Where to find documentation

### 5. Common Gotchas

List known pain points, quirks, and things that trip up new developers. Include workarounds.

## Style Guidelines

- Start with the big picture, then drill into details
- Use analogies to explain complex concepts
- Include ASCII diagrams for architecture and data flow
- Keep explanations conversational and welcoming
