---
description: Safety guardrails and procedural steps for executing large refactors without introducing regressions.
---
# Refactoring Standard Workflow

Use this workflow whenever the AI agent or the user proposes an architectural refactor spanning multiple files or complex logic structures.

<steps>
1. **Assert Coverage**: Ensure the module you are about to refactor is covered by automated unit or integration tests. If there are no tests, inform the user you must establish a testing baseline before altering the code.
2. **Single-Responsibility Alteration**: Do not introduce new features or fix unrelated bugs in the exact same commit as a major structural refactor. Keep the changes strictly atomic.
3. **Execution (The Boy Scout Rule)**: 
   - Rename variables for maximal clarity. 
   - Extract sprawling components into discrete, composable UI pieces.
   - Separate data-fetching layers from rendering layers.
4. **`<reflection>` Checkpoint**: Halt and re-run all existing formatters, linters, and the test suite to ensure your structural modifications resulted in zero build breakages or runtime regressions. Correct any failures before declaring the structural refactor a success.
</steps>
