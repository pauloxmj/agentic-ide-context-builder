# Coding Standards

<system_context>
> Global rule — applies to all projects regardless of language or framework.
</system_context>

<instruction>
When editing or producing code, you must strictly follow the architectural patterns and naming conventions defined below. Do not explain the changes unless requested; simply output the refactored or new code matching these standards.
</instruction>

## General Principles

- Write self-documenting code; use comments only for "why", not "what"
- Prefer composition over inheritance
- Keep functions under 30 lines; extract helpers when they grow
- Single Responsibility: each function/class does one thing well
- DRY: extract shared logic into utilities; never copy-paste code

## Naming Conventions

- **Variables and functions**: `camelCase`
- **Classes, interfaces, types**: `PascalCase`
- **Constants**: `SCREAMING_SNAKE_CASE`
- **File names**: `kebab-case` (e.g., `user-service.ts`, `auth-middleware.py`)
- **Boolean variables**: prefix with `is`, `has`, `should`, `can` (e.g., `isActive`, `hasPermission`)
- **Event handlers**: prefix with `handle` or `on` (e.g., `handleClick`, `onSubmit`)

## Code Style

- Use `const` by default; use `let` only when reassignment is needed; never use `var`
- Prefer early returns to reduce nesting
- Prefer `===` over `==` (or language equivalent)
- Maximum line length: 100 characters
- Use trailing commas in multi-line structures
- Group imports: external libraries → internal modules → relative imports

## Error Handling

- Always handle errors explicitly; never swallow exceptions silently
- Use typed/custom error classes for domain-specific errors
- Log errors with context: user ID, operation name, timestamp
- Prefer `try/catch` at service boundaries, not around every line

## Git Practices

- Write descriptive commit messages: `type(scope): description`
- Types: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `style`
- One logical change per commit
- Never commit secrets, credentials, or environment files
