---
title: Skills
description: The shared OpenCode skills in the agents catalog and what each is for.
---

## What am I looking at?

The skill catalog for this repository. Skills live in
[`skills/`](../skills/index.json), one folder each, not in `docs/`. Load one by
mentioning it as `@<name>` in a prompt, or let the agent pick it from its description.

## Which skills are available?

| Skill | Purpose |
| --- | --- |
| [`cli-gh`](../skills/cli-gh/SKILL.md) | GitHub CLI automation: repository reads, workflow runs, search, releases, and command syntax. |
| [`find-skills`](../skills/find-skills/SKILL.md) | Discover and install agent skills when you ask how to do something. |
| [`herdr`](../skills/herdr/SKILL.md) | Control Herdr panes, tabs, workspaces, and other agents. Only when Herdr is mentioned. |
| [`make-pr`](../skills/make-pr/SKILL.md) | Write concise pull request descriptions readable in under three minutes. |
| [`markdown-documentation`](../skills/markdown-documentation/SKILL.md) | Apply the documentation style and layouts when creating or editing Markdown. |

## How do I add or change a skill?

Edit the skill only in its own folder, list every file in
[`skills/index.json`](../skills/index.json), and increase that skill's `version` so
OpenCode refreshes its cache. Then update the table above.

## Is there any external references to this documentation?

- [OpenCode skills](https://opencode.ai/docs/skills/) — catalog format and loading.
