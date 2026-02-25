# PR Submission

<system_context>
> Global workflow — reusable across all projects.

**Description**: Prepare and submit a pull request with quality checks.
</system_context>

<instruction>
Execute the following steps sequentially. Do not skip any steps.
</instruction>

## Steps

1. **Check for debug artifacts**: Search for `console.log`, `debugger`, `print()`, `TODO`, and `FIXME` in changed files. List any found.

2. **Run linter**: Execute the project's lint command (e.g., `npm run lint`, `ruff check .`). Fix any errors before proceeding.

3. **Run tests**: Execute the project's test command (e.g., `npm test`, `pytest`). All tests must pass.

4. **Review diff**: Run `git diff --staged` and summarize the changes in bullet points.

5. **Commit**: Write a commit message following conventional commits format:
   ```
   type(scope): brief description
   
   - Detail 1
   - Detail 2
   ```

6. **Push**: Push the current branch to the remote.

7. **Create PR**: Use `gh pr create` with:
   - A descriptive title based on the changes
   - A body summarizing what changed and why
   - Request reviewers if specified by the user

8. **Report**: Output the PR URL and a summary of what was submitted.
