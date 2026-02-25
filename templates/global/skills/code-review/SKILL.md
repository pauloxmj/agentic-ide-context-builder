---
name: code-review
description: Systematic code review following best practices. Use when reviewing pull requests, checking code quality, or when the user asks for a code review.
---

# Code Review

<instruction>
When reviewing code, follow this systematic checklist. You must first output a `<review_plan>` detailing the specific files you intend to analyze, and then execute the review.
</instruction>

## Review Process

1. **Understand the context**: Read the PR description, linked issues, and related docs before looking at code
2. **Big picture first**: Check architecture and design decisions before line-level details
3. **Check each file**: Apply the review checklist below to every changed file
4. **Summarize findings**: Group feedback into categories (critical, suggestion, question, praise)

## Review Checklist

### Correctness
- Does the code do what the description says it does?
- Are all edge cases handled? (null, empty, boundary values)
- Are error conditions handled gracefully?
- Does the logic match the business requirements?

### Security
- Is user input validated and sanitized?
- Are there any SQL injection or XSS vulnerabilities?
- Are secrets or credentials exposed?
- Are proper authorization checks in place?

### Performance
- Are there unnecessary database queries or API calls?
- Are there N+1 query patterns?
- Are expensive operations cached where appropriate?
- Are there potential memory leaks?

### Maintainability
- Is the code easy to understand without explanation?
- Are names descriptive and consistent?
- Is there unnecessary complexity that could be simplified?
- Does it follow the project's established patterns?

### Testing
- Are there tests for the new/changed functionality?
- Do tests cover edge cases and error conditions?
- Are tests readable and well-organized?

## Feedback Format

When providing feedback, use this format:

- **🔴 Critical**: Must fix before merging — bugs, security issues, data loss risks
- **🟡 Suggestion**: Improvement recommendation — refactoring, better patterns, readability
- **🔵 Question**: Asking for clarification — design decision, naming choice, edge case
- **🟢 Praise**: Something well-done — clean code, good test coverage, smart solution

Always provide specific line references and code suggestions when possible.
