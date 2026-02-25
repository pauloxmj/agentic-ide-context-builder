---
description: This rule enforces Trunk-Based Development principles. Apply this rule whenever planning new features, creating branches, or managing the git history.
globs: "*"
---
# Trunk-Based Development Protocol

All generated projects and workflows must enforce Trunk-Based Development unless explicitly stated otherwise by the user.

## Core Directives

1. **Single Source of Truth**: The `main` branch is the only long-lived integration branch. Do NOT generate or propose GitFlow branching strategies (such as `develop`, `release/*`, or `hotfix/*` branches).
2. **Short-Lived Feature Branches**: New work must happen in small, short-lived branches that merge directly into `main`.
3. **Continuous Integration**: Code must be safe to deploy at any time. If proposing incomplete features, wrap the new logic in a Feature Flag, allowing the code to merge into `main` safely without exposing the incomplete UI/API to end users.
4. **Manual Merge Trigger**: The agent MUST NOT merge any branch into `main` automatically. All code integration to `main` requires an explicit user command.
5. **Merge Strategy**: When explicitly asked to merge, the agent MUST use the **Squash & Merge** strategy to keep the `main` history clean, linear, and atomic.
6. **PR Conventions**: Assume all PRs target `main`. Keep diffs small and atomic.

Whenever writing CI/CD workflows, configuration files, or documentation on how to contribute: ensure that `main` is treated as the sole integration target.
