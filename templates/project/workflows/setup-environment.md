# Environment Setup

> Project workflow — for onboarding new developers.

## Description

Set up the local development environment for a new team member.

## Prerequisites

<!-- Update with your actual prerequisites -->
- Node.js 20+
- pnpm 9+
- Docker Desktop
- Git

## Steps

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd <project-name>
   ```

2. **Install dependencies**:
   ```bash
   pnpm install
   ```

3. **Set up environment variables**:
   - Copy `.env.example` to `.env.local`
   - Ask the team lead for required secret values
   - Fill in all required variables

4. **Start local services** (database, cache, etc.):
   ```bash
   docker-compose up -d
   ```

5. **Run database migrations**:
   ```bash
   pnpm db:migrate
   ```

6. **Seed development data**:
   ```bash
   pnpm db:seed
   ```

7. **Verify the setup** by running the test suite:
   ```bash
   pnpm test
   ```

8. **Start the development server**:
   ```bash
   pnpm dev
   ```

9. **Verify the application** loads at `http://localhost:3000`

10. **Read the project documentation**:
    - `README.md` for project overview
    - `docs/architecture.md` for architecture decisions
    - `.cursor/rules/` or `.claude/rules/` for AI agent conventions
