# Mina — Architecture Notes

## Core Components

### Mission Control
Visual interface for system status, memory, agents and actions.

### Core API
Central application boundary for requests and system coordination.

### Agent Orchestrator
Routes work to specialized agents and coordinates their outputs.

### Model Router
Selects local or authorized external models.

### Memory
Combines human-readable notes, structured relational data and semantic vector search.

### Tool Registry + Permission Engine
Separates tool discovery from authorization and execution.

## Logical Flow

```mermaid
flowchart TB
    User --> Mission[Mission Control]
    Mission --> Core[Core API]
    Core --> Agents[Agent Orchestrator]

    Agents --> Models[Model Router]
    Models --> Local[Ollama]

    Agents --> Memory[Memory Layer]
    Memory --> Notes[Markdown / Obsidian]
    Memory --> SQL[PostgreSQL]
    Memory --> Vector[Qdrant]

    Agents --> Tools[Tool Registry]
    Tools --> Permission[Permission Engine]
    Permission --> Workflows[n8n / MCP / Services]
```

## Design Considerations

- Local-first operation is preferred.
- Optional services degrade gracefully.
- Memory is persistent and auditable.
- Tool use is permission-gated.
- Personal data and private automation state remain outside this public repository.
