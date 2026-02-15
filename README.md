# [No One Left Behind](https://kyramovva15.itch.io/no-one-left-behind)

**1st Place - 2025 AHS Game Jam**

A 2D platformer built in Godot 4.3 where you race against time to rescue survivors from a virus-infected building. Gain abilities from the people you save, break through obstacles, and get everyone to the helipad before the virus takes hold.

## Gameplay

You explore a crumbling building filled with an airborne virus. There are 4 survivors and a doctor trapped inside. Each rescue unlocks new abilities needed to reach the next survivor. Get everyone to the helipad in time to win.

### Abilities

- **Axe** - Obtained from Axe Man. Break through debris blocking trapped survivors.
- **Double Jump** - Obtained from Double Jump Man. Press jump mid-air for a second boost (reduced velocity).
- **Dash** - Obtained from Hover Man. Press SHIFT to dash horizontally. Has a cooldown meter.

### Win/Loss Conditions

- **Win**: Rescue all 4 survivors and reach the helipad before time runs out.
- **Lose**: Fall into the death pit, run out of time, or fail to rescue all survivors.

## Controls

| Action | Key |
|--------|-----|
| Move | Arrow Keys / A, D |
| Jump | Space / W / Up Arrow |
| Interact | E |
| Dash | Left Shift |

## Project Structure

```
├── main.gd / main.tscn         # Game controller, state management, NPC signals
├── player.gd / player.tscn     # Player movement, abilities, animation states
├── level.gd / level.tscn       # Platforms, collision shapes, death pit
├── npc.gd / npc.tscn           # NPC template with dialogue trigger areas
├── debris.gd / debris.tscn     # Destructible obstacles (axe required)
├── dialogue_box.gd / .tscn     # Typewriter dialogue system, ability signals
├── timer_label.gd              # Virus countdown timer HUD
├── title.tscn                  # Title screen
├── game_over.tscn              # Win/loss screen
├── script.json                 # All character dialogue
├── art/                        # Sprites, backgrounds, tilesets
└── project.godot               # Godot engine config
```

### Key Scripts

**main.gd** - Tracks game state: which NPCs have been spoken to, how many people remain, and whether the player has fallen. Connects signals from debris, NPCs, and the dialogue system to progress the game.

**player.gd** - Character controller with gravity, coyote jump (6 frames), double jump with diminishing velocity (`0.7^jump_count`), and a dash system (1000 speed, 0.2s duration, 0.5s cooldown). Ability flags (`axe_gotten`, `double_jump_got`, `hover_got`) gate mechanics.

**dialogue_box.gd** - Reads `script.json`, displays lines with a typewriter effect (1.5s visible ratio tween), and emits signals (`got_axe`, `got_double_jump`, `got_hover`, `rescued`) when conversations end.

**debris.gd** - Detects player in range + axe equipped, destroys after 1s delay, emits `broke` signal with debris number to unlock the next area.

## Requirements

- [Godot 4.3+](https://godotengine.org/download)

## Running

1. Clone the repository.
2. Open the project folder in Godot Engine 4.3+.
3. Press F5 or click Play.
