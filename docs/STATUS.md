# Mina — Project Status

## Core phases 0–13

The private roadmap records all 14 base phases as completed.

Implemented areas include:

- core API + Mission Control
- Markdown memory
- PostgreSQL + Qdrant + local RAG
- development-memory MCP server
- multi-agent orchestration
- n8n execution layer
- Tool Registry
- Permission Engine
- evidence/research workflows
- voice
- vision
- advanced Mission Control
- controlled autonomous mode
- mobile/Telegram integration
- industrial/professional intelligence

## Verification recorded by the private project

- typecheck clean across the core packages
- **99 tests**
- live API validation
- explicit local-first degradation tests

## Visual / interaction extension

Later phases add:

- source-risk/research import tooling
- memory graph / Cortex
- agent office / HQ
- gesture interaction
- 3D and geo interfaces
- CEO/news interfaces

These extend the core rather than replacing it.

## Environment-dependent validation

Some capabilities need optional external/local infrastructure to be exercised fully:

- real PostgreSQL/Qdrant runtime
- specific Ollama models
- n8n runtime
- local voice models
- OCR binaries
- external channels/accounts

## Showcase rule

The public repository documents the system without exposing personal memory, automation rules, local infrastructure or private integration state.
