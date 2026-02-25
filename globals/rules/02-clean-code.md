---
description: Clean code principles, SOLID, semantic naming, and defensive coding. Apply this rule when writing or refactoring any code.
globs: "*{.ts,.tsx,.js,.jsx,.py,.go,.java,.cpp}"
---
# Clean Code Principles

Adhere strictly to standard software engineering patterns to ensure maintainability and readability across all codebases.

## Architecture Standards

- **SOLID Principles**: Adhere to SOLID for all class and component designs.
  - **SRP**: Single Responsibility Principle (One module/function = one job).
  - **OCP**: Open/Closed Principle (Open for extension, closed for modification).
  - **DIP**: Dependency Inversion (Depend on abstractions/interfaces, not concretions).
- **DRY (Don't Repeat Yourself)**: Abstract repeated logic sensibly, but avoid premature optimization.
- **Pure Functions**: Prefer functional, immutable patterns. Avoid side effects wherever possible.

## Syntax and Error Handling

- **Defensive Coding**: Validate arguments at the very start of functions (fail fast).
- **Try/Catch**: Wrap external API calls or unstable operations. Throw descriptive, actionable errors.
- **Modern Syntax**: Prefer `async/await` over `.then()`. Use optional chaining (`?.`) and nullish coalescing (`??`).

## Naming Conventions

- **Semantic Iterators**: Never use single-letter variable names in iterators or callbacks (`map`, `filter`, `reduce`, `forEach`).
- **Booleans**: Prefix with `is`, `has`, `can`, or `should` (e.g., `isValidUser`).
- **Constants**: Use `SCREAMING_SNAKE_CASE` for magic numbers or global static values.
- **Functions**: Use the Verb-Noun pattern (e.g., `fetchUserData`, `handleClick`).
- **Events**: Prefix event handlers with `handle` (e.g., `handleSubmit`, `handleKeyDown`).

## General Cleanliness

- **No Magic Numbers**: Extract hard-coded numbers and strings into descriptive constants.
- **Early Returns**: Use Guard Clauses to avoid deep nesting and flatten logic.
- **Comments**: Avoid redundant comments that describe *what* the code does (e.g., `// Increment i`). Write "Why" comments to explain business logic or edge cases. Use standard docstrings for public interfaces.

### Examples

**BAD**: `users.map(u => u.id)`
**GOOD**: `users.map(user => user.id)`

**BAD**: `const total = price * 0.1;`
**GOOD**: 
```javascript
const TEN_PERCENT_DISCOUNT = 0.1;
const total = price * TEN_PERCENT_DISCOUNT;