---
description: Validation frameworks and security protocols. Apply this rule when writing APIs, database queries, or type definitions.
globs: "*{.ts,.tsx,.js,.jsx,.py,.go,.java,.cpp}"
---
# Post-Coding Validation

Before concluding any coding activity, submitting a Pull Request, or declaring a task complete, you must ensure the code passes all static analysis and type checks.

## Discovery and Execution

- **Inspect Manifests**: Always read the `package.json` (or equivalent project manifest) to identify the specific scripts designated for linting, formatting, and typechecking (e.g., `npm run lint`, `pnpm typecheck`, `yarn check`).
- **Execute Safely**: Run these identified commands in the terminal. Do not skip this step, even for minor changes.

## Remediation

- **Auto-Fix First**: If the project has an auto-fix command (e.g., `biome check --write` or `eslint --fix`), run it to resolve formatting and basic linting issues automatically.
- **Zero Warnings Policy**: If the typechecker or linter outputs errors or warnings, you must proactively fix them. 
- **Do Not Hallucinate Fixes**: If a type error is complex and requires architectural context you do not possess, stop and ask the user for clarification. Do not use `@ts-ignore` or `any` to bypass the error.

### Examples

**BAD**: "I've updated the component. Let me know if you need anything else!" (Without running `tsc` or the linter).

**GOOD**: 
1. *Checks `package.json` and finds `"lint": "biome check src/"` and `"typecheck": "tsc --noEmit"`*
2. *Runs both commands.*
3. *Notices a missing dependency in a `useEffect` array.*
4. *Fixes the warning, runs the commands again to ensure a clean exit code, and then informs the user the task is complete.*