# DECISIONS.md

## Decision — Human-initiated execution only

No autonomous agents, no background daemons, no cron jobs or unattended execution.
Rationale: "under-automated is a feature at this stage" — control, auditability, and reversibility over autonomy.

## Decision — Embedded (local) OpenClaw mode

No long-running daemon, no background agents, no auto-execution. Invoked explicitly per session.
Rationale: explicit per-session invocation preserves full human oversight and cost visibility.

## Decision — Credentials via environment variables only

API keys via env vars or local auth profiles. No implicit credentials, no hidden call paths.
Rationale: metered, revocable, bounded API usage; no credential leakage risk from hardcoding.

## Decision — TMUX for session management

Persistent sessions across SSH disconnects. Separate panes for OS management, OpenClaw execution, and diagnostics.
Rationale: required tooling for stable agent runs on a headless remote VM.
