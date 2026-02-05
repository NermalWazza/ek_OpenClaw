# QuickStart.md
## OpenClaw VM Startup – Shell & Listener (Tech Runbook)

---

## 1. Scope
This quickstart covers:
- Accessing the VM
- Verifying baseline health
- Starting the OpenClaw **shell** (interactive)
- Starting the OpenClaw **listener / agent**
- Verifying correct operation

Audience: Ops / Systems / DevOps engineers.

---

## 2. Preconditions
- Linux VM (Ubuntu/Debian assumed)
- SSH or console access
- `sudo` privileges
- OpenClaw installed
- Python virtual environment present
- API keys available (OpenAI / Anthropic)
- Outbound HTTPS (443) allowed

---

## 3. VM Access & Baseline Checks

### 3.1 SSH into VM
```bash
ssh user@<vm_ip_or_hostname>
