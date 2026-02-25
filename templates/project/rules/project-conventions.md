# Project Conventions

> Project rule — customize for your specific project. Replace placeholders with your actual stack details.

## Stack

<!-- Update these to match your project -->
- **Language**: TypeScript
- **Framework**: React / Next.js
- **Styling**: CSS Modules / Tailwind CSS
- **State Management**: Zustand / React Context
- **Testing**: Jest + React Testing Library
- **Package Manager**: pnpm

## Project Structure

```
src/
├── app/          # Next.js App Router pages
├── components/   # Reusable UI components
├── features/     # Feature-specific modules
├── hooks/        # Custom React hooks
├── lib/          # Utility functions and helpers
├── services/     # API clients and external service integrations
├── types/        # Shared TypeScript types and interfaces
└── styles/       # Global styles and design tokens
```

## Naming Conventions

- **Components**: `PascalCase.tsx` (e.g., `UserProfile.tsx`)
- **Hooks**: `use` prefix, `camelCase.ts` (e.g., `useAuth.ts`)
- **Utilities**: `camelCase.ts` (e.g., `formatDate.ts`)
- **Types**: `PascalCase.ts`, suffix with `.types.ts` for shared types
- **Tests**: `*.test.ts` or `*.test.tsx`, colocated with source files
- **Styles**: `*.module.css`, colocated with components

## Import Order

1. React / framework imports
2. Third-party libraries
3. Internal modules (absolute paths)
4. Relative imports
5. Style imports
6. Type imports (`import type`)

## Component Patterns

- Use functional components with hooks
- Props interface must be exported
- One component per file
- Colocate styles, tests, and stories with components
- Use `forwardRef` when components need ref access
