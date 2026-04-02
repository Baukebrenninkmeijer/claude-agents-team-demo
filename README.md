# Claude Agents Team Demo

Demo repository showcasing Claude Code's **team agents** feature — multiple AI agents working in parallel, coordinating through shared task lists and direct messaging.

## Demos

### 1. [Full-Stack TaskFlow](demos/fullstack-taskflow/)
**Focus: Parallel task execution with dependencies**

3 agents build a complete task manager app simultaneously:
- `backend-dev` — FastAPI + SQLAlchemy + SQLite
- `frontend-dev` — React + Vite + Tailwind
- `test-writer` — pytest tests + README (waits for others)

Shows: task dependencies, parallel builds, blocked/unblocked workflow.

### 2. [D&D Adventure](demos/dnd-adventure/)
**Focus: Inter-agent communication**

4 agents play a short D&D encounter:
- `dm` — Dungeon Master narrating and managing combat
- `thorin` — Dwarf Fighter (tank)
- `elara` — Elf Wizard (spellcaster)
- `shadow` — Halfling Rogue (scout)

Shows: agents messaging each other, coordinating strategy, sharing knowledge, reacting to each other's actions in real-time.

## How to Run

Each demo folder contains:
- `SPEC.md` — the full scenario specification
- `team-prompt.txt` — the exact prompt to kick off the team

To run a demo, start a Claude Code session in this repo and paste the instructions from `team-prompt.txt`.
