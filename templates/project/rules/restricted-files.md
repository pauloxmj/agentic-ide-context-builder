# Restricted Files

> Project rule — defines files and directories the AI agent must NOT access.

## Sensitive Files

The following files contain sensitive data and **MUST NOT** be read, modified, or output:

- `.env` and `.env.*`
- `credentials.json`
- `secrets/` directory
- `*.pem`, `*.key`, `*.p12`
- `firebase-adminsdk-*.json`
- `service-account-*.json`

## Protected Directories

The following directories should only be modified with explicit user confirmation:

- `migrations/` — Database migrations must be reviewed carefully
- `scripts/deploy/` — Deployment scripts are critical infrastructure
- `config/production/` — Production configuration requires careful review

## Configuration Files

These files should only be modified when explicitly requested:

- `package.json` — Only modify dependencies when asked
- `tsconfig.json` / `pyproject.toml` — Compiler/tool config changes need justification
- `.github/workflows/` — CI/CD pipeline changes require explicit approval
- `docker-compose.yml` / `Dockerfile` — Container config changes need review

## Rules for the Agent

- Never output the contents of restricted files in responses
- If a restricted file is referenced in code, note its existence but do not read it
- Always ask for confirmation before modifying protected files
- When creating new files that will contain secrets, remind the user to add them to `.gitignore`
