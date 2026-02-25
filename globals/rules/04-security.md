---
description: Security principles and secret handling. Apply this rule universally to ensure that no API keys are committed and that external inputs are defensive and validated.
globs: "*"
---
# Security and Secrets Policies

Ensure the overall system posture remains secure and invulnerable to common attack vectors.

## Principles

- **Zero Secrets Policy**: NEVER write or commit hardcoded credentials, API keys, passwords, or connection strings into source code. If required for testing, instruct the user to set them via `.env` or the environment layer.
- **Untrusted Inputs**: Treat all system parameters, user inputs, and external API responses as untrusted. Ensure they are validated before execution.
- **Dependency Trust**: Exercise extreme caution before importing or suggesting new third-party libraries. Stick to standard, major libraries with known security postures rather than obscure tools.
- **OWASP Mindset**: When writing UI, API, or Serverless components, design defensively against Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF), and Injection attacks.
