---
description: IDE capabilities and path configurations for GitHub Copilot.
---

<ide_target name="github-copilot">
# GitHub Copilot Specifics

## Paths & Storage

<ide_quirk type="rule">
- **Project Rules**: `.github/copilot-instructions.md` (Multiple files in `.github/` are parsed sequentially).
- **Global Rules**: Settings-level configuration (potentially `~/.copilot/copilot-instructions.md`).
- **Organization Rules**: Set at the GitHub Organization level (Copilot Enterprise).
</ide_quirk>

## Native Capabilities

<ide_quirk type="precedence">
- **Rule Resolution Order (Highest to Lowest)**:
  1. Organization instructions
  2. Repository instructions
  3. Personal instructions
  4. Chat prompt context
</ide_quirk>

<ide_quirk type="context_injection">
- **Implicit Context**: Automatically gathered background data (open tabs, highlighted code).
- **Explicit Context**: Pinned scopes using `@workspace` (scan entire solution) or `#file:utils.ts` (focus specific file).
</ide_quirk>

<ide_quirk type="skill">
- **Agent Skills**: Parses the root `SKILL.md` of folders to invoke specific terminal sequences or instructions.
</ide_quirk>

<ide_quirk type="mcp">
- **MCP**: Supports reading external, authenticated databases and issue trackers directly.
</ide_quirk>

<ide_quirk type="documentation">
- **Official AI Docs**: `https://docs.github.com/en/copilot`
- **Usage**: Since Copilot lacks a standardized `llms.txt`, use the official GitHub documentation as the primary source of truth for its rule ingestion mechanics.
</ide_quirk>
</ide_target>
