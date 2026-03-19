# Gemini CLI — Pawnpay Integration Guide

Gemini CLI can act as an AI assistant for the Pawnpay multi-store ecosystem.
When running inside the Docker/Podman stack, it has direct access to the
Pawnpay API and the n8n orchestration layer.

## Environment Variables

| Variable | Description |
|---|---|
| `GEMINI_API_KEY` | Google Gemini API key |
| `PAWNPAY_API_URL` | Pawnpay API base URL (e.g. `http://pawndex:8000/api/v1`) |
| `PAWNPAY_API_KEY` | Pawnpay API authentication key |
| `N8N_WEBHOOK_URL` | n8n webhook base URL (e.g. `http://n8n:5678/webhook`) |

## n8n Trigger Commands

Use Gemini CLI to trigger n8n workflows:

```bash
# Trigger all store syncs
gemini "Trigger a sync for all pawnpay stores via n8n"

# AI analysis report
gemini "Run an AI analysis on all pawnpay stores and return the report"

# Health check
gemini "Check the health of all pawnpay services"
```

## Built-in GEMINI.md Configuration

Add a `GEMINI.md` file in your working directory to give Gemini CLI
context about the Pawnpay stack:

```markdown
You are an AI assistant for the Pawnpay multi-store pawn shop management system.

Services available:
- Pawndex API: $PAWNPAY_API_URL
- n8n Orchestration: $N8N_WEBHOOK_URL
- Store codes: NORTH, SOUTH, EAST, WEST, CONWAY

When asked to sync stores, trigger the n8n webhook at:
  POST $N8N_WEBHOOK_URL/sync-trigger
  Body: { "store": "ALL" }

When asked for AI analysis, trigger:
  POST $N8N_WEBHOOK_URL/ai-analyze
  Body: { "store": "ALL" }
```

## Docker Usage

```bash
# Run Gemini CLI against the Pawnpay stack
docker run --rm -it \
  --network pawnpay_net \
  -e GEMINI_API_KEY=$GEMINI_API_KEY \
  -e PAWNPAY_API_URL=http://pawndex:8000/api/v1 \
  -e N8N_WEBHOOK_URL=http://n8n:5678/webhook \
  gemini-cli gemini "Analyze store performance for today"
```

## Podman Usage

```bash
podman run --rm -it \
  --network pawnpay_pawnpay_net \
  -e GEMINI_API_KEY=$GEMINI_API_KEY \
  -e PAWNPAY_API_URL=http://pawndex:8000/api/v1 \
  -e N8N_WEBHOOK_URL=http://n8n:5678/webhook \
  localhost/gemini-cli:latest gemini
```
