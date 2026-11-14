# Platformer Maker

A tile-based 2D platformer editor that runs in a single HTML file. Build a level, set up your character and power-ups, then press **Play** to try it instantly.

> The same guide is available inside the editor: click **❓ Help** in the toolbar or press **H** (or **F1**).

---

## Contents

1. [Getting started](#getting-started)
2. [Screen layout](#screen-layout)
3. [Toolbar](#toolbar)
4. [Tile palette](#tile-palette)
5. [Moving platforms](#moving-platforms)
6. [Character settings](#character-settings)
7. [Power-ups](#power-ups)
8. [Game system (score & lives)](#game-system-score--lives)
9. [Screen & level size](#screen--level-size)
10. [Cheats](#cheats)
11. [Controls](#controls)
12. [Gameplay rules](#gameplay-rules)
13. [Saving, loading & file format](#saving-loading--file-format)
14. [Tips](#tips)

---

## Getting started

1. Open `index.html` in a modern browser (Chrome, Firefox, Edge, Safari). No install or server needed.
2. A small example level loads the first time.
3. Pick a tile from the palette at the bottom, paint with the **left mouse button**, erase with the **right mouse button**.
4. Make sure the level has a **Start** tile (and ideally a **Goal**), then press **▶ Play** or **Enter**.
5. Press **Enter** or **Esc** to go back to the editor.

---

## Screen layout

| Area | Where | What it does |
|---|---|---|
| **Toolbar** | Top | Play/Stop, file actions, settings panels and menus. The status text on the right shows messages, and score/HP/lives while playing. |
| **Canvas** | Middle | The level. A grid is shown in edit mode. |
| **Palette** | Bottom | Tile categories. Click a category to select its last-used tile; categories with a **▲** open a list of all their tiles. |
| **Hint bar** | Bottom-left of the canvas | Short reminder of the keys for the current mode. |
| **Side panels** | Left / right | Character, Power-ups and Moving-platform settings. |

---

## Toolbar

| Button | Shortcut | Description |
|---|---|---|
| **▶ Play / ■ Stop** | `Enter` | Switch between editing and playing. Play needs a Start tile. |
| **↶ Undo** | `Ctrl+Z` | Undo the last paint stroke, clear, resize, load or import (up to 100 steps). |
| **Clear** | — | Empty the whole level (asks for confirmation; can be undone). |
| **Save** | — | Save the level to the browser (localStorage). |
| **Load** | — | Load the level saved in the browser. |
| **Export** | — | Download the level as `level.json`. |
| **Import** | — | Open a `.json` level file. |
| **🏃 Character** | `C` | Open the Character panel (jump, speed, shots, health). |
| **⭐ Power-ups** | `U` | Open the Power-ups editor. |
| **⚙ Game system** | — | Points per coin/enemy and coins needed for an extra life. |
| **🖥 Screen** | — | Screen resolution and level size. |
| **🎮 Cheats** | `I` | Toggle invincibility. |
| **❓ Help** | `H` / `F1` | Open this guide in the game. |

Only one dropdown menu is open at a time; click outside or press `Esc` to close it.

---

## Tile palette

Select a tile with its key or from the palette. **Middle-click** a tile in the level to pick it up as the current tool.

### Terrain

| Tile | Key | Behaviour |
|---|---|---|
| **Ground** | `1` | Solid block with a grass top. |
| **Brick** | `2` | Solid block (looks different from Ground, behaves the same). |
| **Breakable** | `B` | Solid block that shatters when the player hits it **from below**. Comes back on each new life. |
| **Platform** | `3` | One-way platform: jump up through it, land on top. |
| **Falling** | `F` | One-way platform that shakes for 0.5 s after you land on it, then falls. Comes back on each new life. |
| **Moving** | `M` | One-way platform that moves along a path. See [Moving platforms](#moving-platforms). |

### Hazards

| Tile | Key | Behaviour |
|---|---|---|
| **Spikes** | `4` | Touching them costs 1 HP. |

### Enemies

| Tile | Key | Behaviour |
|---|---|---|
| **Enemy** | `5` | Walks left and right, turning at walls and ledges. Touching it costs 1 HP. Jump on it (stomp) or shoot it to defeat it. |

### Items

| Tile | Key | Behaviour |
|---|---|---|
| **Coin** | `6` | Gives points; enough coins give an extra life (see [Game system](#game-system-score--lives)). |

### Power-ups

Every power-up you create in the Power-ups panel appears here. The last entry, **✎ Create / edit…** (`U`), opens the editor.

### Gadgets

| Tile | Key | Behaviour |
|---|---|---|
| **Spring** | `7` | Bounces the player very high (about 2.7× a normal jump). One-way from above. |

### Level

| Tile | Key | Behaviour |
|---|---|---|
| **Start** | `8` | Where the player appears. Only one per level: placing a new one removes the old one. Required to play. |
| **Goal** | `9` | Flag. Touching it completes the level. |

### Edit

| Tile | Key | Behaviour |
|---|---|---|
| **Eraser** | `0` | Removes tiles (same as right-click). |

---

## Moving platforms

When the **Moving** tool is selected, the **Moving platform** panel opens on the left. Its settings apply to the next tiles you paint.

| Setting | Options | Description |
|---|---|---|
| **Path** | ↔ Horizontal · ↕ Vertical · ⤢ Diagonal · ⟳ Circle | Shape of the movement. |
| **Direction** | Depends on the path (→ ←, ↑ ↓, ↗ ↘ ↙ ↖, ↻ ↺) | Which way it starts moving. |
| **Distance** / **Radius** | 1 – 20 tiles | Length of the trip (or circle radius). |
| **Speed** | 0.5 – 15 tiles/s | How fast it moves. |

- The tile you place is the **start point (A)**. Straight paths go back and forth between A and B. Circles start at the top, with the centre `Radius` tiles below.
- A dashed line and a faded copy show the path in the editor.
- **Paint over** an existing moving platform to give it the current settings.
- **Middle-click** a moving platform to copy its settings into the panel.
- Neighbouring tiles with the same settings move together, so you can build wider platforms.
- The player rides the platform; walls still block the player while riding.

---

## Character settings

Open with **🏃 Character** or `C`. Changes apply immediately, even while playing. When the panel is open, dashed **jump arcs** are drawn from the Start tile so you can check what the player can reach.

| Setting | Range | Default | Description |
|---|---|---|---|
| **Jump height** | 0.5 – 20 tiles | 3.4 | Peak height of a full jump at top speed. |
| **Jump width** | 1 – 30 tiles | 4.8 | Horizontal distance of a full jump at top speed (take-off to landing at the same height). |
| **Speed** | 1 – 30 tiles/s | 7.2 | Top running speed. |
| **Speed impact on jump** | 0 – 100 % | 0 | How much a jump shrinks when not running. 0 % = same jump at any speed; 100 % = a standing jump is tiny. When above 0, an orange arc shows the standing jump. |
| **Projectile speed** | 2 – 60 tiles/s | 14 | How fast shots fly. |
| **Projectiles on screen** | 0 – 10 | 3 | Max shots at once. **0 disables shooting.** |
| **Health points** | 1 – 10 HP | 3 | Hits the player can take before losing a life. |
| **Lives** | 1 – 99 | 3 | Lives at the start of a run. |

**Reset defaults** restores the values above. The panel's info line shows air time, standing-jump size, shooting and health summary.

---

## Power-ups

Open with **⭐ Power-ups** or `U`. Power-ups are made by you and saved with the level. The first time the editor runs you get five examples:

| Preset | Effect |
|---|---|
| **Giant** | Size 160 %, speed 90 % |
| **Tiny** | Size 55 %, jump height 120 %, speed 115 % |
| **Wings** | Double jump |
| **Feather** | Glide |
| **Fire** | Throws bouncing projectiles |

### Managing power-ups

- Click a power-up in the list to edit it **and** select it for painting.
- **＋ New** creates one (up to 25). **Duplicate** copies the selected one. **🗑 Delete** removes it and every copy placed in the level.
- **Name** (max 16 characters): its first letter is drawn on the pick-up orb.
- **Colour**: used for the orb, the player's headband and its effects.

### Settings

| Setting | Range | Description |
|---|---|---|
| **Duration** | 0 – 120 s | How long it lasts. **0 = until you lose a life.** The headband blinks during the last 2 seconds. |
| **Character size** | 30 – 300 % | Player size. Growing waits until there is enough room. |
| **Jump height** | 25 – 300 % | Multiplies the character's jump height. |
| **Jump width** | 25 – 300 % | Multiplies the character's jump width. |
| **Speed** | 25 – 300 % | Multiplies the character's speed. |

### Abilities (tick to enable)

| Ability | Settings | Description |
|---|---|---|
| **🪽 Double jump** | Extra jumps in the air: 1 – 5 | Press jump again in mid-air. Refills on landing. |
| **🪂 Glide** | Glide fall speed: 0.5 – 8 tiles/s | Hold jump while falling to float down slowly. |
| **🔥 Projectile throwing** | Projectiles on screen: 1 – 10 · Throw speed: 2 – 40 tiles/s · Bounce height: 0 – 4 tiles (0 = fly straight) | Throw with `X` / `J`. Replaces the character's normal shots while active. |

### Rules

- Picking up a power-up **replaces** the current one.
- Power-ups are **lost when you lose a life**; pick-ups come back with the level.
- Editing a power-up while playing updates it live.

---

## Game system (score & lives)

Open the **⚙ Game system** menu.

| Setting | Range | Default | Description |
|---|---|---|---|
| **Points per coin** | 0 – 10000 | 100 | Score for each coin. |
| **Points per enemy** | 0 – 10000 | 200 | Score for each enemy defeated (stomp, shot or invincible contact). |
| **Coins for a life** | 0 – 999 | 100 | Collecting this many coins gives +1 life ("1UP"). 0 = never. |

Health points and starting lives are set in the [Character panel](#character-settings).

---

## Screen & level size

Open the **🖥 Screen** menu.

**Screen size** — the resolution the game is drawn at:

- **Fit window** (default): fills the available space.
- Fixed sizes: 640×360, 960×540, 1280×720, 1920×1080 (16:9) · 640×480, 800×600, 1024×768 (4:3) · 576×576 (1:1) · 1280×540 (21:9). Fixed sizes are letterboxed and scaled down if the window is too small.

At most 18 rows are visible at once; taller levels scroll vertically.

**Level size (tiles)**:

| Setting | Range | Default | Step buttons | Notes |
|---|---|---|---|---|
| **Width** | 20 – 1000 | 120 | ± 10 | Adds/removes columns **on the right**. |
| **Height** | 8 – 200 | 18 | ± 1 | Adds/removes rows **at the top** (the ground stays in place). |

You can also type a value. Resizing only works in edit mode and can be undone.

---

## Cheats

Open the **🎮 Cheats** menu or press `I` (works in both modes).

- **🛡 Invincibility** — spikes and enemies can't hurt you (touching an enemy defeats it), and falling into a pit puts you back on the last solid ground you stood on. A golden outline shows it is on, and the Cheats button stays highlighted.

---

## Controls

### Editor

| Action | Input |
|---|---|
| Paint | Left click / drag |
| Erase | Right click / drag |
| Pick tile (and moving-platform settings) | Middle click |
| Select tile | `1`–`9`, `0`, `B`, `F`, `M` |
| Scroll horizontally | `←` `→` / `A` `D` (`Q` on AZERTY) or mouse wheel |
| Scroll vertically | `↑` `↓` / `W` `S` (`Z` on AZERTY) or `Shift` + wheel |
| Undo | `Ctrl+Z` |
| Character panel | `C` |
| Power-ups panel | `U` |
| Invincibility | `I` |
| Help | `H` / `F1` |
| Play | `Enter` |
| Close menu / palette list / help | `Esc` |

### Play

| Action | Input |
|---|---|
| Move | `←` `→` / `A` `D` (`Q` on AZERTY) |
| Jump (hold for higher) | `Space` / `W` / `↑` / `Z` |
| Shoot / throw | `X` / `J` |
| Restart the run | `R` |
| Invincibility | `I` |
| Help (pauses the game) | `H` / `F1` |
| Back to the editor | `Enter` / `Esc` |

---

## Gameplay rules

- **A run** starts when you press Play and ends at game over. Score and lives carry over between lives; each life restarts the level from the Start tile with full HP.
- **Getting hit** (spikes, enemies) costs 1 HP, knocks you back and makes you invulnerable (blinking) for 1.2 s. At 0 HP you lose a life.
- **Pits**: falling out of the bottom of the level always costs a whole life, whatever your HP.
- **Stomping**: landing on an enemy defeats it and bounces you up. Hold jump while stomping for a full-height bounce.
- **Shots** fly straight, stop at solid tiles, defeat enemies and disappear off screen.
- **Jump feel**: releasing jump early cuts the jump short. A short grace period lets you jump just after walking off a ledge or just before landing.
- **Level edges** act as walls on the left and right.
- **Goal**: touching the flag completes the level. Press `R` to play again or `Enter` to edit.
- **Game over** when the last life is lost. Press `R` to try again.
- **HUD** (top-left): hearts for HP, then score, coins collected / total, and lives.

---

## Saving, loading & file format

**What the browser remembers automatically**: character settings, game-system settings, power-ups, moving-platform settings, screen size and cheats.

**The level itself** is only stored when you click **Save** (browser) or **Export** (file). On start-up, the level saved in the browser is loaded.

Saved and exported levels include the tiles, character settings, game-system settings, moving-platform settings and power-ups, so a level file is self-contained. Loading or importing a level replaces your current character, game-system and power-up settings with the level's.

### `level.json`

```json
{
  "w": 120,
  "h": 18,
  "rows": ["....", "..."],
  "char": { "jumpH": 3.4, "jumpW": 4.8, "speed": 7.2, "impact": 0, "projSpeed": 14, "projMax": 3, "hp": 3, "lives": 3 },
  "sys": { "coinPoints": 100, "enemyPoints": 200, "coinsPerLife": 100 },
  "meta": { "12,9": { "mode": "h", "dir": "r", "dist": 4, "speed": 2 } },
  "powerups": [ { "id": "A", "name": "Giant", "color": "#e94560", "size": 160, "speed": 90 } ]
}
```

Each string in `rows` is one row of the level, top to bottom, one character per tile:

| Char | Tile | Char | Tile |
|---|---|---|---|
| `.` | Empty | `s` | Spikes |
| `g` | Ground | `e` | Enemy |
| `b` | Brick | `c` | Coin |
| `k` | Breakable | `j` | Spring |
| `p` | Platform | `P` | Start |
| `v` | Falling | `f` | Goal |
| `m` | Moving | `A`–`Z` (not `P`) | Power-up with that `id` |

`meta` keys are `"x,y"` tile coordinates of moving platforms. `mode` is `h`, `v`, `d` or `c`; `dir` is `r`, `l`, `u`, `d`, `ur`, `dr`, `dl`, `ul`, `cw` or `ccw`.

---

## Tips

- Keep the **Character panel** open while designing gaps: the jump arcs from the Start tile show exactly what is reachable.
- Combine **Breakable** blocks with coins or power-ups above them for hidden rewards.
- A row of **Falling** platforms over a pit makes a quick "keep running" section.
- Use **Invincibility** to test the layout of long levels quickly, then turn it off to test difficulty.
- **Export** often: browser storage can be cleared.
