# ek_OpenClaw
Knowledge Share - OpenClaw build and integration.

# OpenClaw VM Substrate  
**Minimal, Governed AI-Agent Runtime (v0.x)**

## Overview

This repository defines a **minimal Linux VM substrate** for running **OpenClaw** as a **human-in-the-loop AI agent runtime**.  
The design prioritises **cost control, auditability, reversibility, and security** over autonomy or scale.

This is **not** an autonomous agent platform.  
It is a **controlled execution environment** for experimenting with AI-assisted workflows under explicit governance.

[ Global_Substrate_Settings ]  →  [ Substrate_Compute ]  →  [ ek_OpenClaw ]
        (governance)                 (infra)                 (runtime)

---

## Design Principles

- Human-initiated execution only  
- No unattended or background agents  
- Explicit cost boundaries (API-metered)  
- Minimal persistent state  
- Low attack surface  
- Easy teardown and redeploy  

“Under-automated” is a feature at this stage.

---

## Toolset Summary (Current Build)

### Compute / VM
- **Platform:** Cloud VM (Azure-backed in current build; cloud-agnostic pattern)
- **Size:** Small footprint (≈ 1–2 vCPU, ~8 GiB RAM, modest disk)
- **GPU:** None
- **Role:** Single-purpose agent substrate (not a desktop or general server)

---

### Operating System
- **OS:** Linux (Ubuntu-class)
- **Desktop:** None (headless)
- **Services:** Minimal (cloud agent only)
- **Networking:** Private access (SSH); no public services exposed

---

### Memory & Swap Configuration
- RAM validated post-provisioning (`free -h`)
- Disk validated (`df -h`)
- Swap enabled (~2 GiB) to:
  - avoid OOM kills
  - stabilise low-memory agent runs
- No aggressive tuning; defaults preferred for predictability

> Goal: stability, not peak performance.

---

### Terminal & Session Management
- **TMUX installed**
  - Persistent sessions across SSH disconnects
  - Clean separation of:
    - OS management
    - OpenClaw execution
    - diagnostics / logs

TMUX is treated as required tooling, not optional convenience.

---

### Python Runtime
- **Python 3 installed via OS packages**
- **Virtual environments (`venv`) used exclusively**
- No system-wide Python packages beyond essentials
- Clean separation between:
  - OS Python
  - project/runtime Python

---

### OpenClaw
- **OpenClaw installed locally**
- Executed in **embedded (local) mode**
- No long-running daemon
- No background agents
- No auto-execution

OpenClaw is invoked explicitly per session.

---

### External API Connectivity
- **External LLM APIs only** (e.g. OpenAI, Anthropic)
- **No Chat UI credential reuse**
- Credentials supplied via:
  - environment variables
  - local auth profiles
- API usage is:
  - metered
  - revocable
  - bounded by provider spend limits

There are **no implicit credentials** and no hidden call paths.

---

## Explicit Non-Goals (By Design)

This substrate intentionally excludes:

- Autonomous or self-directing agents  
- Multi-agent swarms  
- Cron jobs, triggers, or unattended execution  
- Write access to production systems or IaC  
- GUI desktops or public endpoints  
- Heavy observability stacks (ELK, Prometheus, etc.)  
- Unbounded “memory” or vector stores  
- Broad or unrestricted tool execution  

Each exclusion is an architectural decision, not an omission.

---

## Repository Intent

This repository exists to support:

- Reproducible VM builds
- Deterministic agent execution
- Clear governance boundaries
- Incremental capability layering

Future additions must be:
1. Explicitly justified  
2. Cost-bounded  
3. Auditable  
4. Easy to remove  

---

## Near-Term TODO

- **Add & test a dedicated Chat channel**
  - Interactive, short-lived sessions
  - No persistent memory by default
  - Basic logging and cost visibility
- Document:
  - session lifecycle
  - reset/teardown procedures
  - minimal redeploy steps

This will be the first packaged capability layered on top of the substrate.

---

## Status

- **Current state:** Foundations complete (v0.x)  
- **Posture:** Under-powered, under-automated, over-controlled  
- **Next milestone:** First reproducible chat capability with cost visibility

