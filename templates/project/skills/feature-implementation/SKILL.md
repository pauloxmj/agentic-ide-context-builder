---
name: feature-implementation
description: Guide for implementing new features following project patterns and conventions. Use when building new features, adding new endpoints, creating new components, or when the user says they want to build something new.
---

# Feature Implementation

Follow this process when implementing a new feature to ensure consistency with project patterns.

## Before Starting

1. **Understand the requirement**: Read the ticket/issue/description thoroughly
2. **Check existing patterns**: Look for similar features in the codebase and follow their patterns
3. **Plan the approach (Orchestrator Mode)**: Break the feature into small, testable increments using the `<plan>` XML tag. Do not begin writing code until the `<plan>` has been approved by the user.

<instruction>
You are acting as the primary Orchestrator. After the user approves your plan, execute the following steps in order. For massive features, you may instruct the user to spin up specialized sub-agents to handle specific steps (e.g., a documentation agent for Step 7).
</instruction>

## Implementation Process

### Step 1: Define the Types

Start by defining the data types and interfaces:
- Create or update types in the `types/` directory
- Ensure types are exported and well-documented
- Use strict typing — avoid `any`

### Step 2: Build the Domain Logic

Write the business logic first:
- Create domain entities and value objects as needed
- Write validation rules
- Keep this layer framework-free

### Step 3: Build the Data Layer

Implement data access:
- Create or update repository interfaces
- Implement repository methods
- Add database migrations if needed

### Step 4: Build the Service Layer

Create the application logic:
- Implement use cases / service methods
- Handle orchestration, validation, and error cases
- Keep services focused on a single capability

### Step 5: Build the Presentation Layer

Implement the UI or API:
- Create components / routes / endpoints
- Connect to services via hooks or controllers
- Handle loading, error, and empty states

### Step 6: Write Tests

Create tests at each layer:
- Unit tests for domain logic
- Integration tests for service layer
- Component / E2E tests for presentation

### Step 7: Review and Refine

Before submitting:
- Run the full test suite
- Check for consistency with existing patterns
- Ensure documentation is updated
- Verify error handling is complete

## Decision Framework

When in doubt about approach:

| If... | Then... |
|-------|---------|
| Similar feature exists | Follow its pattern exactly |
| No similar feature | Check architecture guidelines |
| Pattern seems wrong | Ask the user before deviating |
| Performance concern | Profile first, optimize second |
| Multiple valid approaches | Choose the simplest one |

## Anti-Patterns to Avoid

- ❌ Skipping types and using `any`
- ❌ Putting business logic in UI components
- ❌ Bypassing the service layer for "quick" data access
- ❌ Creating features without tests
- ❌ Ignoring error states and edge cases
