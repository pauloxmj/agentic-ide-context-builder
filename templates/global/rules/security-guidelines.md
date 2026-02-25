# Security Guidelines

> Global rule — applies to all projects.

## Secrets Management

- **NEVER** commit secrets, API keys, tokens, or credentials to git
- Use environment variables (`.env`) for all secrets
- Add `.env`, `.env.*`, `*.pem`, `*.key`, `credentials.json` to `.gitignore`
- Use a secrets manager (Vault, AWS SSM, etc.) in production

## Restricted Files

The following files and patterns MUST NOT be read, output, or modified by the AI agent:

- `.env` and `.env.*`
- `credentials.json`, `secrets.json`
- `*.pem`, `*.key`, `*.p12`
- `secrets/` directory
- Any file containing API keys, tokens, or passwords

## Input Validation

- Validate all user input at service boundaries
- Use allowlists over denylists when possible
- Sanitize data before database queries (parameterized queries, never string interpolation)
- Validate and sanitize HTML output to prevent XSS

## Authentication & Authorization

- Never store passwords in plain text — use bcrypt or argon2
- Implement proper session management with secure, httpOnly cookies
- Apply principle of least privilege for all access controls
- Always verify authorization on the server side, never trust client-side checks

## Dependencies

- Keep dependencies up to date; run `npm audit` / equivalent regularly
- Review new dependency licenses before adding
- Prefer well-maintained packages with active communities
- Pin dependency versions in production
