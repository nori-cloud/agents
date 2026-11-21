## What am I looking at?

Repository guidance for `nori-cloud/agents`. Human setup is in [README.md](README.md). Shared user rules live in [instructions/AGENTS.md](instructions/AGENTS.md); do not load this root file as global instructions.

## Where do changes belong?

| Path | Purpose |
| --- | --- |
| `skills/<name>/` | Skill instructions and supporting files. |
| `skills/index.json` | OpenCode skill versions and downloadable files. |
| `instructions/AGENTS.md` | Shared user instructions. |

Only OpenCode is supported; there is no Claude Code or OMP plugin. Keep one skill tree and one hand-maintained catalog; no generator or custom installer. The catalog URL points to the directory containing `index.json`; files resolve as `<base-url>/<name>/<file>`.

For local testing, OpenCode can use the absolute `skills` path instead of the README's remote skill URL. Skills are loaded with `@make-pr`. OpenCode combines configured remote instructions with local `AGENTS.md` files, so avoid duplicate guidance.

## How are releases maintained?

- List every skill file, including supporting files, in the catalog.
- Increment the affected skill's version whenever its files change to refresh the HTTP cache.
- Edit skill content only in its canonical directory. Explicit OpenCode sources override matching IDs from discovered directories.

## Is there any external references to this documentation?

- [OpenCode skills](https://opencode.ai/docs/skills/) — catalog format and discovery.
