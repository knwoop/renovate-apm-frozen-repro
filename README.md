# Renovate apm manager: `apm install` runs frozen

Minimal reproduction for the `apm` manager.

`apm.yml` pins `microsoft/apm-sample-package#v1.0.0`, and `apm.lock.yaml` was generated with APM 0.39.0.
`v1.0.1` exists upstream.

## Current behavior

Renovate opens a PR that only bumps the ref in `apm.yml` and reports an artifact error.
Renovate runs `apm install` with `CI=true`, and APM 0.37.0+ then installs as `--frozen`:

```
[i] CI is set and apm.lock.yaml exists: installing as --frozen. Pass --no-frozen to resolve and update it.
[x] --frozen: apm.lock.yaml is out of sync with apm.yml.
```

## Expected behavior

The PR also updates `apm.lock.yaml` and the deployed files under `.claude/`.

## Steps

Run the `renovate` workflow (self-hosted Renovate with `LOG_LEVEL=debug`), or point Renovate at this repository.
