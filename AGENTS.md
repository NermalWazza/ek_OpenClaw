# AGENTS.md

## What this repo is

Documentation for the OpenClaw AI-agent runtime on a Linux VM substrate. Defines the runtime layer above Substrate_Compute. Human-in-the-loop only — no autonomous or unattended agents.

## Architecture position

```
[ Global_Substrate_Settings ] → [ Substrate_Compute ] → [ ek_OpenClaw ]
        (governance)                 (infra)                 (runtime)
```

## Design principles

- Human-initiated execution only — no cron jobs, triggers, or unattended execution
- Explicit cost boundaries (API-metered, revocable, bounded by provider spend limits)
- Minimal persistent state
- Easy teardown and redeploy

## Key runtime components (documented in README.md)

| Component | Detail |
|-----------|--------|
| Python runtime | `venv` only — no system-wide packages |
| Session management | TMUX for persistent SSH sessions |
| API connectivity | External LLMs only (OpenAI, Anthropic) via environment variables |
| OpenClaw mode | Embedded (local), no daemon, no auto-execution |

## Confirmed commands

None in this repo — runtime commands are on the VM and documented in `README.md`.

## Guardrails

- Do not add autonomous agent code, daemons, or background processes.
- Credentials via environment variables only — never hardcoded.
- All new capabilities must be: explicitly justified, cost-bounded, auditable, easy to remove.

## Branch model

`nwlocal` → `main`.
