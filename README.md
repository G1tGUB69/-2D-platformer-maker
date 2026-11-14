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
8. [Enemies](#enemies-1)
9. [Game system (score & lives)](#game-system-score--lives)
10. [Screen & level size](#screen--level-size)
11. [Cheats](#cheats)
12. [Controls](#controls)
13. [Gameplay rules](#gameplay-rules)
14. [Saving, loading & file format](#saving-loading--file-format)
15. [Tips](#tips)

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
| **❚❚ Pause / ▶ Resume** | `P` | Only shown while playing. Freezes the game until you resume. The game also pauses by itself when the window loses focus. |
| **↶ Undo** | `Ctrl+Z` | Undo the last paint stroke, clear, resize, load or import (up to 100 steps). |
| **Clear** | — | Empty the whole level (asks for confirmation; can be undone). |
| **Save** | — | Save the level to the browser (localStorage). |
| **Load** | — | Load the level saved in the browser. |
| **Export** | — | Download the level as `level.json`. |
| **Import** | — | Open a `.json` level file. |
| **🏃 Character** | `C` | Open the Character panel (jump, speed, shots, health). |
| **⭐ Power-ups** | `U` | Open the Power-ups editor. |
| **👾 Enemies** | `E` | Open the Enemies editor. |
| **⚙ Game system** | — | Points per coin and coins needed for an extra life. |
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

Every enemy type made in the [Enemies editor](#enemies-1) appears here. **✎ Create / edit…** (`E`) opens the editor; `5` selects the last enemy used.

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

## Enemies

Open with **👾 Enemies** or `E`. Enemy types are made by you and saved with the level, like power-ups. A starter set is created the first time:

| Preset | What it shows |
|---|---|
| **Walker** | The classic enemy: walks, turns at walls and ledges. |
| **Brute** | Size 1.5 tiles, 3 HP, 500 pts. |
| **Sentry** | Still, 2 HP. |
| **Spiky** | Can't be stomped: shoot it. |
| **Hoverer** | Flies back and forth horizontally (A ↔ B). |
| **Swooper** | Flies back and forth diagonally. |
| **Dart** | Flies left forever once on screen. |
| **Turret** | Still, shoots left and right. |
| **Bomber** | Flies A ↔ B and drops shots downwards. |

### Managing enemies

- Click an enemy in the list to edit it **and** select it for painting.
- **＋ New** creates one (up to 26). **Duplicate** copies the selected one. **🗑 Delete** removes it and every copy placed in the level.
- **Name** (16 characters max) and **Colour**.
- The enemy stands on the tile you paint it on, centred, whatever its size. A ↔ B paths and endless directions are previewed in the editor.
- Changes apply the next time the level starts (Play, a lost life or `R`).

### Settings

| Setting | Range | Default | Description |
|---|---|---|---|
| **Size** | 0.5 – 5 tiles | 0.75 | Width and height of the enemy. |
| **Health points** | 1 – 20 HP | 1 | Stomps or shots needed to defeat it (each one removes 1 HP). |
| **Score when defeated** | 0 – 10000 pts | 200 | Points gained when it is defeated. |
| **🥾 Can be stomped** | on / off | on | Off: landing on it hurts the player (it is drawn with spikes), so it must be shot. |
| **Speed** | 0.5 – 15 tiles/s | 2 | Walk, A ↔ B and Endless only. |
| **Distance A → B** | 1 – 30 tiles | 4 | A ↔ B only (per axis on diagonals). |

### Movement

| Mode | Direction | Behaviour |
|---|---|---|
| **■ Still** | Facing ← → | Doesn't move (floats where it is placed). |
| **🚶 Walk** | ← → | Walks with gravity, turning at walls and ledges. |
| **⇄ A ↔ B** | 8 directions | Flies back and forth between its tile (A) and B, horizontally, vertically or diagonally, through walls. |
| **➜ Endless** | 8 directions | Flies forever in one direction, through walls. Starts once it comes on screen; gone once it leaves the level. |

### 🔫 Fires projectiles (tick to enable)

| Setting | Range | Default | Description |
|---|---|---|---|
| **Direction** | → Facing · ↔ Both sides · ↑ Up · ↓ Down · ↕ Up & down | → Facing | Horizontal or vertical. *Facing* follows where the enemy looks/moves. |
| **Time between shots** | 0.3 – 10 s | 2 | Delay between two volleys. |
| **Projectile speed** | 1 – 30 tiles/s | 6 | How fast its projectiles fly. |

Enemies only fire while on screen. Their projectiles fly straight, stop at solid tiles and cost the player 1 HP. Cannons on the enemy show where it fires.

### Combat

- Each **stomp** or player **shot** removes 1 HP. A damaged enemy flashes and shows a health bar; at 0 HP it is defeated and gives its score.
- Right after a stomp the enemy can't hurt you for a moment, so bouncing off it is safe.

---

## Game system (score & lives)

Open the **⚙ Game system** menu.

| Setting | Range | Default | Description |
|---|---|---|---|
| **Points per coin** | 0 – 10000 | 100 | Score for each coin. |
| **Coins for a life** | 0 – 999 | 100 | Collecting this many coins gives +1 life ("1UP"). 0 = never. |

Points per enemy are set for each enemy type in the [Enemies editor](#enemies-1). Health points and starting lives are set in the [Character panel](#character-settings).

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
| Enemies panel | `E` |
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
| Pause / resume | `P` |
| Restart the run | `R` |
| Invincibility | `I` |
| Help (pauses the game) | `H` / `F1` |
| Back to the editor | `Enter` / `Esc` |

---

## Gameplay rules

- **A run** starts when you press Play and ends at game over. Score and lives carry over between lives; each life restarts the level from the Start tile with full HP.
- **Getting hit** (spikes, enemies, enemy projectiles) costs 1 HP, knocks you back and makes you invulnerable (blinking) for 1.2 s. At 0 HP you lose a life.
- **Pits**: falling out of the bottom of the level always costs a whole life, whatever your HP.
- **Stomping**: landing on an enemy removes 1 of its HP and bounces you up. Hold jump while stomping for a full-height bounce. Enemies that can't be stomped hurt you instead.
- **Shots** fly straight, stop at solid tiles, remove 1 HP from the enemy they hit and disappear off screen.
- **Jump feel**: releasing jump early cuts the jump short. A short grace period lets you jump just after walking off a ledge or just before landing.
- **Level edges** act as walls on the left and right.
- **Goal**: touching the flag completes the level. Press `R` to play again or `Enter` to edit.
- **Game over** when the last life is lost. Press `R` to try again.
- **HUD** (top-left): hearts for HP, then score, coins collected / total, and lives.

---

## Saving, loading & file format

**What the browser remembers automatically**: character settings, game-system settings, power-ups, enemies, moving-platform settings, screen size and cheats.

**The level itself** is only stored when you click **Save** (browser) or **Export** (file). On start-up, the level saved in the browser is loaded.

Saved and exported levels include the tiles, character settings, game-system settings, moving-platform settings, power-ups and enemies, so a level file is self-contained. Loading or importing a level replaces your current character, game-system, power-up and enemy settings with the level's. Older levels without enemy types still load: their `e` tiles become a Walker.

### `level.json`

```json
{
  "w": 120,
  "h": 18,
  "rows": ["....", "..."],
  "char": { "jumpH": 3.4, "jumpW": 4.8, "speed": 7.2, "impact": 0, "projSpeed": 14, "projMax": 3, "hp": 3, "lives": 3 },
  "sys": { "coinPoints": 100, "coinsPerLife": 100 },
  "meta": { "12,9": { "mode": "h", "dir": "r", "dist": 4, "speed": 2 } },
  "powerups": [ { "id": "A", "name": "Giant", "color": "#e94560", "size": 160, "speed": 90 } ],
  "enemies": [ { "id": "e", "name": "Walker", "color": "#c94f6d", "size": 0.75, "hp": 1, "points": 200, "stompable": true,
                 "mode": "walk", "dir": "l", "speed": 2, "dist": 4, "shoot": false, "shotDir": "face", "fireRate": 2, "shotSpeed": 6 } ]
}
```

Each string in `rows` is one row of the level, top to bottom, one character per tile:

| Char | Tile | Char | Tile |
|---|---|---|---|
| `.` | Empty | `s` | Spikes |
| `g` | Ground | `e`, `a`, `d`, … | Enemy type with that `id` (see below) |
| `b` | Brick | `c` | Coin |
| `k` | Breakable | `j` | Spring |
| `p` | Platform | `P` | Start |
| `v` | Falling | `f` | Goal |
| `m` | Moving | `A`–`Z` (not `P`) | Power-up with that `id` |

Enemy `id`s are taken from `eadhilnoqrtuwxyz0123456789`. Enemy `mode` is `still`, `walk`, `path` (A ↔ B) or `line` (endless); `shotDir` is `face`, `lr`, `up`, `down` or `ud`.

`meta` keys are `"x,y"` tile coordinates of moving platforms. `mode` is `h`, `v`, `d` or `c`; `dir` is `r`, `l`, `u`, `d`, `ur`, `dr`, `dl`, `ul`, `cw` or `ccw`.

---

## Tips

- Keep the **Character panel** open while designing gaps: the jump arcs from the Start tile show exactly what is reachable.
- Combine **Breakable** blocks with coins or power-ups above them for hidden rewards.
- A row of **Falling** platforms over a pit makes a quick "keep running" section.
- Use **Invincibility** to test the layout of long levels quickly, then turn it off to test difficulty.
- **Export** often: browser storage can be cleared.
