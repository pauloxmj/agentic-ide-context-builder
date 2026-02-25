---
description: Standardized steps for approaching a bug, executing Root Cause Analysis (RCA), and implementing a fix safely.
---
# Bug Resolution & RCA Workflow

Whenever the user reports a bug, exception, or unexpected behavior, execute this workflow explicitly before attempting a fix.

<steps>
1. **Information Gathering**: Read the latest stack traces or error logs provided by the user. If they haven't provided enough context (e.g. they say "it doesn't work"), ask for the specific CLI output or browser console logs before hallucinating a fix.
2. **Reproduction Hypothesis**: Formulate a hypothesis on what specifically broke. State it clearly. (e.g., *"It appears the user object is null before the component mounts."*)
3. **Isolation & Verification**: Use file reading tools (`view_file`, `grep_search`) to locate the exact lines of code where the error originates.
4. **Test-Driven Fix**: Before modifying the implementation, consider writing or proposing an automated test that catches the bug.
5. **Atomic Resolution**: Implement the minimum necessary change to fix the isolated bug. Do not rewrite large chunks of the file or change the prevailing architecture unless strictly necessary.
6. **`<reflection>` Checkpoint**: Re-run the test suite, execution environment, or linter to definitively prove the newly applied patch resolves the condition. DO NOT skip this step.
7. **Root Cause Analysis (RCA)**: Explain to the user the *Why* in 1-2 concise sentences. Do not just output the code change block. Explain the failure mechanism to educate the user.
</steps>
