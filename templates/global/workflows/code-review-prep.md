# Code Review Preparation

> Global workflow — reusable across all projects.

## Description

Run pre-review quality checks before submitting code for review.

## Steps

1. **Scan for debug statements**: Search all changed files for:
   - `console.log`, `console.debug`, `console.warn` (JavaScript/TypeScript)
   - `print()`, `breakpoint()` (Python)
   - `debugger` statements
   - `TODO`, `FIXME`, `HACK` comments
   Report any findings.

2. **Run linter**: Execute the project linter and report warnings/errors.

3. **Run formatter check**: Run the project formatter in check mode (e.g., `prettier --check`, `ruff format --check`). Report any unformatted files.

4. **Run test suite**: Execute the full test suite. Report results with pass/fail counts.

5. **Check file sizes**: Flag any files that have grown over 300 lines of code.

6. **Check for large functions**: Flag functions over 50 lines.

7. **Summarize changes**: Create a bullet-point summary of all changes organized by file/feature.

8. **Flag risks**: Identify potential risks:
   - Database migrations
   - API breaking changes
   - New dependencies added
   - Changes to authentication or authorization logic
   - Changes to payment or billing code

9. **Generate review checklist**: Output a checklist for the reviewer highlighting areas to focus on.
