---
description: Universal testing philosophy. Apply this rule when writing tests, refactoring, or defining system boundaries across any language or framework.
globs: "*{test,spec}.{ts,tsx,js,jsx,py,go,java,cpp}"
---
# Testing Philosophy

Tests protect developers from regressions and document intended component behavior. They must be resilient and easy to understand.

## Strategies

- **Behavior Over Implementation**: Test the "What" and the "Boundary" (inputs and outputs). Do not test the "How" (private class methods, internal hook states, or hyper-specific DOM structures). Refactoring internal logic should NEVER break a well-written test.
- **Regression Prevention**: Whenever fixing a bug across the project, the workflow must be: 
  1. Write a test that proves the bug exists (it fails).
  2. Implement the fix.
  3. Guarantee the test is now green.
- **The AAA Pattern**: Structure your test suites strictly using `Arrange`, `Act`, and `Assert`. Use blank lines between these phases to maximize readability.
- **Mocking Strategy**: Only mock hard boundaries (Network calls, third-party wrappers, heavy dependency chains). Rely heavily on integration testing for the rest to simulate genuine user flows.
