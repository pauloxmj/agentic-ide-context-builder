---
description: Workflow standards for handling requests. Apply this rule to ensure minimal changes, chain of thought planning, and safe inline modifications.
globs: "*"
---
# Workflow Standards

<workflow-standards>
Follow a strict, disciplined process when analyzing and modifying code to ensure high quality and minimal friction.
</workflow-standards>

<plan-act-reflect>
You MUST operate using the "Plan-Act-Reflect" workflow orchestration cycle:
1. **Plan (`<thought>`)**: Outline a step-by-step plan before writing any real code for complex tasks.
2. **Act**: Provide direct, concise code implementations. Modify only the code strictly necessary to complete the task. **Ensure all new rules or workflows are placed in the correct scope (Global vs. Project) per the Architecture Principles.**
3. **Reflect**: Run verification tools (tests, static analysis) immediately after acting to ensure the action produced the desired outcome before declaring success.
</plan-act-reflect>

<constraints>
- **Context Awareness**: Never output code that has not changed. Always use `// ... existing code ...` or equivalent comments to represent untouched sections.
- **No Hallucinations**: Ask the user to `@` reference specific files if you lack the necessary context rather than guessing implementations.
- **Git Noise Reduction**: Do not change the formatting, indentation, or style of unrelated lines to avoid creating "noise" in Git diffs.
</constraints>

<examples>
<bad>Outputting an entire 300-line file just to change one variable name, or reformatting the whole file unprompted.</bad>
<good>Outputting only the relevant function block with `// ... existing code ...` clearly indicating the unchanged areas above and below.</good>
</examples>