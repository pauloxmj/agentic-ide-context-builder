<template scope="any" target="skill">
---
name: [skill-name] # Max 64 chars, lowercase
description: [1-2 sentences explaining what capability this adds. This is what the agent reads to decide if it should trigger the skill.] # Max 1024 chars
---

# [Skill Title]

When invoked or deemed necessary, follow these exact instructions to [do the thing].

## 1. Analysis Phase
- Review the current state of [target area].
- Identify [key components].

## 2. Execution Phase
- Steps to perform.
- If a script is bundled, direct the agent: `Execute ./scripts/[script-name].sh`

## 3. Verification Phase
- Confirm [outcome].

> *Note: For deep technical context, instruct the agent to read `./references/DETAILS.md` rather than polluting this root file.*
</template>
