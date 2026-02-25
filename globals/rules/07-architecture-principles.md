---
description: Universal architecture principles for global rules, skills, and workflows. Enforces the distinction between global (general/process) and project (stack/context) scopes.
globs: "*"
---
# Architecture Principles: Global vs. Project Scope

<instruction>
Maintain a clean separation between global configurations and project-specific implementations to ensure portability and scalability.
</instruction>

## Core Principles

### 1. Global is for Generalization
- **Focus**: Processes, patterns, ethics, and high-level practices.
- **Goal**: Apply to *any* codebase regardless of the language, framework, or industry.
- **Content**: Plan-Act-Reflect cycles, Clean Code (SOLID/KISS/YAGNI), Communication styles.

### 2. Project is for Specialization
- **Focus**: Stack-specific rules, library conventions, and business logic.
- **Goal**: Optimize the agent for the *current* unique codebase.
- **Content**: React component patterns, SQL schemas, specific API endpoints, project naming conventions.

## Implementation Guidelines

- **NEVER** include stack-specific dependencies (e.g., "Use Tailwind classes") in a Global file.
- **NEVER** define business logic (e.g., "The discount rule is 10%") in a Global file.
- **ALWAYS** question if a new rule could be applied to a completely different project. If not, it belongs in the Project scope.

<examples>
<bad>Global Rule: "Always use `useState` for local state in React components." (REASON: Stack-specific)</bad>
<good>Global Rule: "Always favor local state over global state unless complexity warrants it." (REASON: General pattern)</good>

<bad>Global Rule: "Format dates using the `date-fns` library." (REASON: Library-specific)</bad>
<good>Global Rule: "Ensure all user-facing dates are consistently formatted according to project conventions." (REASON: Process-oriented)</good>
</examples>
