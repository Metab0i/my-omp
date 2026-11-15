# OMP configuration root

```
%USERPROFILE%\.omp
```

This is the live OMP configuration root. The active agent directory is `agent/`
(`omp config path`); named profiles live under `profiles/<name>/agent` and are
not tracked here.

Committing changes to `agent/config.yml`, `agent/AGENTS.md`, or `agent/mcp.json`
updates the running harness on its next reload — there is no copy or sync step.

## Installation

```powershell
git clone git@github.com:Metab0i/my-omp.git "$env:USERPROFILE\.omp"
```

OMP recreates ignored state (databases, caches, logs, sessions) on first launch;
credentials must be re-established with `/login`. Installed plugins reproduce
from the tracked manifests with `omp plugin` / `bun install` in `plugins/`.

Paths in these files are absolute (`shellPath`, MCP tool roots); adjust them for
a different host.

## Layout

| Path | Contents | Tracked |
| --- | --- | --- |
| `agent/config.yml` | Global settings: model roles, theme, approvals, tools | yes |
| `agent/AGENTS.md` | User-level instructions for every session | yes |
| `agent/mcp.json` | MCP server registrations | yes |
| `agent/skills/`, `agent/extensions/` | Authored skills and extensions | yes |
| `agent/skills.lock.json` | Skillshare package pins | yes |
| `plugins/{package.json,bun.lock,*.lock.json,installed_plugins.json}` | Plugin dependency and install state | yes |
| `marketplaces.json` | Added marketplace catalogs | yes |
| `agent/agent.db` | Auth credentials, usage history | no — secrets |
| `agent/models.db`, `history.db`, `skill-descriptions.db` | Catalogs and caches | no |
| `agent/sessions/`, `terminal-sessions/`, `predict/` | Transcripts and session state | no |
| `agent/managed-skills/` | Auto-learn output derived from past sessions | no |
| `cache/`, `logs/`, `natives/`, `run/`, `update/`, `install-id` | Caches, logs, binaries, runtime state | no |
| `plugins/node_modules/`, `plugins/cache/` | Installed code, derivable | no |
| `profiles/` | Per-profile agent directories | no |
