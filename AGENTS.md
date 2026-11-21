## What am I looking at?

Repository guidance for `nori-cloud/agents`. Human setup is in [README.md](README.md). Shared user rules live in [instructions/AGENTS.md](instructions/AGENTS.md); do not load this root file as global instructions.

## Where do changes belong?

| Path | Purpose |
| --- | --- |
| `skills/<name>/` | Skill instructions and supporting files. |
| `.claude-plugin/marketplace.json` | Claude Code/OMP catalog. |
| `.claude-plugin/plugin.json` | Native plugin metadata and version. |
| `skills/index.json` | OpenCode skill versions and downloadable files. |

The repository root is the `nori` plugin: keep one skill tree and two hand-maintained catalogs; no generator or custom installer. Catalog URLs point to the directory containing `index.json`; files resolve as `<base-url>/<name>/<file>`.

## How do other harnesses install skills?

```sh
claude plugin marketplace add nori-cloud/agents
claude plugin install nori@nori-cloud
omp plugin marketplace add nori-cloud/agents
omp plugin install nori@nori-cloud
```

For local testing, replace the marketplace source with the checkout's absolute path. OpenCode can use the absolute `skills` path instead of the README's remote skill URL.

Claude Code namespaces commands, such as `/nori:make-pr`; OpenCode uses `@make-pr`, and OMP keeps `make-pr`. OpenCode combines configured remote instructions with local `AGENTS.md` files, so avoid duplicate guidance.

## How are releases maintained?

- Keep the marketplace entry and native plugin versions aligned; bump both for plugin releases.
- List every skill file, including supporting files, in the OpenCode catalog. Increment the affected skill's version whenever its files change to refresh the HTTP cache.
- Edit skill content only in its canonical directory. Explicit OpenCode sources override matching IDs from discovered directories.

OMP needs both catalog refresh and plugin upgrade:

```sh
omp plugin marketplace update nori-cloud
omp plugin upgrade nori@nori-cloud
```

Claude Code local edits need a new session or `/reload-plugins`; published installs use its native update workflow.

## What checks are needed?

There is no repository build or test runner.

- Validate JSON manifests, matching native versions, and complete catalog file lists.
- For native packaging changes: `claude plugin validate .` and `claude plugin validate .claude-plugin/marketplace.json`.
- For OpenCode setup: inspect `opencode debug config` and `opencode api skill.list` after initialization. Remote skills must resolve inside the download cache; check supporting files against published content.
- Keep dotfile copies and links until verification and a separate cleanup request. Their presence can hide failed remote loading.

## What limitations matter?

`cli-gh` references unbundled `yeet` and `repo-rename` skills. Loading skills does not verify every workflow.

## Is there any external references to this documentation?

- Claude Code: [marketplaces](https://code.claude.com/docs/en/plugin-marketplaces), [manifests](https://code.claude.com/docs/en/plugins/manifest-reference).
- OpenCode: [skills](https://opencode.ai/docs/skills/), [instructions](https://opencode.ai/docs/instructions/#configuration).
