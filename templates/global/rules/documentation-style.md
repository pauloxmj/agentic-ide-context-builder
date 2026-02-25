# Documentation Style

> Global rule — applies to all projects.

## Code Comments

- Use comments to explain **why**, not **what**
- Avoid obvious comments like `// increment counter` above `counter++`
- Document complex algorithms, business rules, and non-obvious decisions
- Use JSDoc / docstrings / equivalent for all public functions and classes

## Function Documentation

Every public function should document:
- **Purpose**: What the function does (one sentence)
- **Parameters**: Each parameter with type and description
- **Returns**: What the function returns
- **Throws**: What errors can be thrown and when
- **Example**: Usage example for non-trivial functions

## README Files

Every project and significant module should have a README with:
- **What it is**: One-paragraph description
- **How to run it**: Setup and run commands
- **How to test it**: Test commands
- **Architecture**: Brief overview of structure and key decisions

## Inline Documentation

- Use `TODO:` for planned improvements (include ticket number if available)
- Use `FIXME:` for known bugs
- Use `HACK:` for temporary workarounds (with explanation of why and when to remove)
- Never use `NOTE:` without context — be specific
