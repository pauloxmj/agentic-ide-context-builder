# Architecture Guidelines

> Project rule — customize for your specific project's architecture decisions.

## Architectural Pattern

<!-- Choose and document your architecture pattern -->
This project follows **Clean Architecture** with clear separation of concerns.

<instruction>
When generating, modifying, or refactoring code, you must strictly adhere to the layered architecture constraints defined below. Wait for the user to specify whether they want you to act as an Orchestrator (planning) or Executor (writing) before proceeding.
</instruction>

## Layer Responsibilities

### Domain (`src/domain/`)
- Business entities and value objects
- Business rules and validation logic
- NO framework imports, NO infrastructure dependencies
- Pure functions and classes only

### Application (`src/app/` or `src/features/`)
- Use cases and application logic
- Orchestrates domain and infrastructure
- Defines interfaces that infrastructure must implement

### Infrastructure (`src/services/` or `src/infra/`)
- Database access, API clients, file system
- Implements interfaces defined by the application layer
- External service integrations

### Presentation (`src/components/` or `src/ui/`)
- UI components, pages, layouts
- Handles user input and display logic
- Depends on application layer only

## Dependency Direction

```
Presentation → Application → Domain
                    ↓
              Infrastructure
```

- Domain has **zero** dependencies on other layers
- Infrastructure implements domain interfaces (dependency inversion)
- Presentation never imports from infrastructure directly

## Design Patterns in Use

- **Repository Pattern**: All data access goes through repositories
- **Service Layer**: Business operations are encapsulated in services
- **Factory Pattern**: For complex object creation
- **Observer/Event Pattern**: For cross-module communication

## Key Decisions

<!-- Document important architectural decisions -->
- All API calls go through service classes, never directly from components
- State management is centralized in stores, not scattered in components
- Environment configuration flows through a single config module
- Database migrations are version-controlled and sequential

## Context Boundary Rules

<instruction>
When operating in this repository, follow these context scoping rules:
1. **Implicit Context**: When solving isolated UI bugs, do not scan the entire codebase. Rely on the currently open files.
2. **Explicit Context**: When instructed to make domain/infrastructure changes or when the user uses `@workspace`, perform a full repository scan to ensure you do not break the dependency inversion rules.
</instruction>

## Anti-Patterns to Avoid

- ❌ Direct database queries from UI components
- ❌ Business logic in API route handlers
- ❌ Circular dependencies between modules
- ❌ God objects / classes with more than one responsibility
- ❌ Hardcoded configuration values
