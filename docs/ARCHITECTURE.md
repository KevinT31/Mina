# Mina — Architecture

## 1. Design Principle

Mina is built around a local-first rule:

> Core usefulness should survive loss of internet access or optional services.

The architecture therefore favors modular components with explicit degradation paths.

## 2. Layers

### Mission Control

React/Vite/Three.js interface connected to the API through REST and WebSocket.

### Core API

Fastify service that coordinates orchestration, memory, tools, security and realtime state.

### Agent Orchestrator

Routes requests to specialized agents and consolidates results.

### Model Router

Selects local models first and can use authorized external providers when configured.

### Memory Service

Three-layer memory:

1. Markdown / Obsidian
2. PostgreSQL
3. Qdrant

### Tool Registry

Maintains explicit tools/adapters.

### Permission Engine

Applies risk levels, safe mode, emergency state and approval workflows before execution.

### Workers / Automation

BullMQ handles background jobs; n8n provides versioned automation workflows.

### Multimodal Services

Voice and vision are isolated Python/FastAPI services.

## 3. Request Flow

```text
Mission Control
    ↓ REST / WebSocket
Core API
    ↓
Agent Orchestrator
    ├─→ Model Router → Ollama / authorized cloud
    ├─→ Memory → Markdown + PostgreSQL + Qdrant
    ├─→ Tool Registry → Permission Engine → tools/workflows
    └─→ Voice / Vision / Workers
    ↓
Logs + audit + response + state updates
```

## 4. Resilience

Examples from the private architecture:

- no local model → explicit fallback/offline behavior
- no internet → local memory and models remain usable
- automation failure → logged without collapsing the core
- agent failure → orchestrator can stop/mark it failed
- dangerous action → approval required
- unavailable voice/vision model → service reports reduced capability

## 5. Security Model

The key distinction is between:

- **capability**: a tool exists
- **authorization**: the current execution is allowed

The Permission Engine sits between the Tool Registry and execution. This prevents an agent from treating tool discovery as blanket permission.

## 6. Data Ownership

Personal vault data, logs, backups and environment configuration stay outside the public showcase.

This document describes architecture only; it is intentionally not an operational setup guide.
