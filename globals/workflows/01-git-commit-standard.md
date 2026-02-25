---
description: Standardized steps for writing Conventional Commits. Use this workflow right before or during a git commit operation.
---
# Git Commit Standard

Ensures all commits generated or suggested by the agent follow the Conventional Commits standard, maintaining a highly readable and automated git history.

## Steps

1. Analyze the staged changes to determine the exact scope and nature of the modifications.
2. Select the correct type keyword: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, or `revert`.
3. Determine the scope (optional but recommended): The specific module or area affected (e.g., `auth`, `ui`, `api`).
4. Write a concise subject line in the imperative mood, all lowercase, with no period at the end.
5. Combine into the final format: `type(scope): subject line`
6. Output the suggested git command: `git commit -m "<message>"