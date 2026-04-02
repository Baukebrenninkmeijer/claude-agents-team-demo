# D&D Adventure - Agent Communication Demo

## Overview

A short D&D encounter played out by a team of AI agents, showcasing real-time inter-agent communication. A Dungeon Master agent narrates the story and manages combat, while 3 player agents roleplay their characters, strategize with each other, and respond to the DM.

## Why This Demo

This demo highlights **agent-to-agent communication** — players discuss tactics, call out threats, request help, and coordinate actions by messaging each other directly. The DM broadcasts narrative and responds to player actions. It's visually compelling in tmux: 4 panes with agents actively chatting.

## The Adventure: "The Goblin Bridge"

A classic 3-round encounter:

1. **Round 1 - Discovery**: The party approaches a crumbling stone bridge over a ravine. Goblin archers are spotted on the far side. Players must discuss approach strategy.
2. **Round 2 - Combat**: Goblins attack. Players coordinate combat tactics (tank, flank, cast spells). A goblin shaman starts summoning something.
3. **Round 3 - Boss**: A troll emerges from under the bridge. Players must adapt their strategy — the rogue might know trolls are weak to fire, sharing this with the mage.

## Agents

### DM (Dungeon Master)
- Narrates the scene and environment
- Manages turn order and combat mechanics (simplified D20 rolls)
- Broadcasts narrative to all players after each round
- Responds to individual player actions
- Tracks HP for monsters and players
- Keeps the encounter moving (3 rounds max)

### Thorin (Dwarf Fighter)
- Personality: Brave, protective, charges in first
- Stats: HP 45, AC 18, Attack +7, Damage 1d10+4
- Tactics: Frontline tank, draws aggro, uses Shield Wall
- Communication style: Short, gruff, battle cries
- Will ask the rogue to flank, tell the mage to stay back

### Elara (Elf Wizard)
- Personality: Analytical, strategic, waits for the right moment
- Stats: HP 22, AC 12, Spell Attack +6, Spell Save DC 14
- Spells: Fire Bolt (1d10), Burning Hands (3d6 cone), Shield (reaction), Sleep
- Tactics: Stays at range, asks party to buy time for big spells
- Will ask about enemy weaknesses, coordinate AoE with party positioning

### Shadow (Halfling Rogue)
- Personality: Cocky, observant, always looking for an edge
- Stats: HP 30, AC 15, Attack +7, Damage 1d6+4 (+2d6 sneak attack)
- Abilities: Sneak Attack, Cunning Action (hide/dash/disengage), Perception +6
- Tactics: Scouts ahead, flanks with fighter, calls out threats
- Will share knowledge about monsters, suggest ambush points

## Communication Patterns to Showcase

These are the key moments the audience should see:

1. **Strategy discussion** (Round 1): All 3 players message each other to plan approach
   - Shadow: "I count 4 goblins, 2 archers on the bridge, 1 shaman in the back"
   - Thorin: "I'll charge the bridge head-on. Shadow, can you flank right?"
   - Elara: "If you group them on the bridge, I can hit them all with Burning Hands"

2. **Combat coordination** (Round 2): Players react to DM and coordinate
   - Thorin to Shadow: "I'm taking heavy fire, need you to take out that archer"
   - Shadow to Elara: "Shaman is casting something — can you counterspell?"
   - Elara to all: "Stay clear of the bridge entrance, casting Burning Hands next round"

3. **Knowledge sharing** (Round 3): Rogue shares intel, party adapts
   - Shadow to all: "That's a troll! They regenerate — need fire damage to stop it"
   - Elara: "I've got Fire Bolt and Burning Hands. Thorin, keep it busy"
   - Thorin: "On it. Shadow, grab a torch from the bridge wreckage"

## Game Mechanics (Simplified)

- D20 rolls: agents "roll" by picking a number 1-20 (DM can override for drama)
- Attack: roll + modifier vs AC
- Damage: roll damage dice on hit
- HP tracking: DM announces HP changes
- No initiative order — players go in any order, then DM resolves and narrates

## Encounter Stats

### Goblin Archer (x3)
HP 7, AC 13, Attack +4, Damage 1d6+2

### Goblin Shaman (x1)
HP 12, AC 11, Spell Attack +4, Spells: Hex, Summon (takes 2 rounds)

### Bridge Troll (Round 3)
HP 40, AC 14, Attack +6, Damage 2d6+3, Regenerate 5 HP/round (stopped by fire)

## Tone

Fun but focused. The goal is to show off communication, not to write a novel. Each agent message should be 1-3 sentences max. The whole encounter should take about 5 minutes of agent runtime.
