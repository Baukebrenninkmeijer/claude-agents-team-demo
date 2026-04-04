# Claude Code Multi-Agent Demos

Demos showcasing multi-agent collaboration with [Claude Code](https://claude.ai/code) — from local team coordination to cross-network agent communication via [Viche](https://github.com/viche-ai/viche).

![Architecture Overview](architecture-diagram.png)

## Demos

### 1. Full-Stack TaskFlow — Parallel Task Execution

**3 agents build a complete task manager app simultaneously.**

A backend dev, frontend dev, and test engineer work in parallel with task dependencies — the test writer waits for the backend, then writes tests and a README once everything is ready.

- **Stack**: FastAPI + SQLAlchemy | React + Vite + Tailwind | pytest
- **Shows**: Task dependencies, parallel builds, blocked/unblocked workflows

```
demos/fullstack-taskflow/
├── SPEC.md           # App specification and API design
└── team-prompt.txt   # Prompt to launch the team
```

### 2. D&D Adventure — Inter-Agent Communication

**4 agents play a 3-round D&D encounter, communicating in real-time.**

A Dungeon Master narrates the scene while three player agents (Thorin the Fighter, Elara the Wizard, Shadow the Rogue) coordinate tactics, share intel, and react to each other's decisions — all through Claude Code's `SendMessage` API.

- **Shows**: Real-time agent messaging, emergent coordination, in-character roleplay
- **Highlights**: Shadow warns the party about troll fire weakness, Thorin calls tactical formations, Elara times her spells based on party positioning

```
demos/dnd-adventure/
└── team-prompt.txt   # Self-contained prompt with all character sheets and encounter design
```

### 3. Viche Network — Cross-Instance Agent Discovery

**Two Claude Code instances discover and message each other over the internet.**

Uses [Viche](https://github.com/viche-ai/viche), an open-source agent networking protocol, to connect Claude Code instances running on different machines. Agents register with a shared registry, discover peers by capability, and exchange tasks.

- **Shows**: Agent discovery, capability-based routing, cross-network messaging
- **Protocol**: WebSocket-based MCP channel server connecting to a Viche registry

```
viche/
├── agent1/.mcp.json  # MCP config for first Claude Code instance
└── agent2/.mcp.json  # MCP config for second Claude Code instance
```

## How to Run

### Local Team Demos (TaskFlow, D&D)

1. Open Claude Code in this repo
2. Copy the contents of the demo's `team-prompt.txt`
3. Paste it into Claude Code — the agents will spawn automatically

### Viche Network Demo

1. Install [Viche channel server](https://github.com/viche-ai/viche) dependencies:
   ```bash
   cd <path-to-viche-channel> && bun install
   ```
2. Open two Claude Code instances, each in a different `viche/agent*/` directory
3. Both instances connect to the Viche registry via MCP and can discover + message each other:
   ```
   # From either agent, discover peers:
   viche_discover("*")

   # Send a task to another agent:
   viche_send("<agent-id>", "Review this PR for security issues")
   ```

## Architecture

The architecture diagram covers:

- Claude Code's team agent spawning model
- Task dependency resolution and parallel execution
- Viche network topology (registry, WebSocket channels, agent discovery)
- Message flow between agents across instances

## Requirements

- [Claude Code](https://claude.ai/code) CLI
- [Bun](https://bun.sh) (for Viche channel server)
- A Viche registry (self-hosted or public) for the network demo
