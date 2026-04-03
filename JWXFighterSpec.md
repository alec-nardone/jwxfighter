## JWX AIPoC Fighting Game — "HELLO WORLD" Complete Game Specification
**Document Type:** Technical Game Specification

**Purpose:** One-shot implementation spec for Claude AI coding demonstration

**Team:** AIPoC (AI Proof of Concept)

**Date:** April 3, 2026

**Status:** Draft

## Overview
### Concept
**"HELLO WORLD"** is a 1v1 arcade-style fighting game built as a browser-based single-page application, inspired by Street Fighter II (SNES era). It serves as a showcase piece for the JWX AIPoC team — demonstrating the capability to one-shot a complex, polished interactive application using AI-assisted coding.

The game features eight playable/opponent characters drawn from the JWX brand family — each rendered as a pseudo-anthropomorphic 16-bit sprite of their respective company logo, with floating arms and legs. The player selects one character and fights through all others in a fixed gauntlet. The final boss — **"HELLO"**, a giant spinning Earth globe with floating arms and legs and the word "HELLO" painted across its face — is the secret villain teased throughout the game.

### Tone & Style
- **Visual style:** 16-bit pixel art aesthetic (SNES-era resolution feel: 256×224 logical pixel canvas, scaled up to fill viewport)
- **Color palette:** Brand-accurate colors per character; rich parallax scrolling backgrounds per stage
- **Audio:** Chiptune / 8-bit synthesized music and sound effects (Web Audio API generated or sprite-based)
- **Pacing:** Fast, arcade-snappy. Rounds are 90 seconds. Best of 3 rounds per match.
- **Difficulty:** Single player vs. CPU gauntlet — 7 opponent fights + 1 boss fight
### Win Condition
The player completes the game by defeating all 7 opponent characters in sequence, then defeating **HELLO** (the final boss). Upon defeating HELLO, the globe explodes and the word `> HELLO WORLD` types out across the screen in terminal-green text — the payoff moment.

### Tech Stack Constraint
The entire game MUST be delivered as a **single self-contained HTML file** with no external dependencies beyond standard browser APIs. All assets (sprites, audio, fonts) must be either:

- Procedurally generated via JavaScript Canvas API, or
- Base64-encoded inline
- This is a deliberate AI coding challenge constraint.
## Character Roster
All characters are rendered as **16-bit pixel-art sprites** approximately **64×80 pixels** (logical canvas units) depicting their respective logo as a body torso/head, with two floating arms and two floating legs that animate independently. Arms and legs maintain a small gap from the body and move with bounce/float animations. Each character has a **brand-accurate color palette** (primary + secondary + shadow colors).

There are **8 player-selectable characters** (including the one the player picks, who then becomes unavailable as an opponent). The **final boss** is non-selectable.

### 1. JWX
- **Body:** The JWX wordmark logo block (white text on dark background, square-ish body)
- **Colors:** `#000000` body, `#FFFFFF` text, `#FF4B00` accent (JWX orange)
- **Arms/Legs:** Dark charcoal floating limbs with orange joint dots
- **Personality:** Powerful all-rounder. The "Ryu" of the roster. Balanced stats.
- **Special Visual:** Body glows orange when executing a special move
### 2. JW Player
- **Body:** The JW Player logo — interlocking `JW` lettermark in a rounded rectangle
- **Colors:** `#FF4500` primary (JW red-orange), `#FFFFFF` lettermark, `#1A1A1A` dark outline
- **Arms/Legs:** Orange-tinted floating limbs
- **Personality:** Fast striker. Low health, high speed. The "Chun-Li" archetype.
- **Special Visual:** Lettermark pulses on hit
### 3. Connatix
- **Body:** Connatix logo mark — the stylized `C` arc/swoosh shape
- **Colors:** `#6C3BFF` purple, `#FFFFFF` inner, `#4A20D4` shadow purple
- **Arms/Legs:** Purple-tinted floating limbs with white highlight dots
- **Personality:** Trickster/zoner. Projectile-heavy. The "Dhalsim" archetype.
- **Special Visual:** Purple particle trail on special moves
### 4. VUALTO
- **Body:** VUALTO wordmark block — bold uppercase sans-serif
- **Colors:** `#00B4D8` cyan/teal, `#FFFFFF` text, `#0077A8` shadow
- **Arms/Legs:** Teal-tinted limbs
- **Personality:** Heavy grappler. Slow, high damage, high health. The "Zangief" archetype.
- **Special Visual:** Shockwave ring on grabs
### 5. InPlayer
- **Body:** InPlayer logo — stylized `in` mark or wordmark block
- **Colors:** `#E63946` red, `#FFFFFF` text, `#9B1D24` dark red shadow
- **Arms/Legs:** Red floating limbs
- **Personality:** Counter-fighter. High defense, punish-heavy moveset. The "Guile" archetype.
- **Special Visual:** Shield flash animation on successful block
### 6. Aug X Labs (Augie)
- **Body:** Augie character/logo — the Aug X Labs "Augie" mascot or `AX` stylized mark
- **Colors:** `#FFD700` gold/yellow, `#FF6B00` orange accent, `#2A1A00` dark outline
- **Arms/Legs:** Gold floating limbs with orange glow
- **Personality:** Wild card / rushdown. Highest speed on roster. The "Blanka" archetype.
- **Special Visual:** Electric sparks on attacks; body flashes gold during super
### 7. Quantum Path
- **Body:** Quantum Path logo mark — geometric/abstract symbol or wordmark
- **Colors:** `#00FF88` neon green, `#001A0D` dark background body, `#00CC66` mid green
- **Arms/Legs:** Neon green floating limbs with dark joints
- **Personality:** Technical/defensive. Moderate speed, complex move chains. The "Ken" mirror archetype.
- **Special Visual:** Matrix-style digit rain particle on specials
### 8. HELLO (Final Boss — Non-Selectable)
- **Body:** A large spinning **Earth globe** (~96×96 px, larger than all other fighters) — rendered with visible continent outlines in pixel art. The word **"HELLO"** is painted in bold white letters across the front face of the globe (wrapping around the equator band).
- **Colors:** Ocean blue `#1A6EBD`, land green `#2D8A4E`, "HELLO" text `#FFFFFF` with black outline, atmosphere glow `#87CEEB`
- **Arms/Legs:** Massive dark-grey floating limbs, larger than any other character's
- **Globe Animation:** Slowly rotates on its Y-axis during idle; spins fast during special moves
- **Personality:** Boss archetype — all moves hit harder, more health (3× standard pool), can use all projectile types
- **Tease:** During the gauntlet (fights 4–7), between rounds, a brief **world map silhouette flashes** in the background for 1–2 frames with a rumble effect and an ominous bass note — hinting that something is watching. At fight 7's victory screen, a shadow of HELLO appears and the screen distorts briefly before cutting to the boss intro.
### Stat Summary Table
## Character Health Speed Attack Special JWX ★★★ ★★★ ★★★ ★★★ JW Player ★★ ★★★★★ ★★★ ★★ Connatix ★★ ★★★ ★★ ★★★★★ VUALTO ★★★★★ ★★ ★★★★ ★★★ InPlayer ★★★★ ★★★ ★★★ ★★★★ Aug X Labs ★★ ★★★★★ ★★★★ ★★★ Quantum Path ★★★ ★★★★ ★★★ ★★★★ **HELLO (Boss)** ★★★★★★ ★★★ ★★★★★ ★★★★★ Game Engine & Technical Architecture
## Character Health Speed Attack Special JWX ★★★ ★★★ ★★★ ★★★ JW Player ★★ ★★★★★ ★★★ ★★ Connatix ★★ ★★★ ★★ ★★★★★ VUALTO ★★★★★ ★★ ★★★★ ★★★ InPlayer ★★★★ ★★★ ★★★ ★★★★ Aug X Labs ★★ ★★★★★ ★★★★ ★★★ Quantum Path ★★★ ★★★★ ★★★ ★★★★ **HELLO (Boss)** ★★★★★★ ★★★ ★★★★★ ★★★★★ Game Engine & Technical Architecture
### Runtime Environment
- **Platform:** Browser (Chrome, Firefox, Safari, Edge — latest versions)
- **Rendering:** HTML5 `<canvas>` element, 2D context (`ctx.getContext('2d')`)
- **Game loop:** `requestAnimationFrame`-based loop, targeting **60 FPS**
- **Logical resolution:** **480×270** logical pixels (16:9, scaled up via CSS `transform: scale()` to fill the viewport while maintaining aspect ratio)
- **Delivery:** Single `index.html` file — zero external dependencies
### Canvas Architecture
```
[Root Canvas 480×270]
  ├── Layer 0: Background (far parallax — sky/backdrop)
  ├── Layer 1: Background (mid parallax — scenery elements)
  ├── Layer 2: Background (near parallax — foreground props)
  ├── Layer 3: Stage floor
  ├── Layer 4: Characters + projectiles
  ├── Layer 5: Hit effects / particles
  └── Layer 6: HUD overlay (always on top)

```
All layers are drawn to the **same single canvas** in order each frame using the game loop. No offscreen canvases are required (though the implementation may use one for sprite caching).

### Game Loop
```
gameLoop(timestamp):
  delta = timestamp - lastTimestamp
  lastTimestamp = timestamp

  processInput()
  updateGameState(delta)
    ├── updatePhysics(delta)
    ├── updateAnimations(delta)
    ├── updateAI(delta)
    ├── checkCollisions()
    └── updateParticles(delta)
  
  render()
    ├── clearCanvas()
    ├── drawBackground()
    ├── drawCharacters()
    ├── drawProjectiles()
    ├── drawParticles()
    └── drawHUD()

  requestAnimationFrame(gameLoop)

```
Delta time is used for physics and animation, but **combat frame timing is integer-frame-based** (60 = 1 second) to keep fighting game logic deterministic.

### Input System
**Player 1 (keyboard):**

Action Key Move Left `←` Arrow or `A` Move Right `→` Arrow or `D` Jump `↑` Arrow or `W` Crouch `↓` Arrow or `S` Light Punch `U` Heavy Punch `I` Light Kick `J` Heavy Kick `K` Block `O` or `L` Special Move Directional combo + attack key (see Combat System) **Input buffer:** Maintain a **16-frame rolling input buffer** per player. Special move detection reads this buffer. A special move is triggered if the correct sequence appears within the buffer window.

**Input is disabled** during: knockdown animation, round-start countdown, round-end animation, victory screen.

### Physics Constants
```
const PHYSICS = {
  GRAVITY: 1800,          // px/s² (logical pixels)
  JUMP_VELOCITY: -620,    // px/s initial upward velocity
  MAX_FALL_SPEED: 900,    // px/s terminal velocity
  WALK_SPEED: 160,        // px/s ground movement
  DASH_SPEED: 380,        // px/s dash
  DASH_DURATION: 0.18,    // seconds
  KNOCKBACK_VELOCITY: 280,// px/s on hit
  GROUND_Y: 210,          // Y coordinate of floor surface
  LEFT_BOUNDARY: 30,      // min X for any character
  RIGHT_BOUNDARY: 450,    // max X for any character
  PUSH_DISTANCE: 48,      // minimum gap between character centers
};

```
Characters cannot overlap. If both characters are pushed against the same wall, the wall yields in favor of the attacking character.

### State Machine (Per Character)
Each character object runs a finite state machine. States:

```
IDLE → WALKING → JUMPING → CROUCHING
IDLE → ATTACK_LIGHT_PUNCH
IDLE → ATTACK_HEAVY_PUNCH
IDLE → ATTACK_LIGHT_KICK
IDLE → ATTACK_HEAVY_KICK
IDLE → ATTACK_SPECIAL
IDLE → BLOCKING
ANY  → HIT_STUN (on receiving hit)
ANY  → KNOCKDOWN (on health ≤ 0 or heavy knockback)
KNOCKDOWN → RISING
RISING → IDLE

```
Each state has:

- `duration` (frames)
- `cancellable` (bool — whether it can be interrupted by another input)
- `hitbox` (active attack box, null if not attacking)
- `hurtbox` (area that receives damage — always active unless blocking)
- `velocity_x_override` (optional, overrides physics during animations like dashes)
### Sprite Rendering (Procedural)
All character sprites are **drawn procedurally** using Canvas 2D API geometric primitives — rectangles, arcs, bezier curves, and `fillText`. No image files.

**Character sprite structure (per draw call):**

- Draw **legs** (two floating rectangles below body, slight hover offset based on animation frame)
- Draw **body** (main logo shape — rectangle with logo text/mark drawn inside)
- Draw **arms** (two floating rectangles to sides of body, offset based on attack state)
- Draw **face/logo details** (text, arcs, brand marks using canvas paths)
- Apply **shadow** (semi-transparent ellipse under character)
- **Animation frames** are defined as keyframe deltas applied to the base draw positions. No sprite sheets — all animation is parametric.
### Collision System
Two box types per character:

- **Hurtbox:** Slightly inset from the full sprite bounding box. Always active.
- **Hitbox:** Extends beyond the character on the attack side. Only active during specific attack frames.
```
// Example hitbox structure
{
  x_offset: 40,   // from character center
  y_offset: -20,  // from ground
  width: 30,
  height: 20,
  damage: 12,
  stun_frames: 15,
  knockback_x: 200,
  knockback_y: -100,
  type: 'punch' | 'kick' | 'projectile' | 'throw' | 'special'
}

```
Collision detection runs **once per frame** after physics update. A hitbox that has already landed (`hasHit = true`) does not fire again until the attack animation resets.

### Projectile System
Projectiles are independent objects with their own position, velocity, hitbox, and owner reference. They are destroyed on:

- Hitting the opponent
- Hitting the stage boundary
- Being cancelled by another projectile (mutual destruction)
- Owner's projectile cooldown timeout (max 1 active projectile per character at a time)
### Memory / Performance Budget
Since this is a single HTML file targeting modern browsers:

- No WebGL — pure 2D Canvas
- No audio files — all sound generated via **Web Audio API** oscillators and noise
- Frame budget: <16ms per frame
- Canvas clear + redraw every frame (no dirty region optimization needed at this resolution)
## Character Selection Screen
### Layout
The character selection screen fills the full canvas (480×270). It consists of:

```
┌─────────────────────────────────────────────────────┐
│          ★  HELLO WORLD  ★  [flashing title]        │  ← Title bar (top 30px)
├───────────────┬─────────────────────────────────────┤
│               │                                     │
│  [PLAYER 1]   │      CHARACTER PORTRAIT PANEL       │
│  CURSOR BOX   │   (large animated sprite, 128×160)  │
│               │    + Character name (flashing)      │
├───────────────┘    + Stat bars (SPD / ATK / HP)     │
│                                                     │
│   ┌────┐ ┌────┐ ┌────┐ ┌────┐                      │
│   │ C1 │ │ C2 │ │ C3 │ │ C4 │  ← Row 1 (4 chars)  │
│   └────┘ └────┘ └────┘ └────┘                      │
│   ┌────┐ ┌────┐ ┌────┐ ┌────┐                      │
│   │ C5 │ │ C6 │ │ C7 │ │ ?? │  ← Row 2 (3 + 1 ???)│
│   └────┘ └────┘ └────┘ └────┘                      │
│                                                     │
│           [PRESS ENTER TO FIGHT]                    │  ← Bottom bar
└─────────────────────────────────────────────────────┘

```
- **Character grid:** 4×2 grid of portrait tiles, each **64×64 px**
- **Grid position:** Centered horizontally, in the lower 60% of the screen
- **8th slot (bottom-right):** Shows `???` with a dark/locked appearance and a **pulsing red glow** — this is HELLO's locked slot. Cannot be selected. Hovering it plays a distorted bass stab sound.
- **Portrait panel (right side):** Displays a large (~128×160 px) animated idle sprite of the currently highlighted character, their name in pixel font, and three stat bars: SPD, ATK, HP (filled left-to-right with color bars)
### Character Portrait Tiles
Each tile (64×64) contains:

- A **miniature version** of the character's logo sprite (centered, ~40×48 px)
- The **character's name** in 6pt pixel font below the sprite
- A **colored border** matching the character's primary brand color
- **Idle bob animation**: sprite bounces up/down ±2px on a 1.5s sine loop
- When a tile is **selected** (cursor on it):
- Border color pulses (full brightness → dimmed → full, 0.4s cycle)
- Portrait panel updates to show the full animated preview
- A **cursor selection SFX** fires (short beep, ~220Hz, 80ms)
- When a tile is **confirmed** (player presses Enter/confirm):
- The tile flashes white 3× rapidly
- A **confirm SFX** fires (ascending two-note chime)
- Transition animation begins (see below)
### Navigation
- **Arrow keys** (or WASD): Move cursor across the grid
- **Enter / Space**: Confirm selection
- Cursor wraps around edges (left from col 1 → col 4, etc.)
- The `???` tile is navigable (cursor can land on it) but cannot be confirmed — attempting to press Enter on it plays an error buzz (150Hz, 200ms)
### Transition Animation (Selection → Fight)
- Selected character tile **zooms to fill** the full canvas (200ms ease-in)
- Screen **flashes white** (2 frames)
- **VS screen** appears: Player character on left, first opponent on right, large `VS` text center
- VS screen holds for **1.5 seconds** with a dramatic ascending chime
- Both character sprites do an "intro pose" (arm raised, slight forward lean)
- **Stage fade-in**: VS screen dissolves, stage background fades in, characters drop from top into start positions
### Fight Order (Gauntlet Sequence)
The opponent order is **fixed** regardless of which character the player picks. The player's chosen character is removed from the opponent pool:

Fight # Opponent Stage 1 JW Player The Broadcast Stage 2 Connatix The Ad Network Alley 3 VUALTO The Stream Vault 4 InPlayer The Paywall Plaza 5 Aug X Labs The AI Lab 6 Quantum Path The Data Grid 7 [Player's character's "mirror" — swap with displaced char] Mirror Stage 8 **HELLO (Boss)** The Globe Arena If the player selects a character that appears in the above order, that opponent slot is replaced by the character that would have been in position 7 (mirror fight). The boss fight always remains fight #8.### Title Screen (Pre-Selection)

Before the character select screen, display a **title screen**:

- Black background with animated pixel stars (slow rightward scroll)
- **"HELLO WORLD"** title text in large pixel font, center screen — letters appear one-by-one with typewriter SFX, then the whole title **pulses** with a red glow
- Below title: A **silhouette of the Earth globe** (HELLO's form) barely visible in the background, very dark — only visible on close inspection. No label. Easter egg.
- Prompt: `PRESS ENTER TO START` (blinking, 1s on/off)
- Press Enter → character select screen with a swoosh transition SFX
## Combat System
### Core Combat Overview
Combat follows classic 2D fighting game conventions. Two characters face each other on a 2D plane (no depth/Z-axis). The player fights the CPU opponent. Best of 3 rounds wins the match, then the next opponent loads.

### Move Categories
- Normal Moves (Button Presses) Move Input Startup Active Recovery Damage Stun Light Punch (LP) `U` 4f 3f 8f 5 10f Heavy Punch (HP) `I` 8f 4f 18f 12 20f Light Kick (LK) `J` 5f 3f 10f 6 12f Heavy Kick (HK) `K` 10f 5f 22f 15 25f Crouching LP `↓ + U` 4f 2f 8f 4 8f Crouching HK `↓ + K` 12f 6f 28f 14 0f (knockdown) Jump LP (in air) `U` 5f 4f — 7 12f Jump HK (in air) `K` 7f 5f — 16 knockdown `f` = frames (at 60fps, 1 frame = ~16.6ms)**Startup frames:** Character commits to the move, hitbox not yet active.
**Active frames:** Hitbox is live — can connect with opponent.

**Recovery frames:** Animation completes, character cannot act.

**Stun frames:** Opponent is locked in hit-stun for this many frames on connect.

- Special Moves (Universal — All Characters)All 7 non-boss characters share the same **base special move set**, with visual differences per character:
- Move Name Input Sequence Description **Fireball** `→ ↘ ↓ + LP or HP` (QCF + punch) Launches a horizontal projectile. LP = slow, HP = fast. **Rising Uppercut** `→ ↓ ↘ + LP or HP` (DP + punch) Leaps diagonally forward, invincible on frames 1–4, heavy knockback on hit. **Spinning Kick** `↓ ↙ ← + LK or HK` (QCB + kick) Spinning horizontal kick, moves character forward. HK version hits twice. **Dash** `→ →` or `← ←` Short burst of forward/backward movement. Not an attack. 12-frame animation. Each character's **visual flavor** for specials differs:
- **JWX Fireball:** Orange energy disc
- **JW Player Fireball:** Red play-button-shaped bolt
- **Connatix Fireball:** Purple arc burst (curves slightly)
- **VUALTO Fireball:** Cyan shockwave ring (slow, wide)
- **InPlayer Fireball:** Red shield projectile (bounces once off ground)
- **Aug X Labs Fireball:** Gold lightning bolt
- **Quantum Path Fireball:** Green matrix-code sphere
- Character-Unique Special Move (Super)Each character has **one Super Move** activated by a **two-motion input** requiring the Super Meter to be full:
**Super input:** `→ ↘ ↓ ↙ ← → + HP` (half-circle forward + HP)

Character Super Name Effect JWX **Stream Dominator** Fires 3 orange discs in rapid succession; each hits for 10 dmg JW Player **Broadcast Rush** Teleports behind opponent, 5-hit combo, ends with launcher Connatix **Ad Barrage** Fills screen with 8 small purple projectiles from above VUALTO **Stream Lock** Grabs opponent and pile-drives them for 45 dmg; unblockable InPlayer **Paywall** Deploys a solid barrier that blocks all projectiles for 5 seconds Aug X Labs **Augmented Fury** Grows 50% larger for 8 seconds; all attacks +50% dmg Quantum Path **Quantum Leap** Becomes invisible for 3 seconds; attacks still register Super moves **freeze the screen for 8 frames** on activation (flash-freeze cinematic effect), then play out.

- Blocking & Defense- Action Input Effect Standing Block Hold `←` (facing right) or `→` (facing left) + no attack Blocks mid and high attacks. Takes **10% chip damage** (reduced damage on block). Crouching Block `↓ + ←` (or `↓ + →`) Blocks low attacks. Also blocks most mid attacks. Takes 10% chip damage. Parry Press `→` (toward opponent) within 3f of incoming hit Perfect parry — absorbs hit, no damage, brief stun on attacker (8f). Single-use per instance. **Cannot block throws/grabs**
- Blocking resets the **Super Meter charge** for the blocking player by –5% per blocked hit
- Blocking during a crouching heavy kick sweep attack does **NOT** prevent knockdown
- Throw / Grab- Move Input Range Damage Forward Throw `← / → + LP + LK` simultaneously 32px 20 dmg + positional reset Air Throw (in air) `LP + LK` 28px 18 dmg + knockdown Throws bypass blocking entirely
- If both characters input throws simultaneously within 3 frames of each other: **Throw Tech** — both pushed back, no damage
- Throw has **5f startup, 0f active window** (point-range, must be within range on frame 5)
- After a throw, the **thrower recovers in 20f**, thrown character recovers in **35f** (opportunity for follow-up)
### Hit Reactions & Knockback
Hit Type Reaction Light hit (LP/LK) Character pushes back slightly (30px), enters hit-stun Heavy hit (HP/HK) Character launches backward (80px), hit-stun + brief airtime Sweep (crouching HK) Hard knockdown — character falls and must rise Rising Uppercut Wall-of-the-screen sends opponent into short juggle state Juggle Additional hits in the air deal 75% damage (juggle scaling) Super hit Launches far back, usually to stage boundary **Combo scaling:** Each consecutive hit in a combo reduces damage by **10% per hit** (down to 20% floor). So a 10-hit combo's last hit deals ~20% of its base damage.

### Jump System
- **Neutral Jump:** `↑` — character jumps straight up, ~1.2 second air time
- **Forward Jump:** `↑ + →` — parabolic arc forward
- **Back Jump:** `↑ + ←` — parabolic arc backward (escape tool)
- **Jump Cancel:** Certain normal attacks can be cancelled into a jump (jump-cancel window = 6 frames after a light attack connects)
- **Double Jump:** NOT available (not in the Street Fighter paradigm)
- **Air moves:** LP, HK available in air. No crouching attacks in air.
- **Landing lag:** 3f upon landing — character cannot act immediately
### Super Meter
- Each character has a **Super Meter** (0–100)
- Meter **charges by:**
- Landing a hit: +5
- Being hit: +8 (rage-charge)
- Landing a parry: +15
- Blocking: +2 per blocked hit
- **Depletes** fully on Super Move use (to 0)
- Meter is **preserved between rounds** within a match (carries over)
- Meter resets to 0 at the start of a **new match** (new opponent)
- Visual: Displayed on HUD as a glowing yellow bar (see HUD section)
### Combo System
A **combo counter** appears above the hit opponent whenever consecutive hits land without the opponent recovering. Rules:

- Hits within **10 frames** of each other extend the combo
- Combo counter displays as `Nx` (e.g., `4x HIT`) in yellow pixel font, center-screen
- Combo counter briefly scale-animates on each increment
- On combo end, counter holds for 60 frames then fades
- **Combo counter does NOT display for 1-hit attacks** (only 2+ hits)
### Hitbox Visualization (Debug Mode)
Include a hidden debug mode toggled by pressing `F1`:

- Renders all active hitboxes as **red semi-transparent rectangles**
- Renders all hurtboxes as **blue semi-transparent rectangles**
- Renders stage boundaries as **yellow vertical lines**
- Displays current character state string above each character
- Displays current frame count in top-right corner
### Move Cancel Rules (Links & Chains)
- **Light → Heavy cancel:** LP or LK can be cancelled into HP or HK on hit (not on block)
- **Normal → Special cancel:** Any normal attack can be cancelled into a special move on hit or block (standard Street Fighter cancel)
- **Special → Super cancel:** A special move can be cancelled into a Super if meter is full (rare/advanced)
- **Cannot cancel:** Heavy Kick sweep, knockdown states, throws, or recovery frames of Heavy Punch
## Environments & Stages
### Stage Architecture
Each stage is a **2D parallax scrolling environment** painted behind the fighters. The stage has three depth layers (far, mid, near) that scroll at different rates as the camera pans to follow the fight. The **camera follows the midpoint** between both characters and pans horizontally only — no vertical camera movement.

**Stage dimensions:**

- **Visible canvas area:** 480×270 px
- **Total stage width:** 960 px (2× the canvas — allows panning)
- **Floor Y position:** 210 px (constant across all stages)
- **Camera pan limits:** Characters cannot walk off either end of the stage (hard boundary walls at x=30 and x=930 in stage space)
- **Parallax scroll rates:**
## Layer Scroll Factor Description Far (Layer 0) 0.2× camera pan Distant skyline / backdrop Mid (Layer 1) 0.5× camera pan Main scenery elements Near (Layer 2) 0.8× camera pan Foreground props/elements Floor (Layer 3) 1.0× (fixed) The stage floor surface Stage 1 — The Broadcast Stage
### Layer Scroll Factor Description Far (Layer 0) 0.2× camera pan Distant skyline / backdrop Mid (Layer 1) 0.5× camera pan Main scenery elements Near (Layer 2) 0.8× camera pan Foreground props/elements Floor (Layer 3) 1.0× (fixed) The stage floor surface Stage 1 — The Broadcast Stage
**Opponent:** JW Player

- **Backdrop:** A dark broadcast studio at night. Large video screens on the back wall play a looping playback animation (a simple pixel-art "play" button pulsing).
- **Mid layer:** Broadcast cameras on tripods, spotlight cones sweeping slowly
- **Near layer:** Cable bundles on the floor, a "LIVE" sign on the left wall that blinks red
- **Floor:** Polished dark wood stage floor with subtle reflection
- **Colors:** Deep navy `#0D1B2A`, monitor glow `#FF4500`, spotlight white `#FFFFEE`
- **Ambient effect:** Dust motes drifting upward (8–12 white 1px particles, slow float)
- **Stage interaction:** If a character is knocked into the left wall, the "LIVE" sign sparks (visual only — 6-frame spark burst)
### Stage 2 — The Ad Network Alley
**Opponent:** Connatix

- **Backdrop:** A neon-drenched city alley at night. Digital ad billboards line the far wall, cycling through fake ad copy ("BUY AD SPACE", "CPM: 9999", "CLICK HERE") in pixel text
- **Mid layer:** Purple-tinted lamp posts, glowing manhole covers
- **Near layer:** Stacked ad server boxes (blinking status LEDs), scattered USB cables
- **Floor:** Wet cobblestone with neon reflections (gradient overlay)
- **Colors:** Midnight purple `#1A0030`, neon `#6C3BFF`, wet stone `#2A2A2A`
- **Ambient effect:** Rain particles — thin vertical lines, 40px tall, semi-transparent, falling at slight angle
- **Stage interaction:** Billboard text cycles every 4 seconds. During supers, all billboards flash white simultaneously.
### Stage 3 — The Stream Vault
**Opponent:** VUALTO

- **Backdrop:** A high-tech server vault. Massive server racks recede into the background with blinking blue/green LEDs in grid patterns
- **Mid layer:** Holographic data stream lines (horizontal cyan lines) flowing right-to-left
- **Near layer:** Industrial floor grating, warning stripe tape on left/right edges
- **Floor:** Metal grating floor with subtle blue under-glow
- **Colors:** Steel grey `#2A3240`, cyan `#00B4D8`, LED green `#00FF44`
- **Ambient effect:** Data stream particles (cyan dots) flowing horizontally across mid-layer at slow speed
- **Stage interaction:** When a heavy attack lands, the nearest server rack column flickers its LEDs (random blink pattern, 20 frames)
### Stage 4 — The Paywall Plaza
**Opponent:** InPlayer

- **Backdrop:** A grand marble-floored plaza with a large ornate **gate/door** in the center background — locked with a giant padlock. Text above reads "PREMIUM ACCESS" in gold pixel font.
- **Mid layer:** Stone pillars on left and right, a velvet rope barrier in the foreground
- **Near layer:** A bouncer silhouette (still pixel art) on the far right — static decoration
- **Floor:** Red-and-gold checkered marble
- **Colors:** Deep crimson `#4A0010`, gold `#FFD700`, marble white `#F5F0E8`
- **Ambient effect:** Coin/sparkle particles drift upward near the gate (gold 2px dots, slow float)
- **Stage interaction:** If the player wins a round, the gate cracks slightly (visual state change — crack added to the gate sprite). Three cracks → gate breaks on match win with a shatter particle burst.
### Stage 5 — The AI Lab
**Opponent:** Aug X Labs (Augie)

- **Backdrop:** A glowing AI research laboratory. Circuit board pattern on the back wall with flowing yellow energy traces
- **Mid layer:** Holographic AI model visualizations (abstract geometric shapes, slowly rotating)
- **Near layer:** Lab workstations with screens showing code streams, an "AUGIE v2.0" logo on the wall
- **Floor:** White laboratory floor with yellow warning lines at each stage edge
- **Colors:** White `#F0F0F0`, gold `#FFD700`, circuit trace orange `#FF6B00`
- **Ambient effect:** Spark particles — brief bright flashes (2px, 8-frame lifetime) appear randomly across the mid-layer at low frequency (one every ~2 seconds)
- **Stage interaction:** When Aug X Labs activates their Super, the entire background briefly goes to a white scanline pattern for 8 frames (electric overload effect)
### Stage 6 — The Data Grid
**Opponent:** Quantum Path

- **Backdrop:** An abstract digital space — infinite grid receding into the horizon (perspective grid drawn in neon green on black, like The Matrix)
- **Mid layer:** Floating data cubes slowly rotating and drifting across the background
- **Near layer:** Ground-level green particle trails from each cube's path
- **Floor:** Flat black floor with a neon green grid overlay
- **Colors:** Black `#000000`, matrix green `#00FF44`, deep green `#003300`
- **Ambient effect:** Matrix digit rain — columns of falling green characters (0/1 pixel text), sparse, slow
- **Stage interaction:** When Quantum Path activates invisibility super, the entire background **inverts colors** for the duration
### Stage 7 — Mirror Stage
**Opponent:** (displaced character — see fight order)

- **Backdrop:** A plain reflective silver void — the character's own sprite is reflected upside-down in the "floor" surface (mirror image)
- **Mid layer:** Floating silver/chrome cubes spinning slowly
- **Near layer:** None — minimalist aesthetic
- **Floor:** Mirror-finish silver surface — characters' feet show subtle reflection
- **Colors:** Silver `#C0C0C0`, white `#FFFFFF`, shadow grey `#404040`
- **Ambient effect:** Slow sparkle twinkles (star-like, 1px, random positions, 8-frame fade)
- **Stage note:** Eerie and minimal — signals the game is building toward something
### Stage 8 — The Globe Arena (Boss Stage)
**Opponent:** HELLO (Final Boss)

- **Backdrop:** The Earth from orbit — a large curved horizon visible in the upper portion of the canvas, blue-white globe edge against black space. Stars in the deep background.
- **Mid layer:** Satellite silhouettes slowly drifting. A faint aurora borealis shimmer in green/teal.
- **Near layer:** The "arena floor" is the curved surface of the Earth itself — a stone-grey curved platform
- **Floor:** Dark grey curved surface, with faint continent outlines visible
- **Colors:** Space black `#000010`, ocean blue `#1A6EBD`, atmosphere teal `#00FFCC`, star white `#FFFFFF`
- **Ambient effect:** Stars twinkle slowly (random blinks, ~30 stars). Slow aurora wave animation in upper 40px of canvas.
- **Stage interaction:** Each time HELLO takes significant damage (every 25% health lost), the Earth in the background **cracks** — a pixel-art crack line added to the globe horizon. At 0 health, the globe explodes (see Boss Fight section).
- **Camera behavior:** Camera does NOT pan on this stage — both characters are locked to a fixed-width arena (480px). This is intentional — the boss arena feels "contained."
### Environmental Interactivity Summary
## Feature All Stages Specific Stage Stage boundary walls ✓ — Parallax scroll ✓ — Ambient particles ✓ — Hit-reactive background ✓ (flicker) See per-stage notes Destructible elements — Paywall Plaza (gate), Globe Arena (earth cracks) Color inversion — Data Grid (on Quantum super) Camera lock — Globe Arena only HUD & Health System
## Feature All Stages Specific Stage Stage boundary walls ✓ — Parallax scroll ✓ — Ambient particles ✓ — Hit-reactive background ✓ (flicker) See per-stage notes Destructible elements — Paywall Plaza (gate), Globe Arena (earth cracks) Color inversion — Data Grid (on Quantum super) Camera lock — Globe Arena only HUD & Health System
### HUD Layout Overview
The HUD is drawn on **Layer 6** — always on top of all game elements. It occupies the **top 30px and bottom 20px** of the 480×270 canvas. The HUD does NOT obscure the fight area.

```
┌────────────────────────────────────────────────────────────────┐
│ [P1 PORTRAIT] [████████████████████░░] P1   TIMER   P2 [░░████████████████████] [P2 PORTRAIT]  │
│              [▓▓▓▓▓▓▓▓▓▒▒▒▒▒▒▒▒▒▒▒▒]                [▒▒▒▒▒▒▒▒▒▓▓▓▓▓▓▓▓▓▓▓▓▓]               │
│              SUPER METER                               SUPER METER                              │
│                                                                │
│  [─────────────── FIGHT AREA ──────────────────]            │
│                                                                │
│  [ROUND 1]  [WIN ●] [WIN ○] [WIN ○]           [1x HIT]     │ ← Bottom strip
└────────────────────────────────────────────────────────────────┘

```
### Health Bars
**Position:**

- P1 health bar: Top-left, starts at x=50, y=8, extends **rightward** toward center
- P2 health bar: Top-right, starts at x=430, y=8, extends **leftward** toward center
- Each bar is **160px wide × 10px tall**
- Both bars are **center-anchored** — they shrink from the outside edge toward center (inward drain)
- **Health Bar Visual Layers (drawn back to front):**
- **Background rail:** Dark grey `#333333`, full bar width, rounded ends
- **Ghost bar:** Yellow `#FFFF00`, lags behind real health by 0.5s then drains slowly over 1s — classic SF2 "ghost" effect
- **Current health bar:** Color shifts based on remaining percentage:
- 50% HP: Green `#44CC44`- 25–50% HP: Yellow `#FFCC00`
- <25% HP: Red `#FF2222` + **pulsing animation** (brightness oscillates at 4Hz)
- **Bar border:** 1px dark outline `#000000`
- **Health Values:**
- Standard character: **100 HP**
- HELLO (boss): **300 HP** (3× bar — displayed with a larger bar and a `×3` glyph)
- Chip damage (from blocking): Damages real health only, NOT ghost bar
- Health does NOT regenerate between rounds within a match (carries over to next round)
- Health IS fully restored at the start of each new match (new opponent)
### Round Win Indicators
Below each health bar, **3 small circles** (6px diameter) indicate rounds won:

- Empty round: Hollow white circle `○` outline
- Won round: Filled gold circle `●`
- Active round: Pulsing white circle
- These track wins within the current match (best of 3).
### Timer
- Displayed at the **top center** of HUD: Large pixel font, two digits (e.g., `90`)
- **Starting time:** 90 seconds per round
- **Font:** Big pixel font, white with 1px black outline
- **Timer behavior:**
- Counts down in real time
- Below 10 seconds: Timer text turns **red** and pulses
- At 0: Round ends — character with more HP wins the round (TIME OUT)
- If HP is equal at timeout: **DRAW** — both characters lose the round (no winner circle added)
- Timer **pauses** during: knockdown animation, win/lose screen, super activation freeze
### Super Meter Bar
Below each health bar (y=22, same x alignment):

- Each bar is **140px wide × 5px tall**
- **Color:** Yellow `#FFD700` fill on dark grey rail `#222222`
- **When full:** Bar glows (subtle white border animation) and the character's name text flashes gold
- **Label:** Tiny `SUPER` text (4pt pixel font) to the left of P1's bar, right of P2's bar
### Character Name Display
- Small pixel text (6pt) above each health bar showing the character's name
- P1 name: Left-aligned under health bar
- P2 name: Right-aligned under health bar
- Flash white on round start (1 second), then return to white (default)
### Round Announcement Text
Large centered text overlaid on screen during key moments:

Text Trigger Font Size Color Duration `ROUND 1` / `ROUND 2` / `ROUND 3` Round start 24px White + shadow 60 frames hold, then scale-out `FIGHT!` After "ROUND X" text exits 28px Yellow 40 frames, scale-in then out `KO!` On a character reaching 0 HP from a normal hit 32px Red 80 frames hold `K.O.!` On a character reaching 0 HP from a Super move 36px Red + gold flash 80 frames, flash effect `PERFECT!` Round won without taking any damage 24px Gold 80 frames `TIME OUT` Timer reaches 0 24px Orange 60 frames `DRAW` Timeout with equal HP 24px White 60 frames `YOU WIN!` Player wins the match 28px Yellow held until input `YOU LOSE` Player loses the match 28px Red 80 frames, then Game Over All announcement texts use a **scale-in** (starts at 50% size → 100%, over 10 frames) with a brief screen flash on KO/Perfect.

### Combo Counter Display
When a combo is active (2+ consecutive hits):

- Displayed at: Center-bottom of the fight area (y=200), slightly toward the defender
- Format: `4x HIT` or `8x COMBO` (switches at 6+ hits)
- **Font:** 14px pixel font, yellow `#FFD700` with black shadow
- **Scale animation:** Each increment causes a quick pop (scale to 130% → back to 100%, 6 frames)
- **Color escalation:**
- 2–4 hits: Yellow `#FFD700`
- 5–8 hits: Orange `#FF8800`
- 9+ hits: Red `#FF2200` + outline glow
### Damage Numbers (Optional Flourish)
When a hit lands, a small floating damage number rises from the hit point:

- Format: `-12` (red for damage dealt to P1, blue for P2)
- Rises 20px over 30 frames, fades out
- Font: 8px pixel font
- Does NOT display for chip damage (too noisy)
### Health System Rules Summary
## Rule Value Starting HP (standard) 100 Starting HP (HELLO boss) 300 Min HP 0 (death) Chip damage rate 10% of move's base damage HP carries over between rounds Yes (within a match) HP resets between matches Yes (new opponent) Super meter carries between rounds Yes Super meter resets between matches Yes (to 0) KO threshold HP ≤ 0 Timeout win condition Higher HP at 0:00 Game States & Flow
## Rule Value Starting HP (standard) 100 Starting HP (HELLO boss) 300 Min HP 0 (death) Chip damage rate 10% of move's base damage HP carries over between rounds Yes (within a match) HP resets between matches Yes (new opponent) Super meter carries between rounds Yes Super meter resets between matches Yes (to 0) KO threshold HP ≤ 0 Timeout win condition Higher HP at 0:00 Game States & Flow
## Audio System
All audio is **generated entirely via the Web Audio API** — no audio files, no external assets. Everything is synthesized using oscillators, gain nodes, filters, and noise buffers inline in JavaScript. This is a hard constraint for the single-file delivery requirement.

### Audio Architecture
```
// Single shared AudioContext — created once on first user interaction
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

// Master gain node — all sounds route through this
const masterGain = audioCtx.createGain();
masterGain.gain.value = 0.6;
masterGain.connect(audioCtx.destination);

```
**Two audio channels:**

- **Music channel** — looping background chiptune tracks (lower gain, ~0.4)
- **SFX channel** — one-shot sound effects (higher gain, ~0.8), polyphonic (multiple can overlap)
Note: `AudioContext` must be created or resumed inside a user gesture handler (click/keypress) to comply with browser autoplay policy. The game should resume the context on the first `keydown` event.### Music Tracks (Per Screen / Stage)
Each track is a **procedurally generated chiptune sequence** — a looping array of `{ frequency, duration, waveType }` note objects played in sequence using `OscillatorNode`. Waveforms used: `square` (melody), `triangle` (bass), `sawtooth` (lead riff).

   Track Screen / Stage Style Tempo Key Notes    `track_title` Title Screen Mysterious, slow arpeggio 80 BPM Minor key, sparse; builds to loop   `track_select` Character Select Upbeat, punchy 140 BPM Major key, bouncy loop   `track_stage1` Broadcast Stage Rock/electric feel 160 BPM Driving beat, power chords   `track_stage2` Ad Network Alley Synthwave, neon 130 BPM Minor synth lead, pulsing bass   `track_stage3` Stream Vault Industrial, tense 150 BPM Heavy square wave, staccato   `track_stage4` Paywall Plaza Regal, pompous 120 BPM Fanfare-style, major key   `track_stage5` AI Lab Glitchy, fast 170 BPM Arpeggiated, odd time feel   `track_stage6` Data Grid Matrix-like, eerie 110 BPM Minor, sparse, digital bleeps   `track_stage7` Mirror Stage Unsettling, reversed feel 90 BPM Chromatic, dissonant   `track_boss` Globe Arena (HELLO) Epic, urgent 180 BPM Full arrangement, driving; most complex   `track_victory` Victory screen Short triumphant jingle — 4-bar fanfare, plays once   `track_gameover` Game Over Descending sad phrase — 3-note descend, plays once   `track_ending` Ending sequence Triumphant, building — Builds from single note to full chord  **Music implementation pattern:**

```
function playTrack(notes, loop = true) {
  // notes = [{freq, dur, wave}, ...]
  // Schedule each note using audioCtx.currentTime offsets
  // On last note: if loop, reschedule from start
  // Returns a stop() handle to cancel the loop
}

```
Music **fades out** (gain ramp over 0.5s) when transitioning between screens.

### Sound Effects (SFX) Reference
All SFX are short synthesized bursts. Implementation uses `OscillatorNode` + `GainNode` with an envelope (attack + decay).

###    SFX ID Trigger Wave Freq Duration Notes    `sfx_punch_light` Light punch lands `square` 280Hz → 180Hz 80ms Freq sweep down   `sfx_punch_heavy` Heavy punch lands `square` 180Hz → 80Hz 140ms Lower, heavier sweep   `sfx_kick_light` Light kick lands `sawtooth` 320Hz → 200Hz 90ms Slightly brighter than punch   `sfx_kick_heavy` Heavy kick lands `sawtooth` 200Hz → 100Hz 160ms Deep thud quality   `sfx_block` Blocking a hit `square` 440Hz 60ms Flat tone, no sweep; metallic   `sfx_whiff` Attack misses (air) `sine` 600Hz → 400Hz 50ms Soft whoosh   `sfx_jump` Character leaves ground `triangle` 300Hz → 500Hz 100ms Short ascending blip   `sfx_land` Character lands `square` 150Hz 40ms Short flat low thud   `sfx_fireball_launch` Projectile fired `sawtooth` 500Hz → 300Hz 120ms Descending buzz   `sfx_fireball_hit` Projectile hits opponent `square` 350Hz → 150Hz 100ms Impact crunch   `sfx_special_activate` Special move triggers `sawtooth` 200Hz → 800Hz 200ms Ascending power swell   `sfx_super_activate` Super move triggers Combined — 400ms Chord: 200+400+600Hz simultaneously, then silence   `sfx_ko` KO landing hit Combined — 300ms `sfx_punch_heavy` + low rumble (40Hz noise burst)   `sfx_round_start` "FIGHT!" text `square` 660Hz 80ms Sharp start sting   `sfx_cursor_move` Select screen navigation `square` 220Hz 40ms Short beep   `sfx_cursor_confirm` Character confirmed `triangle` 440Hz → 660Hz 120ms Two-note ascending   `sfx_cursor_error` Attempting to select `???` `square` 150Hz 200ms Flat low buzz   `sfx_timer_low` Timer ≤ 10 seconds `square` 880Hz 80ms Plays on each second tick   `sfx_hello_tease` HELLO tease flash (fights 4–7) `sine` 80Hz → 40Hz 500ms Deep descending rumble   `sfx_parry` Successful parry `triangle` 880Hz → 1200Hz 80ms Bright sharp ting   `sfx_throw` Throw connects `square` 200Hz → 100Hz 180ms Slow heavy impact   `sfx_combo_increment` Combo counter increases `triangle` scales with count 30ms Freq = 220 + (comboCount × 40)Hz — escalates  Noise Generation (for rumble/explosion effects)
For the globe explosion and KO rumble, use **white noise** generated via an `AudioBuffer` filled with random values:

```
function createNoiseBuffer(duration) {
  const bufferSize = audioCtx.sampleRate * duration;
  const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
  const data = buffer.getChannelData(0);
  for (let i = 0; i < bufferSize; i++) {
    data[i] = Math.random() * 2 - 1;
  }
  return buffer;
}

```
Apply a **lowpass filter** (`BiquadFilterNode`, frequency ~200Hz) to turn white noise into a low rumble.

### Audio Volume Controls
No in-game volume UI is required. Default levels:

- Master gain: `0.6`
- Music gain: `0.4` (relative to master)
- SFX gain: `0.8` (relative to master)
These constants should be defined at the top of the JS and easily tuneable.

## Boss Fight & Narrative
### Narrative Thread: Teasing HELLO
HELLO is not introduced at the start — he is seeded throughout the gauntlet through environmental and audio cues. The player should feel a building unease before the reveal.

Tease Schedule###    Fight # Tease Event Mechanic    1–3 None No tease — clean arcade fights   4 (InPlayer) Between rounds: the stage background **shudders** for 3 frames. A **dark globe silhouette** (barely visible, 10% opacity) looms in the top-center of the screen for exactly 2 frames. Background flicker + overlay draw   5 (Aug X Labs) After the VS screen loads, a single **deep bass rumble** plays (`sfx_hello_tease`) with no visual explanation. Audio only   6 (Quantum Path) On the opponent's **win screen** (if they win a round), the background flickers and "H E L L O" briefly appears in the background in large faded letters (5% opacity, white) for 4 frames, then vanishes. If the player wins all rounds cleanly, it still flickers once during the stage fade. Text overlay, subliminal   7 (Mirror fight) At the **match end screen** (regardless of winner), the victory animation cuts out 1 second early. The screen goes black for 0.5s. A loud `sfx_hello_tease` plays. Then, for 1.5 seconds: the full **HELLO sprite** appears centered on screen, scaled 2×, rotating slowly, with a red tint. It then cuts to a distorted static screen for 4 frames, then the BOSS_INTRO cinematic begins. Full reveal cutscene  BOSS_INTRO Cinematic (State: `BOSS_INTRO`)
Duration: ~5 seconds. Input is fully disabled. This plays as a non-interactive cutscene drawn on canvas.

**Sequence:**

- **(0.0s)** Black screen. The cursor `>` appears in the center of the screen, blinking.
- **(0.5s)** The text `> INITIALIZING...` types out one character at a time (typewriter SFX: `sfx_cursor_move` at 80ms intervals).
- **(1.2s)** Text clears. The Globe Arena background fades in slowly (1s ease).
- **(2.2s)** HELLO drops from the top of the screen into position — oversized, globe rotating. As he lands: `sfx_throw` plays + screen shakes (±3px for 10 frames).
- **(3.0s)** HELLO raises both arms slowly. The word "HELLO" on his globe glows white.
- **(3.8s)** Text appears below him in large pixel font: `**H E L L O**` — each letter appears one at a time with a deep bass note (`sfx_hello_tease` slowed).
- **(4.5s)** Screen flash white (2 frames). HELLO shrinks to his normal combat position on the right side of the arena.
- **(5.0s)** "ROUND 1 / FIGHT!" sequence plays normally. `track_boss` begins.
### HELLO — Boss Combat Specification
Stats- **HP:** 300 (3× standard)
- **Speed:** Moderate (same walk speed as standard characters)
- **HUD:** HELLO's health bar is **wider** than standard (240px instead of 160px) with a `×3` label. Uses the same color-shift and ghost-bar mechanics.
- **Size:** HELLO's sprite is **~96×96 px** — larger hitbox, larger hurtbox. Arms extend further.
HELLO's Unique Move SetHELLO does NOT use the standard special move inputs. His moves are defined as follows:

   Move Input (AI-driven) Description Damage Notes    **Globe Slam** Overhead leap Jumps straight up, comes down fist-first. Unblockable if opponent is directly below on landing. 22 8-frame startup, massive knockback   **Hello Wave** Projectile Fires a slow, LARGE projectile (32×16 px wave-shaped, green/white). Travels full screen width. 15 Slower than standard fireballs; takes up more vertical space   **Seismic Stomp** Low attack Stomps the ground — a shockwave travels along the floor to the stage boundary. Hits low, cannot be blocked standing. 18 Crouching block or jump to avoid   **Orbital Grab** Proximity throw If the player is within 48px, grabs and spins them around his body (360° arc, 3 hits), throws them across screen. 35 total Unblockable, 10f startup   **World Spin** Super Spins in place at high speed for 2 seconds — hitbox active entire duration, drags opponent in. Costs no meter (boss has unlimited super). 8/hit (~10 hits max) Activated when HELLO HP < 50%  HELLO's AI PhasesHELLO operates in **2 distinct phases** based on his remaining HP:

**Phase 1 (HP 300–151): "Greeting"**

- Moves at normal speed
- Uses Hello Wave projectiles frequently (~every 3s)
- Occasionally Seismic Stomps when player is mid-range
- Reacts to player jumps with Globe Slam
- AI aggression: moderate
**Phase 2 (HP 150–0): "Hostile Takeover"**

- Moves ~25% faster
- Background: Earth in the backdrop begins **cracking** (visual state — add crack lines every 50 HP lost in this phase)
- `track_boss` pitch-shifts up by one semitone (Web Audio API: `playbackRate` on the source — [PROPOSED - NEEDS VALIDATION: Web Audio API `AudioBufferSourceNode.playbackRate` works for buffer sources; for procedurally scheduled oscillators, this requires retuning individual oscillator frequencies instead])
- Activates World Spin when HP first drops below 50% (one-time trigger)
- Uses Orbital Grab more aggressively (~every 4s if in range)
- AI aggression: high
### HELLO Death Sequence & Ending
Triggered when HELLO's HP reaches 0.

**Sequence:**

- **(Frame 0)** Final hit lands. Normal `sfx_ko` plays. HELLO freezes in place.
- **(0.1s)** Screen flash white (3 frames).
- **(0.3s)** HELLO begins a **crack animation** — pixel-art crack lines radiate outward from his body over 30 frames. The globe rotation accelerates to max speed.
- **(0.8s)** The Globe Arena background Earth fully shatters (all 4 crack lines converge).
- **(1.0s)** **EXPLOSION:** 80–120 particles burst outward from HELLO's center position. Particle types:
- 40% large chunks (8×8 px blue/green globe fragments)
- 40% small sparks (2×2 px white/yellow)
- 20% smoke puffs (8×8 px grey, slow drift)
- All particles have randomized velocity vectors (speed 80–400 px/s), gravity applies
- Particles fade over 1.5s
- `createNoiseBuffer(0.6)` low-pass noise burst plays at full gain (explosion rumble)
- **(1.5s)** Particles still drifting. Screen fades to black over 1 second.
- **(2.5s)** Black screen. Cursor `>` appears, bottom-left. `track_ending` begins (soft, building).
- **(2.6s–4.6s)** Text types out character by character, terminal-green `#00FF44` on black, monospace pixel font:
```
> SYSTEM ONLINE
> RUNNING HELLO_WORLD.EXE
> ...
> HELLO WORLD

```
- Each line types at ~60ms per character. Pause 0.3s between lines.
- **(4.6s)** `> HELLO WORLD` line completes. The cursor blinks 3×. The text glows brighter.
- **(5.0s)** The JWX logo (player's character's logo) appears in the top-right corner, small, with `POWERED BY JWXAIPOC` text beneath it. `track_ending` swells to full volume.
- **(6.5s)** `PLAY AGAIN? [ENTER]` prompt fades in. Waiting for input.
### Villain Motivation (Flavor Text — Optional)
If implementing a between-fight interstitial (text overlay, 2s display before VS screen), use the following one-liners. These are displayed as white-on-black pixel text, like classic arcade flavor text:

##    Fight Flavor Text    Before fight 1 `"The gauntlet begins. Your rivals await."`   Before fight 4 `"Something stirs beyond the network..."`   Before fight 6 `"The data paths converge. Something is watching."`   Before fight 7 `"One last echo before the storm."`   Before boss *(replaced by BOSS_INTRO cinematic — no text)*  AI Opponent Behavior
All CPU opponents are driven by a **single AI system** with per-character **behavior profiles** that tune the weights and thresholds. There is no machine learning — the AI is a deterministic decision tree with randomized timing to simulate human-like hesitation and imperfection.

### AI Update Rate
The AI evaluates its next action **every 6–18 frames** (randomized per evaluation cycle). This prevents the AI from being frame-perfect and creates a believable reaction window. Formula:

```
aiThinkInterval = Math.floor(6 + Math.random() * 12); // 6–18 frames

```
The AI does NOT re-evaluate mid-action. Once an action is committed (e.g., jumping, attacking), it plays out before the next decision is made.

### AI Decision Tree
Each AI evaluation cycle runs the following priority-ordered checks:

```
1. DANGER CHECK (highest priority)
   └─ If HP < 25% AND opponent HP > 50%:
       → Activate DEFENSIVE mode (block more, jump back, use Super if available)

2. SUPER CHECK
   └─ If Super meter = 100% AND opponent is within 150px:
       → 60% chance: USE SUPER
       → 40% chance: defer (don't telegraph)

3. PROJECTILE REACTION
   └─ If an opponent projectile is active AND approaching:
       → If close (<80px): JUMP over it
       → If mid-range (80–180px): Fire own projectile to cancel, OR jump
       → If far (>180px): 50% chance jump, 50% chance walk forward

4. OPPONENT IN AIR
   └─ If opponent is jumping:
       → If jumping toward AI: attempt anti-air (Rising Uppercut), 40% trigger rate
       → If jumping away: walk forward, wait

5. CLOSE RANGE (gap < 80px)
   └─ Priority order:
       a. 30% chance: THROW (if not in stun)
       b. 40% chance: LIGHT ATTACK combo (LP → HP cancel)
       c. 20% chance: SPECIAL MOVE (Rising Uppercut or Spinning Kick)
       d. 10% chance: BLOCK and wait

6. MID RANGE (gap 80–200px)
   └─ Priority order:
       a. 35% chance: WALK FORWARD
       b. 30% chance: FIREBALL projectile
       c. 20% chance: DASH FORWARD
       d. 15% chance: JUMP FORWARD (offensive jump-in)

7. FAR RANGE (gap > 200px)
   └─ Priority order:
       a. 50% chance: WALK FORWARD
       b. 30% chance: FIREBALL
       c. 20% chance: IDLE (brief hesitation, 10–20 frames)

```
### Difficulty Scaling (Gauntlet Progression)
CPU difficulty increases across the 8 fights. Each fight number maps to a **difficulty multiplier** applied to the AI's decision weights and reaction times.

   Fight # Opponent Difficulty AI Think Interval Aggression Block Rate    1 JW Player Easy 14–18f Low (40%) 15%   2 Connatix Easy-Med 12–18f Low-Med (50%) 20%   3 VUALTO Medium 10–16f Med (55%) 25%   4 InPlayer Medium 10–14f Med (60%) 35%   5 Aug X Labs Med-Hard 8–14f Med-High (65%) 25%   6 Quantum Path Hard 7–12f High (70%) 30%   7 Mirror Hard 6–12f High (75%) 30%   8 HELLO (Boss) Very Hard 6–10f Very High (85%) 40%  **Aggression %**: Probability that when in mid/close range, the AI chooses an offensive action (attack/dash) over defensive/neutral (block/idle/back-step).

**Block Rate**: Base probability per evaluation cycle that the AI enters a blocking stance when the player is attacking in range.

### Per-Character Behavior Profiles
Each character has a **behavior profile** that biases their AI toward their archetype. These are additive modifiers on top of the base decision tree weights:

###    Character Profile Key Biases    JW Player Rushdown +20% dash forward, +15% light combo, −15% projectile use   Connatix Zoner +30% fireball, −20% close attack, +10% jump back   VUALTO Grappler +25% throw attempt (close), +15% walk forward, −20% fireball   InPlayer Defensive +20% block rate, +15% counter-attack (after blocking), −15% aggression   Aug X Labs Wild Card All weights randomized ±15% each evaluation cycle (intentionally erratic)   Quantum Path Technical +15% special cancel use, +10% parry attempt, −10% random idle   HELLO (Boss) Boss Uses unique move set (see Boss Fight section); ignores standard decision tree; uses Phase 1/2 behavior  HELLO AI (Boss-Specific)
HELLO does not use the standard decision tree. His AI runs a **separate boss behavior loop**:

```
HELLO AI (evaluates every 8–12 frames in Phase 1, 6–8 frames in Phase 2):

1. If player is airborne:
   → 50% chance: Globe Slam (if HELLO is beneath player's projected landing spot)
   → 50% chance: Hello Wave projectile

2. If player is close (<70px):
   → 40% chance: Orbital Grab
   → 35% chance: Globe Slam
   → 25% chance: Light attack combo

3. If player is mid-range (70–200px):
   → 40% chance: Hello Wave
   → 30% chance: Seismic Stomp
   → 20% chance: Walk forward
   → 10% chance: Dash forward

4. If player is far (>200px):
   → 60% chance: Hello Wave
   → 40% chance: Walk forward

5. World Spin: Triggered ONCE when HP drops below 150 (50%). 
   Not re-activated.

6. Phase 2 modifier (HP < 150):
   → All evaluation intervals reduced by 2 frames
   → Orbital Grab weight +15% in close range
   → Hello Wave frequency increases (fires on 55% of mid/far decisions)

```
### Anti-Cheese Measures
To prevent trivially exploitable AI patterns:

- **Jump spam counter:** If the player has jumped 3+ times in the last 10 seconds, the AI's anti-air trigger rate increases to 70% for the next 20 seconds.
- **Fireball spam counter:** If the player fires 3+ projectiles without moving, the AI switches to a "rush mode" for 5 seconds — ignoring fireballs and dashing/jumping aggressively forward.
- **Corner trap awareness:** If the AI is in the corner (within 60px of boundary), it increases jump-back frequency by 40% to attempt to escape.
- **Throw-loop prevention:** The AI cannot attempt a throw within 90 frames of its last throw attempt (regardless of success), preventing infinite throw loops.
### AI Blocking Rules
The AI blocks **reactively**, not predictively:

- Block triggers when an opponent attack animation enters its **active frames** AND the AI is within 150px
- Block is held for the duration of the attack animation + 4 additional frames (delayed release — simulates human reaction lag)
- The AI will NOT block if currently in a special move animation, jumping, or in knockdown
- Parry attempt: 10% chance (base) to attempt a parry instead of a standard block when an attack is incoming — this increases to 20% for Quantum Path
## Implementation Notes for Claude
This section is addressed **directly to the AI coding agent** (Claude) that will implement this game. Read this entire document before writing a single line of code.

### Prime Directive
Deliver a **single **`**index.html**`** file** that, when opened in a modern browser, runs the complete game described in this specification. No build step. No npm. No CDN links. No external files. The file must be entirely self-contained.

### Before You Write Code: Read the Whole Spec
Do not start coding section by section. Read the entire document, build a mental model of:

- The game state machine (Game States & Flow)
- The physics constants (Game Engine)
- The character data structure (Character Roster)
- The audio architecture (Audio System)
Then plan your **data structures first**, code second.

### Recommended Code Structure (Inside `<script>` tag)
```
index.html
└── <script>
    ├── CONSTANTS  (canvas size, physics, colors, timing)
    ├── AUDIO      (AudioContext setup, SFX functions, music sequencer)
    ├── CHARACTERS (data definitions for all 8 fighters + HELLO)
    ├── STAGES     (data definitions for all 8 stages)
    ├── INPUT      (keyboard state tracking, input buffer)
    ├── ENTITIES
    │   ├── Fighter class (state machine, physics, animation, draw)
    │   └── Projectile class (position, velocity, hitbox, draw)
    ├── PARTICLES  (particle system: burst, trail, smoke)
    ├── AI         (decision tree, behavior profiles)
    ├── HUD        (draw functions for all HUD elements)
    ├── SCREENS
    │   ├── drawTitleScreen()
    │   ├── drawCharacterSelect()
    │   ├── drawVSScreen()
    │   └── drawEndingScreen()
    ├── GAME STATE MACHINE (top-level state + transitions)
    └── GAME LOOP  (requestAnimationFrame entry point)

```
### Critical Implementation Notes
1. Single Canvas, Multiple LayersDraw everything to one canvas each frame. Clear with `ctx.clearRect(0, 0, W, H)` at the top of every render call. Draw order: background layers → characters → particles → HUD. Never use multiple canvases.

2. Character Sprites Are Procedural — No ImagesEvery character must be drawn using `ctx.fillRect`, `ctx.arc`, `ctx.fillText`, `ctx.bezierCurveTo`, etc. Design each character's `draw(ctx, x, y, facingRight, state, animFrame)` function to accept an animation frame parameter (0–59 for a 60-frame cycle) and interpolate arm/leg positions using `Math.sin(animFrame * Math.PI / 30)` for the float animation.

**Floating limb implementation:**

```
// Arms: offset from body center using sin wave
const armBob = Math.sin(animFrame * 0.2) * 3;
// Left arm (always floats slightly above body center)
ctx.fillRect(x - bodyWidth/2 - 10 + armBob, y - 10, 8, 16);
// Right arm
ctx.fillRect(x + bodyWidth/2 + 2 - armBob, y - 10, 8, 16);
// Legs: opposite phase
const legBob = Math.cos(animFrame * 0.2) * 3;
ctx.fillRect(x - 10, y + bodyHeight + legBob, 8, 14);
ctx.fillRect(x + 2, y + bodyHeight - legBob, 8, 14);

```
3. The Input Buffer is Non-NegotiableSpecial move detection REQUIRES the 16-frame input buffer. Do not skip this. Without it, QCF motions will not register reliably. Store inputs as `{key, frame}` pairs and scan backward from current frame.

4. AudioContext Autoplay PolicyThe `AudioContext` will be in `suspended` state until a user gesture. On the first `keydown` event, call `audioCtx.resume()`. Wrap all audio calls in a check: `if (audioCtx.state === 'running')`.

5. Hit Detection TimingHitboxes are only active during specific frame windows of attack animations. Use the frame data tables in the Combat System section. Do not use continuous hitbox detection — check `currentFrame >= startupFrames && currentFrame < startupFrames + activeFrames`.

6. The Ghost Health BarThe ghost bar (yellow, lags behind real HP) requires storing two values: `currentHP` and `displayedHP`. `displayedHP` updates at a slower rate (lerp toward `currentHP` at ~0.02/frame after a 0.5s delay).

7. Canvas ScalingThe logical canvas is 480×270. Scale it to fill the browser window while maintaining aspect ratio:

```
function resizeCanvas() {
  const scaleX = window.innerWidth / 480;
  const scaleY = window.innerHeight / 270;
  const scale = Math.min(scaleX, scaleY);
  canvas.style.width = (480 * scale) + 'px';
  canvas.style.height = (270 * scale) + 'px';
}
window.addEventListener('resize', resizeCanvas);
resizeCanvas();

```
8. Font RenderingUse a pixel-art-style font. Since no external fonts are allowed, use `ctx.font = 'bold Xpx monospace'` for all text. Monospace approximates pixel font well enough. For the title screen and round announcements, use larger sizes (24–36px).

9. Music Sequencer PatternImplement a simple note sequencer that schedules Web Audio API notes ahead of time using `audioCtx.currentTime`:

```
function scheduleNote(freq, startTime, duration, wave = 'square') {
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.type = wave;
  osc.frequency.value = freq;
  gain.gain.setValueAtTime(0.3, startTime);
  gain.gain.exponentialRampToValueAtTime(0.001, startTime + duration);
  osc.connect(gain);
  gain.connect(musicGain);
  osc.start(startTime);
  osc.stop(startTime + duration + 0.05);
}

```
Schedule notes 1–2 bars ahead of playhead. Reschedule on loop.

10. HELLO's Health BarHELLO's 300 HP requires special HUD treatment. Render his health bar as the standard width (160px) but with a `×3` indicator, OR scale his bar to 240px. Either approach is acceptable — just ensure it's visually clear he has more HP than standard fighters.

11. Particle SystemKeep particles simple: an array of `{x, y, vx, vy, life, maxLife, size, color}` objects. Update each frame: apply gravity to `vy`, add velocity to position, decrement `life`. Remove dead particles. Draw as `ctx.fillRect` or `ctx.arc`. Cap total particles at **200** at any time to avoid performance issues.

12. State TransitionsUse a single `gameState` string variable and a `setState(newState)` function that handles cleanup (clear particles, stop music, reset timer) before entering the new state. Do NOT scatter state change logic across multiple places.

### Known Complexity Areas (Plan Carefully)
###    Area Risk Mitigation    Input buffer + special move detection High — easy to get wrong Build and test this in isolation first   Physics + character collision (push-apart) Medium — edge cases at walls Test corner cases: both at left wall, simultaneous wall push   Music sequencer timing drift Medium — Web Audio scheduling can drift Use `audioCtx.currentTime` exclusively, never `setTimeout` for audio   Combo counter timing Low-Medium Track `lastHitFrame`, compare to `currentFrame`   HELLO boss phases + unique moves Medium Isolate boss AI as a completely separate code path   Canvas scaling on resize Low Use CSS transform only, never change canvas width/height attribute  Out of Scope (Do Not Add)
- Multiplayer (2-player keyboard) — single player vs CPU only
- Mobile/touch controls — keyboard only
- Save state / high score persistence — no localStorage needed
- Network features of any kind
- Settings menu or volume controls
- Character unlock progression
- Any external API calls
### Definition of Done
The game is complete when:

-  Title screen displays with animated stars and hidden HELLO silhouette
-  Character select screen shows all 7 selectable characters + locked `???` slot
-  All 8 fights play through (7 gauntlet + 1 boss)
-  All 4 base moves (LP, HP, LK, HK) + 3 specials functional per character
-  Super moves functional for all 7 characters
-  Health bars with ghost effect display correctly
-  Super meter fills and depletes correctly
-  Timer counts down; timeout logic works
-  All 8 stages have distinct visual backgrounds with parallax
-  All SFX trigger on correct game events
-  At least 6 of 13 music tracks are implemented (title, select, 4 stages, boss)
-  HELLO tease events fire on fights 4–7
-  BOSS_INTRO cinematic plays before fight 8
-  Ending sequence plays with `> HELLO WORLD` terminal text
-  Game Over screen with restart works
-  Debug mode (F1) shows hitboxes
-  File is a single `.html` file that opens directly in browser with no server required
## Game States & Flow
The game is driven by a top-level **state machine**. Only one state is active at a time. Transitions are explicit and driven by timers or player input.

```
TITLE_SCREEN
    │  (press Enter)
    ▼
CHARACTER_SELECT
    │  (confirm selection)
    ▼
VS_SCREEN  ──────────────────────────────────────────────────────────────┐
    │  (1.5s auto-advance)                                               │
    ▼                                                                    │
ROUND_INTRO  (display "ROUND X" + "FIGHT!")                             │
    │  (animation complete)                                              │
    ▼                                                                    │
FIGHTING  (main game loop runs here)                                     │
    │                                                                    │
    ├──► (HP ≤ 0 or timer = 0) ──► ROUND_END                           │
    │                                   │                               │
    │                        ┌──────────┴───────────┐                  │
    │                   (match not over)        (match over)            │
    │                        │                       │                  │
    │                   ROUND_INTRO              MATCH_END              │
    │                   (next round)                 │                  │
    │                                    ┌───────────┴──────────┐      │
    │                               (player won)          (player lost) │
    │                                    │                       │      │
    │                            NEXT_OPPONENT              GAME_OVER   │
    │                                    │                              │
    │                        (more opponents remain) ──────────────────►┘
    │                                    │
    │                        (all opponents beaten)
    │                                    │
    │                                    ▼
    │                            BOSS_INTRO  (special cinematic)
    │                                    │
    │                                FIGHTING  (boss fight)
    │                                    │
    │                            (boss defeated)
    │                                    │
    │                                    ▼
    └──────────────────────────────► ENDING

```
### State Descriptions
###    State Description    `TITLE_SCREEN` Animated title, star field, hidden HELLO silhouette. Waits for Enter.   `CHARACTER_SELECT` Grid UI, cursor navigation, portrait preview. Waits for confirm.   `VS_SCREEN` Shows P1 vs CPU character, stage name. Auto-advances after 1.5s.   `ROUND_INTRO` "ROUND X" → "FIGHT!" text overlay. Input disabled. ~2.5s total.   `FIGHTING` Active gameplay. Full input, physics, AI, collision all running.   `ROUND_END` KO / Time Out result shown. Winner pose animation. ~2s hold.   `MATCH_END` Match winner determined. Victory/defeat text shown. ~2s hold.   `NEXT_OPPONENT` Brief transition: stage fade-out → VS screen for next fighter.   `BOSS_INTRO` Special 3-second cinematic (see Boss Fight section). Input disabled.   `GAME_OVER` Player lost — "GAME OVER" screen, prompt to restart from beginning.   `ENDING` Globe explosion + `> HELLO WORLD` terminal text sequence.  Restart Behavior
- From `GAME_OVER`: Press Enter → returns to `TITLE_SCREEN` (full reset)
- From `ENDING`: After the payoff sequence completes (~6s), prompt appears: `PLAY AGAIN? [ENTER]` → returns to `TITLE_SCREEN`
- No save state or continue system — pure arcade style