# Platformer Maker

A tile-based 2D platformer editor that runs in a single HTML file. Build a level, set up your character, enemies, power-ups, NPCs and merchants, then press **Play** to try it instantly.

> The same guide is available inside the editor: click **❓ Help** in the toolbar or press **H** (or **F1**).

---

## Contents

1. [Getting started](#getting-started)
2. [Screen layout](#screen-layout)
3. [Toolbar buttons](#toolbar-buttons)
4. [Editor layout](#editor-layout)
5. [Tile palette](#tile-palette)
6. [Hidden items in Breakable blocks](#hidden-items-in-breakable-blocks)
7. [Moving platforms](#moving-platforms)
8. [Springs](#springs)
9. [Bubble spawners](#bubble-spawners)
10. [Goal pole](#goal-pole)
11. [NPCs & text boxes](#npcs--text-boxes)
12. [Character settings](#character-settings)
13. [Power-ups](#power-ups)
14. [Enemies](#enemies-1)
15. [Game system (score & lives)](#game-system-score--lives)
16. [Screen & level size](#screen--level-size)
17. [Cheats](#cheats)
18. [Controls](#controls)
19. [Gameplay rules](#gameplay-rules)
20. [Saving, loading & file format](#saving-loading--file-format)
21. [Tips](#tips)

---

## Getting started

1. Open `index.html` in a modern browser (Chrome, Firefox, Edge, Safari). No install or server needed.
2. On the title screen, click **▶ Start** (or press `Enter`, `Space` or `Esc`).
3. A small example level loads the first time.
4. Pick a tile from the **Level elements** bar (at the bottom by default), paint with the **left mouse button**, erase with the **right mouse button**.
5. Make sure the level has a **Start** tile (and ideally a **Goal**), then press **▶ Play** or **Enter**.
6. Press **Enter** or **Esc** to go back to the editor.

---

## Screen layout

| Area | Default place | What it does |
|---|---|---|
| **Bars** | Top and bottom | Five toolbars (Play, Edit & files, Game design, Level elements, Layout & Help). Each can be docked on any edge of the screen, see [Editor layout](#editor-layout). The status text shows messages, and score/HP/lives while playing. |
| **Canvas** | Middle | The level. A grid is shown in edit mode. |
| **Hint bar** | Bottom-left of the canvas | Short reminder of the keys for the current mode. |
| **Side panels** | Left / right | Character, Power-ups and Enemies editors (right); settings for the selected tool (left): Moving platform, Spring, Flame jet, Bubbles, Goal, Text box, NPC or Merchant. Sections inside panels and menus can be collapsed; the editor remembers which are open. |

---

## Toolbar buttons

| Button | Bar | Shortcut | Description |
|---|---|---|---|
| **▶ Play / ■ Stop** | Play | `Enter` | Switch between editing and playing. Play needs a Start tile. |
| **❚❚ Pause / ▶ Resume** | Play | `P` | Only shown while playing. Freezes the game until you resume. The game also pauses by itself when the window loses focus. |
| **↶ Undo** | Edit & files | `Ctrl+Z` | Undo the last paint stroke, clear, resize, load or import (up to 100 steps). |
| **Clear** | Edit & files | — | Empty the whole level (asks for confirmation; can be undone). |
| **Save** / **Load** | Edit & files | — | Save the level to the browser (localStorage) / load it back. |
| **Export** / **Import** | Edit & files | — | Download the level as `level.json` / open a `.json` level file. |
| **🏃 Character** | Game design | `C` | Open the Character panel (jump, speed, shots, health, perks). |
| **⭐ Power-ups** | Game design | `U` | Open the Power-ups editor. |
| **👾 Enemies** | Game design | `E` | Open the Enemies editor. |
| **⚙ Game system** | Game design | — | Score, coins, lives and hazard settings. |
| **🖥 Screen** | Game design | — | Screen resolution and level size. |
| **🎮 Cheats** | Game design | `I` `T` `N` | Invincibility, endless time, no enemy AI. |
| **🧩 Layout** | Layout & Help | — | Dock each bar on any edge of the screen. |
| **❓ Help** | Layout & Help | `H` / `F1` | Open this guide in the game (pauses the game). |

The **Level elements** bar holds the tile categories (see [Tile palette](#tile-palette)). Only one dropdown menu is open at a time; click outside or press `Esc` to close it.

---

## Editor layout

Open the **🧩 Layout** menu to arrange the screen. The tools are split into five bars, and each one can be docked on any edge: ⬆ top, ⬇ bottom, ⬅ left or ➡ right.

| Bar | Default | Contains |
|---|---|---|
| **▶ Play / Pause** | Bottom | Test the level, pause it. |
| **↶ Edit & files** | Top | Undo, Clear, Save, Load, Export, Import. |
| **🏃 Game design** | Top | Character, Power-ups, Enemies, Game system, Screen, Cheats. |
| **🧱 Level elements** | Bottom | The tile categories (Terrain, Hazards…). |
| **🧩 Layout & Help** | Top | The Layout menu, the Help button and the status text. |

- **⇅ Flip sides** moves every bar to the opposite edge (top ↔ bottom, left ↔ right). **Reset** restores the defaults.
- Bars on the same edge sit side by side; on the left or right edge they stack vertically.
- Dropdown menus and element lists open toward the play area, so they are never cut off.
- The layout is saved in the browser.

---

## Tile palette

Select a tile with its key or from the **Level elements** bar: click a category to select its last-used tile; categories with a **▲** open a list of all their tiles. **Middle-click** a tile in the level to pick it up as the current tool (this also copies a moving platform's, spring's, flame jet's, bubble spawner's, goal's, text box's, NPC's or merchant's settings).

### Terrain

| Tile | Key | Behaviour |
|---|---|---|
| **Ground** | `1` | Solid block with a grass top. |
| **Brick** | `2` | Solid block (looks different from Ground, behaves the same). |
| **Breakable** | `B` | Solid block that shatters when the player hits it **from below**. Can hide a coin or power-up (see [Hidden items](#hidden-items-in-breakable-blocks)). Comes back on each new life. |
| **Platform** | `3` | One-way platform: jump up through it, land on top. |
| **Falling** | `F` | One-way platform that shakes for 0.5 s after you land on it, then falls. Comes back on each new life. |
| **Moving** | `M` | One-way platform that moves along a path. See [Moving platforms](#moving-platforms). |
| **Power brick** | `X` | Solid block: hit it **from below** to release a random power-up (from your Power-ups list) on top of it. Gives a coin if there are no power-ups. Works once, then it is spent. |
| **Coin brick** | `O` | Solid block: hit it **from below** to get a coin. Works once, then it is spent. |
| **Spin brick** | `Y` | Solid block that only shatters when the character touches it **while doing a rotating jump** (any side). You spin straight through it. |
| **Text box** | | Solid block holding a text (up to 200 characters). In play the text pops up in a bubble while you touch the block, and for 3 s after hitting it from below. See [NPCs & text boxes](#npcs--text-boxes). |

Spent and broken bricks come back on each new life. If there is no room above a Power brick, its power-up is given to you straight away.

### Hazards

| Tile | Key | Behaviour |
|---|---|---|
| **Spikes** | `4` | Touching them costs 1 HP. |
| **Flame jet** | | Solid burner you can stand on. On a cycle it shoots a flame straight up (stopped by solid tiles); touching the flame costs 1 HP. It flickers just before firing. Each burner has its own settings, see [Flame jets](#flame-jets). |
| **Lava** | | *Zone.* Touching it costs a whole life, like a pit (invincibility puts you back on the last solid ground). |
| **Water** | | *Zone.* You swim: 60 % speed, slow sinking, press jump at any time to swim up. With your head at the surface, jump leaps out. Air jumps refill in water; gliding and the rotating jump stop. |
| **Poison** | | *Zone.* Toxic gas you can move through, but it costs 1 HP every *Poison: seconds per HP* (**⚙ Game system › Hazards**, 0.2 – 10 s, default 1); the first hit comes after half that time. |

Zones fill whole tiles: paint several side by side to make a pool or a cloud; the top row gets a surface.

#### Flame jets

When the **Flame jet** tool is selected, the **Flame jet** panel opens on the left. Its settings apply to the next burners you paint; paint over a burner to apply them, middle-click one to copy its settings. Every burner's reach is outlined in the editor and its flame plays live.

| Setting | Range · default | Description |
|---|---|---|
| Flame height | 1 – 20 tiles · 3 | How high the flame reaches above the burner. |
| Burn time | 0.2 – 10 s · 1.5 | How long the flame stays lit. |
| Pause time | 0 – 10 s · 1.5 | Rest between two flames (0 = always lit). |
| Delay | 0 – 10 s · 0 | Shifts the burner's cycle, so a row of jets can fire one after another. |

### Enemies

Every enemy type made in the [Enemies editor](#enemies-1) appears here. **✎ Create / edit…** (`E`) opens the editor; `5` selects the last enemy used.

### Items

| Tile | Key | Behaviour |
|---|---|---|
| **Coin** | `6` | Worth 1 coin by default. Gives points; enough coins give an extra life (see [Game system](#game-system-score--lives)). |
| **Big coin** | | Worth 5 coins by default: counts that many towards the coin total, extra lives and score. |
| **Mega coin** | | Worth 10 coins by default, with the same effect. |

The value and size of each coin kind are set in **⚙ Game system › 🪙 Coins**. Bigger coins are also easier to grab.

### Power-ups

Every power-up you create in the Power-ups panel appears here. The last entry, **✎ Create / edit…** (`U`), opens the editor.

### Gadgets

| Tile | Key | Behaviour |
|---|---|---|
| **Spring** | `7` | Launches the player. Each spring has its own direction, trajectory and strength. See [Springs](#springs). |
| **Bubbles** | `G` | Solid block that keeps releasing soap bubbles. Touching a bubble pops it and bounces the character. See [Bubble spawners](#bubble-spawners). |

### NPCs

| Tile | Key | Behaviour |
|---|---|---|
| **NPC** | | Character you can talk to: stand next to it and press `↓` / `S`. Says 1 to 5 sentences, one per key press. |
| **Merchant** | | Sells power-ups, extra time, lives and health points for coins: stand next to it and press `↓` / `S`. |

See [NPCs & text boxes](#npcs--text-boxes).

### Level

| Tile | Key | Behaviour |
|---|---|---|
| **Start** | `8` | Where the player appears. Only one per level: placing a new one removes the old one. Required to play. |
| **Goal** | `9` | Goal pole: the tile is its base, the height is set per goal. Touching the pole completes the level; the higher you touch it, the more points. See [Goal pole](#goal-pole). |

### Edit

| Tile | Key | Behaviour |
|---|---|---|
| **Eraser** | `0` | Removes tiles (same as right-click). |

---

## Hidden items in Breakable blocks

Paint a coin (**Coin**, **Big coin** or **Mega coin**) or a **power-up** onto an existing **Breakable** block to hide it inside. The block shows a hint of its content in the editor.

- When the player breaks the block from below, a hidden **coin** is collected immediately at its full value (it counts towards the level's coin total), and a hidden **power-up** appears in the block's place.
- Painting Breakable over the block again keeps its content; erasing the block removes it.
- Hidden items come back with the block on each new life.

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

## Springs

When the **Spring** tool is selected, the **Spring** panel opens on the left. Its settings apply to the next springs you paint. While the tool is selected, the trajectory of every spring is drawn in the editor.

| Setting | Options / range | Default | Description |
|---|---|---|---|
| **Direction** | ↑ ↗ → ↘ ↓ ↙ ← ↖ (45° steps) | ↑ | Where the spring launches the player. `R` / `Shift+R` rotate it. |
| **Trajectory** | ⌒ Arc · ➝ Straight | Arc | Arc: launched with gravity, like a big jump. Straight: flies in a straight line without gravity. |
| **Height** *(arc)* | 1 – 40 tiles | 9 | Peak height of an upward bounce above the spring. |
| **Width** *(arc)* | 1 – 40 tiles | 8 | Horizontal distance from take-off to landing (same level) at top speed. |
| **Distance** *(straight)* | 1 – 40 tiles | 6 | How far the straight launch goes before gravity takes over. |
| **Speed** *(straight)* | 2 – 60 tiles/s | 20 | Speed of the straight launch. |

- An **upward arc** spring works like a one-way platform: land on it to bounce. It keeps your running speed, and releasing jump doesn't cut the bounce short.
- A **rotated** spring launches you as soon as you touch it, along its arrow, at the same speed as an upward bounce of that height.
- A **straight** launch gives no control for its duration, then you fall normally. It stops early if you hit a wall.
- **Paint over** a spring to apply the current settings; **middle-click** one to copy its settings.

---

## Bubble spawners

When the **Bubbles** tool is selected, the **Bubble spawner** panel opens on the left. Its settings apply to the next spawners you paint, and every spawner's bubble path is drawn in the editor.

| Setting | Options / range | Default | Description |
|---|---|---|---|
| **Direction** | ↑ ↗ ↖ ↓ ↘ ↙ | ↑ | Where the bubbles travel (vertical or diagonal). `R` / `Shift+R` rotate it. |
| **Spawn every** | 0.2 – 10 s | 1.5 | Time between two bubbles (lower = more bubbles). |
| **Speed** | 0.5 – 15 tiles/s | 3 | How fast bubbles travel. |
| **Distance** | 1 – 40 tiles | 8 | How far a bubble goes before it pops on its own. |

- Touching a bubble pops it and bounces the character up, like a stomp; hold jump for a full jump.
- Bubbles pass through the spawner itself but pop on any other solid tile.
- **Paint over** a spawner to apply the current settings; **middle-click** one to copy its settings.

---

## Goal pole

When the **Goal** tool is selected, the **Goal** panel opens on the left.

| Setting | Range | Default | Description |
|---|---|---|---|
| **Pole height** | 1 – 20 tiles | 5 | Height of the pole; the tile you place is its base. |

- Touching the pole anywhere completes the level.
- The score depends on how high the character's feet are on the pole, from **Flag bottom points** to **Flag top points** (see [Game system](#game-system-score--lives)). Both values are shown next to the pole.
- **Paint over** a goal to apply the current height; **middle-click** one to copy it. Goals from older levels are 1 tile high.

---

## NPCs & text boxes

The **Text box** is in the **Terrain** category; **NPC** and **Merchant** are in the **NPCs** category. Each one has its own settings, edited in a panel on the left when its tool is selected. As with springs, the panel's settings apply to the next ones you paint: **paint over** a placed one to apply them, **middle-click** one to copy its settings. While the tool is selected, every placed one shows its text in a bubble in the editor.

### 📜 Text box

- A solid block holding a text of up to 200 characters (line breaks are kept).
- In play, the text pops up in a bubble above the block while the character touches it (standing on it, pushing against it), and for 3 s after hitting it from below.

### 🧑 NPC

- Settings: **name**, **colour** and **1 to 5 sentences** (empty ones are skipped).
- In play, stand next to the NPC (a *↓ Talk* bubble appears) and press `↓` / `S`. The game pauses; each press of `Space` / `↓` shows the next sentence, `Esc` stops talking.
- NPCs can't be hurt and don't block the way.

### 🛒 Merchant

Each Merchant has its own **name**, **colour**, **greeting** and **inventory**: tick what it sells.

| Item | Effect | Price set in |
|---|---|---|
| **⭐ Power-ups** | All of them (including ones created later) or only the ticked ones. A bought power-up is given at once and replaces the current one. | ⭐ Power-ups › **🛒 Shop price** (per power-up, default 10) |
| **⏱ Time** | Adds *Seconds per purchase* (5 – 300, default 30, per Merchant) to the level timer. Only offered when the level has a time limit. | ⚙ Game system › ⏱ Time › **Price per second** (default 1) |
| **❤️ Extra life** | +1 life. | 🏃 Character › **Price of a life** (default 50) |
| **💗 Health point** | Restores 1 HP (not above the maximum). | 🏃 Character › **Price per health point** (default 10) |

- In play, stand next to the Merchant (a *↓ Shop* bubble appears) and press `↓` / `S`. The game pauses while the shop is open.
- `↑` / `↓` choose, `Space` buys, `Esc` or **Leave** closes the shop. Items you can't afford show their price in red.
- You pay with the coins collected during the current life (Big and Mega coins count for their value). Spent coins are gone; a price of 0 makes the item free.

---

## Character settings

Open with **🏃 Character** or `C`. Changes apply immediately, even while playing. When the panel is open, dashed **jump arcs** are drawn from the Start tile so you can check what the player can reach. The panel has two collapsible sections.

### 📏 Metrics

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
| **🛒 Price of a life** | 0 – 999 coins | 50 | Coins a Merchant asks for an extra life (0 = free). |
| **🛒 Price per health point** | 0 – 999 coins | 10 | Coins a Merchant asks to restore 1 HP (0 = free). |

### ✨ Perks

Abilities the character always has. Each perk's setting appears once it is ticked. A power-up can still grant a perk for a while even when it is off here.

| Perk | Setting | Default | Description |
|---|---|---|---|
| **🧗 Wall jump** | Wall slide speed: 0.5 – 20 tiles/s (default 3) | off | Jump off walls while in the air; hold toward a wall to slide down it slowly. |
| **🪂 Glide** | Glide fall speed: 0.5 – 8 tiles/s (default 2) | off | Hold jump while falling to float down slowly. |
| **🌀 Rotating jump** | Spin speed: 0.5 – 6 turns/s (default 2) | off | Jumps spin the character until it lands. While spinning, touching an enemy from any side hits it (−1 HP) and bounces you off, and Spin bricks shatter. |

**Reset defaults** restores the values above. The panel's info lines summarise air time, standing-jump size, shooting, health and perks.

---

## Power-ups

Open with **⭐ Power-ups** or `U`. Power-ups are made by you and saved with the level. The first time the editor runs you get eight examples:

| Preset | Effect |
|---|---|
| **Giant** | Size 160 %, speed 90 % |
| **Tiny** | Size 55 %, jump height 120 %, speed 115 % |
| **Wings** | Double jump |
| **Feather** | Glide |
| **Twister** | Rotating jump (3 turns/s) |
| **Climber** | Wall jump |
| **Fire** | Throws bouncing projectiles |
| **Star** | Invincibility for 10 s, speed 115 % |

### Managing power-ups

- Click a power-up in the list to edit it **and** select it for painting.
- **＋ New** creates one (up to 25). **Duplicate** copies the selected one. **🗑 Delete** removes it and every copy placed in the level (including copies hidden in Breakable blocks).
- **Name** (max 16 characters): its first letter is drawn on the pick-up orb.
- **Colour**: used for the orb, the player's headband and its effects.

### 📏 Stats

| Setting | Range | Description |
|---|---|---|
| **Duration** | 0 – 120 s | How long it lasts. **0 = until you lose a life.** The headband blinks during the last 2 seconds. |
| **Character size** | 30 – 300 % | Player size. Growing waits until there is enough room. |
| **Jump height** | 25 – 300 % | Multiplies the character's jump height. |
| **Jump width** | 25 – 300 % | Multiplies the character's jump width. |
| **Speed** | 25 – 300 % | Multiplies the character's speed. |
| **🛒 Shop price** | 0 – 999 coins | Coins a Merchant asks for it (default 10). 0 = free. |

### ✨ Abilities (tick to enable)

| Ability | Settings | Description |
|---|---|---|
| **🪽 Double jump** | Extra jumps in the air: 1 – 5 | Press jump again in mid-air. Refills on landing. |
| **🪂 Glide** | Glide fall speed: 0.5 – 8 tiles/s | Hold jump while falling to float down slowly. |
| **🌀 Rotating jump** | Spin speed: 0.5 – 6 turns/s | Jumps spin the character; while spinning, touching an enemy from any side hits it and bounces you off. |
| **🧗 Wall jump** | Wall slide speed: 0.5 – 20 tiles/s | Jump off walls in mid-air; hold toward a wall to slide down it slowly. |
| **🔥 Projectile throwing** | Projectiles on screen: 1 – 10 · Throw speed: 2 – 40 tiles/s · Bounce height: 0 – 4 tiles (0 = fly straight) | Throw with `X` / `J`. Replaces the character's normal shots while active. |
| **⭐ Invincibility** | — | Spikes, flames, poison, enemies and their shots can't hurt you, and touching an enemy defeats it (and gives its score). A rainbow outline shows it is on. **Pits and lava still cost a life**, unlike the Invincibility cheat. |

When both the character and the active power-up have glide, wall jump or rotating jump, the power-up's setting is used.

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
| **Helmet** | Immune to the rotating jump, 2 HP. |
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

### 📏 Stats

| Setting | Range | Default | Description |
|---|---|---|---|
| **Size** | 0.5 – 5 tiles | 0.75 | Width and height of the enemy. |
| **Health points** | 1 – 20 HP | 1 | Stomps or shots needed to defeat it (each one removes 1 HP). |
| **Score when defeated** | 0 – 10000 pts | 200 | Points gained when it is defeated. |
| **🥾 Can be stomped** | on / off | on | Off: landing on it hurts the player (it is drawn with spikes), so it must be shot. |
| **🌀 Immune to rotating jump** | on / off | off | On: the character's rotating jump doesn't damage it, and spinning into it hurts the player (it is drawn with a metal helmet). Stomp it with a normal jump or shoot it. |

### 🚶 Movement

| Mode | Direction | Behaviour |
|---|---|---|
| **■ Still** | Facing ← → | Doesn't move (floats where it is placed). |
| **🚶 Walk** | ← → | Walks with gravity, turning at walls and ledges. |
| **⇄ A ↔ B** | 8 directions | Flies back and forth between its tile (A) and B, horizontally, vertically or diagonally, through walls. |
| **➜ Endless** | 8 directions | Flies forever in one direction, through walls. Starts once it comes on screen; gone once it leaves the level. |

| Setting | Range | Default | Used by |
|---|---|---|---|
| **Speed** | 0.5 – 15 tiles/s | 2 | Walk, A ↔ B, Endless |
| **Distance A → B** | 1 – 30 tiles | 4 | A ↔ B (per axis on diagonals) |

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

Open the **⚙ Game system** menu. Its five sections can be collapsed.

| Section | Setting | Range | Default | Description |
|---|---|---|---|---|
| 🏆 Score | **Points per coin** | 0 – 10000 | 100 | Score for each coin (a Big or Mega coin gives its value × this). |
| 🏆 Score | **🚩 Flag top points** | 0 – 100000 | 5000 | Score for touching the goal pole at its very top. |
| 🏆 Score | **🚩 Flag bottom points** | 0 – 100000 | 100 | Score for touching the goal pole at its base. |
| 🏆 Score | **🚩 Flag score steps** | 0 – 20 | 0 | 0 = the flag score grows smoothly with height; 2 or more = the pole is split into that many score bands. |
| 🪙 Coins › Values | **Coin / Big coin / Mega coin** | 1 – 100 | 1 / 5 / 10 | How many coins each kind is worth. |
| 🪙 Coins › Sizes | **Big coin size % / Mega coin size %** | 50 – 250 | 100 / 100 | Size of the drawing and of the pickup area. |
| ❤️ Lives | **Coins for a life** | 0 – 999 | 100 | Collecting this many coins gives +1 life ("1UP"). 0 = never. |
| ⏱ Time | **⏱ Time limit (s)** | 0 – 999 | 0 | Seconds to reach the goal on each life. 0 = no time limit (no timer, and Merchants don't sell time). Running out of time costs a life. |
| ⏱ Time | **🛒 Price per second** | 0 – 100 | 1 | Coins a Merchant asks for each second of extra time (each Merchant sells time in packs of seconds). |
| ⚠️ Hazards | **☠️ Poison: seconds per HP** | 0.2 – 10 | 1 | Time spent in a Poison zone for each HP lost (lower = deadlier). The first hit comes after half this time. |

Points per enemy are set for each enemy type in the [Enemies editor](#enemies-1). Health points, starting lives and the Merchants' life / HP prices are set in the [Character panel](#character-settings).

With a time limit, the timer is shown in the HUD (red and blinking in the last 10 s). It stops while you talk to an NPC or shop, and with the ⏳ Endless time cheat.

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

Open the **🎮 Cheats** menu or use the keys below (they work in both modes). The Cheats button stays highlighted while any cheat is on, and the status bar shows its icon while playing.

| Cheat | Key | Effect |
|---|---|---|
| **🛡 Invincibility** | `I` | Spikes, flames, poison, enemies and their shots can't hurt you (touching an enemy defeats it), and falling into a pit or lava puts you back on the last solid ground you stood on. A golden outline shows it is on. The ⭐ Invincibility power-up ability does the same, except for pits and lava. |
| **⏳ Endless time** | `T` | Timed power-ups never run out and the level timer stops. |
| **🧊 No enemy AI** | `N` | Enemies stand still and don't shoot. You can still stomp them, and touching them still hurts. |

---

## Controls

### Editor

| Action | Input |
|---|---|
| Paint | Left click / drag |
| Erase | Right click / drag |
| Pick tile (and its settings) | Middle click |
| Select tile | `1`–`9`, `0`, `B`, `F`, `M`, `X`, `O`, `Y`, `G` |
| Rotate spring / bubbles (that tool selected) | `R` / `Shift+R` |
| Scroll horizontally | `←` `→` / `A` `D` (`Q` on AZERTY) or mouse wheel |
| Scroll vertically | `↑` `↓` / `W` `S` (`Z` on AZERTY) or `Shift` + wheel |
| Undo | `Ctrl+Z` |
| Character / Power-ups / Enemies panel | `C` / `U` / `E` |
| Cheats | `I` invincibility · `T` endless time · `N` no enemy AI |
| Help | `H` / `F1` |
| Play | `Enter` |
| Close menu / palette list / help | `Esc` |

### Play

| Action | Input |
|---|---|
| Move | `←` `→` / `A` `D` (`Q` on AZERTY) |
| Jump (hold for higher) | `Space` / `W` / `↑` / `Z` |
| Wall jump (with the perk/ability) | Jump while touching a wall in mid-air |
| Glide (with the perk/ability) | Hold jump while falling |
| Rotating jump (with the perk/ability) | Any jump spins you |
| Swim (in water) | Press jump to swim up; jump at the surface to leap out |
| Shoot / throw | `X` / `J` |
| Talk / open shop | `↓` / `S` next to an NPC or Merchant |
| Next sentence (talking) | `Space` / `↓` · `Esc` stops |
| Shop | `↑` `↓` choose · `Space` buy · `Esc` leave |
| Pause / resume | `P` |
| Restart the run | `R` |
| Cheats | `I` / `T` / `N` |
| Help (pauses the game) | `H` / `F1` |
| Back to the editor | `Enter` / `Esc` |

---

## Gameplay rules

- **A run** starts when you press Play and ends at game over. Score and lives carry over between lives; each life restarts the level from the Start tile with full HP.
- **Getting hit** (spikes, flames, enemies, enemy projectiles) costs 1 HP, knocks you back and makes you invulnerable (blinking) for 1.2 s. At 0 HP you lose a life.
- **Pits and lava**: falling out of the bottom of the level or touching lava always costs a whole life, whatever your HP.
- **Stomping**: landing on an enemy removes 1 of its HP and bounces you up. Hold jump while stomping for a full-height bounce. Enemies that can't be stomped hurt you instead.
- **Shots** fly straight, stop at solid tiles, remove 1 HP from the enemy they hit and disappear off screen.
- **Jump feel**: releasing jump early cuts the jump short. A short grace period lets you jump just after walking off a ledge (or leaving a wall) or just before landing.
- **Rotating jump**: every jump spins you until you land (gliding, wall-sliding, swimming or getting hit also stops it). While spinning, touching an enemy from any side — even one that can't be stomped — removes 1 of its HP and bounces you off, unless the enemy is immune.
- **Invincibility** from a ⭐ power-up (rainbow outline) protects you from spikes, flames, poison, enemies and their shots, and defeats any enemy you touch. Pits and lava still cost a life.
- **Wall jump** kicks you away from the wall in a full-size jump; you briefly can't steer back toward it.
- **Bricks, coins and power-ups** come back on each new life.
- **Level edges** act as walls on the left and right.
- **Goal**: touching the pole completes the level and gives flag points by height (shown on the end screen). Press `R` to play again or `Enter` to edit.
- **Game over** when the last life is lost. Press `R` to try again.
- **Time limit** (if set in ⚙ Game system): running out of time costs a life; each life starts with the full time.
- **Coins** collected during a life can be spent at Merchants; the counter restarts at 0 on each new life.
- **HUD** (top-left): hearts for HP, then score, coins collected / total, lives and the timer (when there is a time limit).

---

## Saving, loading & file format

**What the browser remembers automatically**: character settings, game-system settings, power-ups, enemies, moving-platform, spring, flame-jet, bubble, goal, text-box, NPC and merchant settings, screen size, editor layout, cheats and which panel sections are open.

**The level itself** is only stored when you click **Save** (browser) or **Export** (file). On start-up, the level saved in the browser is loaded.

Saved and exported levels include the tiles, character settings, game-system settings, moving-platform, spring, flame-jet, bubble-spawner and goal settings, text boxes, NPCs, merchants, hidden items, power-ups and enemies, so a level file is self-contained. Loading or importing a level replaces your current character, game-system, power-up and enemy settings with the level's. Older levels without enemy types still load: their `e` tiles become a Walker.

### `level.json`

```json
{
  "w": 120,
  "h": 18,
  "rows": ["....", "..."],
  "char": { "jumpH": 3.4, "jumpW": 4.8, "speed": 7.2, "impact": 0, "projSpeed": 14, "projMax": 3, "hp": 3, "lives": 3, "lifePrice": 50, "hpPrice": 10,
            "wallJump": false, "wallSlide": 3, "glide": false, "glideFall": 2, "spinJump": false, "spinSpeed": 2 },
  "sys": { "coinPoints": 100, "flagTop": 5000, "flagBottom": 100, "flagSteps": 0, "coinsPerLife": 100,
           "coinVal": 1, "bigVal": 5, "megaVal": 10, "bigSize": 100, "megaSize": 100, "poisonRate": 1,
           "timeLimit": 0, "timePrice": 1 },
  "meta": {
    "12,9": { "mode": "h", "dir": "r", "dist": 4, "speed": 2 },
    "20,15": { "h": 9, "w": 8, "rot": 0, "path": "arc", "dist": 6, "speed": 20 },
    "30,11": { "item": "c" },
    "8,12": { "text": "Hello! Touch me to read me." },
    "10,15": { "name": "Villager", "color": "#d9a441", "lines": ["Hello, traveller!", "The goal is to the right.", "", "", ""] },
    "14,15": { "name": "Merchant", "color": "#2f8f5b", "greet": "Welcome!", "allPowers": false, "powers": ["A"],
               "time": true, "timeAmt": 30, "life": true, "hp": true }
  },
  "powerups": [ { "id": "A", "name": "Giant", "color": "#e94560", "size": 160, "speed": 90, "price": 10 } ],
  "enemies": [ { "id": "e", "name": "Walker", "color": "#c94f6d", "size": 0.75, "hp": 1, "points": 200, "stompable": true, "spinImmune": false,
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
| `^` | Flame jet | `@` | Lava |
| `~` | Water | `;` | Poison |
| `!` | Power brick | `$` | Big coin |
| `%` | Coin brick | `*` | Mega coin |
| `&` | Spin brick | `+` | Bubble spawner |
| `#` | Text box | `[` | NPC |
| `]` | Merchant | | |

Enemy `id`s are taken from `eadhilnoqrtuwxyz0123456789`. Enemy `mode` is `still`, `walk`, `path` (A ↔ B) or `line` (endless); `shotDir` is `face`, `lr`, `up`, `down` or `ud`.

`meta` keys are `"x,y"` tile coordinates. What the entry holds depends on the tile there:

- **Moving platform** (`m`): `mode` is `h`, `v`, `d` or `c`; `dir` is `r`, `l`, `u`, `d`, `ur`, `dr`, `dl`, `ul`, `cw` or `ccw`.
- **Spring** (`j`): `rot` is 0–7 (45° steps clockwise from straight up); `path` is `arc` (uses `h`, `w`) or `line` (uses `dist`, `speed`).
- **Breakable** (`k`): `item` is a coin kind (`c`, `$`, `*`) or a power-up `id`.
- **Flame jet** (`^`): `h` (flame height, tiles), `on` / `off` (burn / pause time, s), `delay` (s).
- **Bubble spawner** (`+`): `rot` is 0, 1, 7 (↑ ↗ ↖) or 3, 4, 5 (↘ ↓ ↙); `every` (s), `speed` (tiles/s), `dist` (tiles).
- **Goal** (`f`): `h` is the pole height in tiles (1 if missing).
- **Text box** (`#`): `text` (up to 200 characters).
- **NPC** (`[`): `name`, `color`, `lines` (5 strings; empty ones are skipped).
- **Merchant** (`]`): `name`, `color`, `greet`; `allPowers` (sell every power-up) or `powers` (list of power-up `id`s); `time` with `timeAmt` (seconds per purchase), `life`, `hp` (true = sold). Prices are global (power-ups, Game system, Character).

---

## Tips

- Keep the **Character panel** open while designing gaps: the jump arcs from the Start tile show exactly what is reachable.
- Hide coins or power-ups inside **Breakable** blocks for secret rewards.
- A row of **Falling** platforms over a pit makes a quick "keep running" section.
- Sideways or **straight** springs make fast launch sections; select the Spring tool to see every trajectory.
- Build tall shafts and give the player **Wall jump** (perk or Climber power-up) to climb them.
- Use **Invincibility** and **No enemy AI** to test the layout of long levels quickly, then turn them off to test difficulty.
- Put a **Merchant** before a hard section and price **HP** so players must collect coins to afford it.
- Use **Text boxes** for hints and **NPCs** for story; select their tool to proofread every text in the editor.
- **Export** often: browser storage can be cleared.
