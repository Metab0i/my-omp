# OMP agent configuration

```
%USERPROFILE%\.omp\agent      (omp config path)
```

Committing here changes the running harness on its next config reload — there is no copy or sync step between "version controlled" and "actually applied".

## Installation

```powershell
git clone git@github.com:Metab0i/my-omp.git "$env:USERPROFILE\.omp\agent"
```

Paths in these files are absolute (`shellPath`, MCP tool roots); adjust them for a different host.

## Profiles

Only the default profile is tracked here. `omp --profile <name>` uses `~/.omp/profiles/<name>/agent`, which has its own independent configuration.
