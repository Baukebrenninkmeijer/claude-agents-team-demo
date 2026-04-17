# Claude Code Multi-Agent Demos

Demos showcasing multi-agent collaboration with [Claude Code](https://claude.ai/code) — from local team coordination to cross-network agent communication via [Viche](https://github.com/viche-ai/viche).

This repo is meant to be **cloned and run** — each demo is self-contained and launches from a single prompt file. If you're new here, start with [TaskFlow](#1-full-stack-taskflow--parallel-task-execution) (local, no extra infra) and then explore the others.

![Architecture Overview](architecture-diagram.png)

## What you'll learn

- **How Claude Code spawns agent teams** and routes work between them
- **Task dependencies and parallel execution** — how agents block/unblock each other
- **Inter-agent messaging** via `SendMessage` (agents talk to each other, not just to you)
- **Cross-instance agent networks** via [Viche](https://github.com/viche-ai/viche) — discovery and routing across machines

## TL;DR — fastest path to a running demo

```bash
git clone <this-repo> && cd team-demo
# Open Claude Code in the repo root, then paste the contents of:
cat demos/fullstack-taskflow/team-prompt.txt
```

That's it — agents spawn, build the app, and write tests. See [How to Run](#how-to-run) for the other demos.

## Repository Map

Where to find what:

```
team-demo/
├── README.md                          # This file — overview and how to run each demo
├── architecture-diagram.png           # Rendered architecture diagram (referenced above)
├── architecture-diagram.excalidraw    # Editable source for the diagram
├── linkedin-post.md                   # Draft LinkedIn post about these demos
│
├── demos/
│   ├── fullstack-taskflow/            # Demo 1: parallel multi-agent app build
│   │   ├── SPEC.md                    #   App spec, API design, data model
│   │   └── team-prompt.txt            #   Paste into Claude Code to launch the team
│   │
│   └── dnd-adventure/                 # Demo 2: inter-agent messaging via SendMessage
│       └── team-prompt.txt            #   Self-contained: character sheets + encounter
│
└── viche/                             # Demo 3: cross-instance agent discovery
    ├── agent1/.mcp.json               #   MCP config for the first Claude Code instance
    └── agent2/.mcp.json               #   MCP config for the second Claude Code instance
```

Quick pointers:
- **Want to run a demo?** See [How to Run](#how-to-run) below.
- **Want to understand the architecture?** Open `architecture-diagram.png` or the `.excalidraw` source.
- **Want to see what each team does?** Read the `team-prompt.txt` in that demo — it contains the full brief given to the agents.
- **Want the TaskFlow API contract?** `demos/fullstack-taskflow/SPEC.md`.

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

- [Claude Code](https://claude.ai/code) CLI — required for every demo
- [Bun](https://bun.sh) — only for the Viche channel server
- A Viche registry (self-hosted or public) — only for the network demo

The TaskFlow and D&D demos need nothing beyond Claude Code itself.

## FAQ

**Do I need API keys?** Only whatever Claude Code already uses. No extra keys for TaskFlow or D&D. The Viche demo needs access to a Viche registry.

**Can I modify the demos?** Yes — edit the `team-prompt.txt` for a demo to change the brief, roster, or task graph. The prompt is the whole contract.

**Where do the agents' outputs go?** TaskFlow writes code into a working directory Claude Code picks (usually a subfolder). D&D prints narration and dialogue in the conversation. Viche exchanges messages via MCP tools.

**I want to add a new demo.** Create `demos/<your-demo>/team-prompt.txt` with the full brief, add a section to this README, and (optionally) a `SPEC.md` if the demo has a non-trivial contract.

## License / Contributing

No formal license yet — open an issue if you want to reuse or contribute.
