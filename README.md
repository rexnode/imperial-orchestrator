# Imperial Orchestrator for OpenClaw

A high-availability, role-based, multi-model routing skill pack for OpenClaw.

## What you get

- Court-style multi-role model orchestration
- Automatic model discovery from OpenClaw config
- Role-based routing by domain and complexity
- 401 auth circuit breaker
- Cross-provider fallback
- Degraded survival mode
- Machine-readable state snapshots

## Quick start

```bash
cd imperial-orchestrator-skill
python3 scripts/health_check.py --openclaw-config ~/.openclaw/openclaw.json --write-state ./.imperial_state.json
python3 scripts/router.py --task "Write a Go service for TRX address monitoring" --openclaw-config ~/.openclaw/openclaw.json --state-file ./.imperial_state.json
```

## Package layout

- `SKILL.md` — skill instructions and operating rules
- `config/` — role, routing, registry, and failure policy config
- `scripts/` — Python implementation
- `examples/` — install examples and sample patches
- `tests/` — smoke tests

## Recommended deployment pattern

1. Keep `router-chief` on the most stable provider or a local model.
2. Use specialist models for coding, ops, or legal tasks.
3. Add at least one **local** fallback model.
4. Run `health_check.py` before or during session bootstrap.
5. Persist state to `.imperial_state.json`.

## Example routing result

```json
{
  "mode": "plan_then_execute",
  "lead_role": "ministry-coding",
  "selected_model": "openrouter/deepseek-chat",
  "fallback_chain": [
    "ollama/qwen2.5-coder:14b",
    "openrouter/gpt-4.1-mini"
  ],
  "survival_model": "ollama/qwen2.5:7b"
}
```
