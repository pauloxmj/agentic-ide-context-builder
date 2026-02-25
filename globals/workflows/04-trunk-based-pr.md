---
description: This workflow outlines the Trunk-Based Development standard for PR creation and merging. Use this workflow when opening pull requests or integrating code changes.
---
# Trunk-Based PR Lifecycle

This repository uses Trunk-Based Development. All code integrates directly into the `main` branch. Long-lived branches (like `develop` or release branches) are prohibited.

## Workflow Rules

1. **Short-Lived Branches**: All feature branches must be scoped to a single logical change and merged as quickly as possible (typically within 1-2 days).
2. **Direct to Main**: Open Pull Requests directly against `main`. There is no `develop` or `integration` branch.
3. **Feature Flags**: For incomplete features that cannot be deployed to users, merge the code into `main` hidden behind a feature flag or conditional logic rather than keeping a branch open.
4. CI Checks: Ensure all required CI checks (linting, tests, build verifications) pass before merging.
5. No Broken Windows: The `main` branch MUST stay deployable at all times.
6. **Manual Merge Trigger**: The agent MUST NOT perform the merge automatically. Integration to `main` happens only after an explicit user command.

## Creating a PR

1. Ensure your branch is up to date with `main`: `git pull origin main --rebase`
2. Title your PR according to the Conventional Commits standard (e.g., `feat(auth): add google sign in`).
3. If the feature is incomplete or experimental, document the feature flag in the PR description.
4. Review against the Definition of Done (i18n, accessibility, automated tests).
5. Open the PR and wait for user review. When asked to merge, use **Squash & Merge** to keep the `main` history clean and linear.
