---
title: Shared agent resources
description: Shared user instructions and OpenCode skills for nori-cloud.
---

## What am I looking at?

Shared user instructions and skills for **OpenCode**. Instructions are loaded
remotely from this repository; skills are loaded from its catalog.

## How do I use it?

Merge this into `~/.config/opencode/opencode.json`:

```json
{
  "instructions": ["https://raw.githubusercontent.com/nori-cloud/agents/main/instructions/AGENTS.md"],
  "skills": ["https://raw.githubusercontent.com/nori-cloud/agents/main/skills/"]
}
```

Browse the [skill catalog](skills.md). Maintenance rules are in the
[repository guidance](../AGENTS.md).

## Is there any external references to this documentation?

- [nori-cloud/agents](https://github.com/nori-cloud/agents) — the repository.
- [Shared instructions](https://github.com/nori-cloud/agents/blob/main/instructions/AGENTS.md) — the rules every session loads.
- [OpenCode skills](https://opencode.ai/docs/skills/) — catalog format and loading.
