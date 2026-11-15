# OMP agent configuration

This repository **is** the live OMP agent directory on this workstation:

```
%USERPROFILE%\.omp\agent      (omp config path)
```

Committing here changes the running harness on its next config reload — there is no copy or sync step between "version controlled" and "actually applied".

## Tracked

| File | Purpose |
| --- | --- |
| `config.yml` | Global settings: model roles (incl. `advisor`), theme, approvals, provider/tool policy |
| `AGENTS.md` | User-level instructions loaded into every session |
| `mcp.json` | MCP server registrations |
| `README.md` | This file |
| `.gitignore` | Whitelist for the above |

## Ignored

Everything else in the directory is runtime state and stays out of git:

- `agent.db*` — auth credentials (API keys), usage history, settings journal
- `models.db*`, `skill-descriptions.db*`, `history.db*` — catalogs and caches
- `sessions/`, `terminal-sessions/`, `predict/` — transcripts and session state
- `cache/`, `blobs/` — caches and spilled tool output

`.gitignore` uses a whitelist (`*` plus explicit `!` entries), so a new state file can never be staged by accident. Never track `agent.db`: it contains secrets.

## Use on another machine

```powershell
git clone git@github.com:Metab0i/my-omp.git "$env:USERPROFILE\.omp\agent"
```

Or copy `config.yml`, `AGENTS.md`, and `mcp.json` into an existing `%USERPROFILE%\.omp\agent`. OMP recreates the ignored state (databases, caches, sessions) on first launch, so credentials must be re-established with `/login`.

Paths in these files are absolute (`shellPath`, MCP tool roots); adjust them for a different host.

## Profiles

Only the default profile is tracked here. `omp --profile <name>` uses `~/.omp/profiles/<name>/agent`, which has its own independent configuration.
