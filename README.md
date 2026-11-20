## What am I looking at?

Shared instructions and skills for **Claude Code, OpenCode, and OMP**. This repository keeps one skill source and two hand-maintained catalogs; it has no generator, custom installer, or package dependencies.

This setup has not published the repository or deployed an HTTP endpoint. Use the local instructions below; remote marketplace registration is only appropriate after publication.

## Where is the source?

```text
instructions/AGENTS.md                 Shared agent instructions
.claude-plugin/marketplace.json        Claude Code / OMP marketplace
plugins/nori/.claude-plugin/plugin.json
plugins/nori/skills/index.json         OpenCode HTTP catalog
plugins/nori/skills/<name>/SKILL.md     Canonical skills and supporting files
```

The five skills are `cli-gh`, `find-skills`, `herdr`, `make-pr`, and `markdown-documentation`. Claude Code and OMP discover the plugin's `skills/` directories; OpenCode reads those same directories locally or through the HTTP catalog. There are no per-tool skill copies to maintain in this repository.

## How do I install from a local checkout?

These commands use the initial absolute checkout path. Substitute your checkout's absolute path if it differs.

Keep the existing dotfile skills and symlinks during setup and verification. OpenCode's explicit `skills` source takes precedence over matching IDs from the dotfile directories. Confirm the registered skill paths and supporting files come from this repository before a separate dotfile cleanup; do not remove the old copies during this stage.

### Claude Code

```sh
claude plugin marketplace add /home/norris/git/nori-cloud/agents
claude plugin install nori@nori-cloud
```

### OMP

```sh
omp plugin marketplace add /home/norris/git/nori-cloud/agents
omp plugin install nori@nori-cloud
```

Both use the native `nori-cloud` marketplace and its single `nori` plugin. Local installation does not require publishing or accessing GitHub.

Claude Code namespaces plugin commands, for example `/nori:make-pr`. OpenCode loads the skill with `@make-pr`; OMP keeps the skill name `make-pr`.

### OpenCode

Merge this into your OpenCode configuration, for example `~/.config/opencode/opencode.json`. Use the native `skills` array, not an additional plugin or installer:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": [
    "/home/norris/git/nori-cloud/agents/plugins/nori/skills"
  ]
}
```

This local path is the simplest private/offline setup. It includes supporting files directly from the checkout. Avoid registering duplicate skill sources unless you intend OpenCode's later sources to override earlier ones.

## Can I use the HTTP catalog locally?

Yes, optionally. With Python already installed, run this server in a separate terminal:

```sh
python3 -m http.server 8765 --bind 127.0.0.1 --directory /home/norris/git/nori-cloud/agents/plugins/nori/skills
```

Use this OpenCode configuration **instead of** the local skills path:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["http://127.0.0.1:8765/"]
}
```

Keep the server running while OpenCode fetches the catalog. It serves `index.json` and resolves each file as `<base-url>/<name>/<file>`, directly from the canonical skill directories. This loopback-only example is not a deployed site and does not require a new package dependency.

## How are shared instructions installed?

The marketplace installs skills, **not** `instructions/AGENTS.md`. This repository contains a copy of the shared instructions; the current dotfiles setup still links its own `agents/AGENTS.md`. Leave those instruction links unchanged during skill verification. OpenCode can load a trusted HTTP(S) Markdown URL through its `instructions` array once hosting is available; this setup does not configure a remote instruction URL yet.

## How do I maintain and update the catalogs?

Edit the canonical skill files once. Maintain these two catalogs by hand:

- `.claude-plugin/marketplace.json` lists `nori` at `./plugins/nori`, initially version `0.1.0`. Keep that version aligned with `plugins/nori/.claude-plugin/plugin.json`; bump both when releasing plugin changes.
- `plugins/nori/skills/index.json` lists each OpenCode skill, its version string, and every downloadable file. Increment the affected skill's version whenever its files change so OpenCode refreshes its HTTP cache.

The native plugin includes its skill directories and supporting files. The HTTP catalog must enumerate supporting files explicitly: `cli-gh` includes `agents/openai.yaml` and `references/version.txt` as well as `SKILL.md`. Add any future supporting files to the relevant catalog entry. The other four skills currently need only `SKILL.md`.

Refreshing a marketplace updates its catalog; it is not the same as upgrading an installed OMP plugin. Refresh the catalog, then apply the plugin release:

```sh
omp plugin marketplace update nori-cloud
omp plugin upgrade nori@nori-cloud
```

Claude Code local marketplace edits become available on a new session or `/reload-plugins`. For published installs, use the tool's native marketplace update and plugin update workflow. OpenCode HTTP updates depend on the per-skill version strings; local-path sources read the checkout directly.

## What existing limitations should I know about?

`cli-gh` references the `yeet` and `repo-rename` skills, which are not included in this five-skill collection. Those existing references are preserved unchanged; installation does not supply those skills or fabricate replacements. Workflows requiring them need separately available skills.

## Is there any external references to this documentation?

- [Claude Code marketplaces](https://code.claude.com/docs/en/plugin-marketplaces) — native local marketplace setup and publication.
- [Claude Code plugin manifests](https://code.claude.com/docs/en/plugins/manifest-reference) — plugin metadata.
- [OpenCode skills](https://opencode.ai/docs/skills/) — local sources, the current `skills` array, HTTP catalogs, and cache versions.
- [OpenCode instructions](https://opencode.ai/docs/instructions/#configuration) — local and remote instruction sources.
