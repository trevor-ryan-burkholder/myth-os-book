# Myth-OS: The Hold

## Browser-Based Dungeon Crawler. Full Specification.

Working title: Myth-OS: The Hold
Format: Browser game (HTML, JS/TS, Canvas via Phaser 3)
Genre: Roguelike-lite. Run-based. No combat in the traditional sense.
Target run length: 15 to 25 minutes
Player profiles: Newcomer (Apprentice mode), Reader (Adept mode)

---

## 0. Document Map

This spec runs in three parts.

Part 1 is a concept document. Read it to decide if the design holds together before going further.

Part 2 is the full game design document. It defines mechanics, systems, content, modes, and UI.

Part 3 is the prototype specification. It defines the tech stack, file structure, and MVP build phases.

An appendix at the end gives the Codex mapping table linking game-native names back to Myth-OS terms.

---

## Part 1. Concept Document

### 1.1 Pitch

The Hold is a short browser game. Players move through a layered inner space and meet figures who guard parts of themselves. They cannot attack. They cannot force entry. They have to sense what each figure protects, adjust their approach, and earn access through indirect interaction. Each run ends with one thing carried out into the player's real day.

The game teaches Myth-OS by enforcing its rules. Pressure does not win. Speed does not win. Reading the signal, holding range, and choosing the right approach wins.

### 1.2 Why a game teaches this better than reading alone

A book defines the rules. A game makes the player obey them.

When the player tries to force a figure, the figure's walls go up and the room locks. The player learns the rule by hitting it, not by being told. When the player pushes past their Ground meter, the run ends without payoff. The lesson lands because the consequence is immediate and small.

The game does not replace the book. It runs alongside it. A reader plays to practice. A newcomer plays first and reads to go deeper.

### 1.3 Core Loop

One room of play looks like this.

Enter a room. The Signal HUD shows ambient signal strength and a coarse direction. A figure waits in the room or adjacent to it.

Sense the room. Move slowly to read where the signal sharpens. Sudden movement raises the figure's walls.

Make contact. When the signal locks on, choose an Approach: Witness, Reflect, Offer, or Ask. Each approach affects the figure differently based on what they protect.

Read the response. The figure responds with a signal pattern. The player adjusts.

Hold range. The Ground meter drops if the player pushes, lingers too long in a charged room, or repeats a mismatched approach.

Move on. After a successful interaction, the figure either opens a door, offers a Token, or steps aside. The player moves deeper into the Hold.

Exit. After three to five rooms, the player reaches the Carry-Out altar. They choose one thing to take into the day ahead. The run ends.

### 1.4 Themes the Game Enforces

Five rules sit underneath every mechanic.

Resonance beats logic. The player has no stats sheet to read. Signal is felt through animation, sound, and the HUD's coarse readout. Reasoning out the answer fails. Reading the room works.

Indirect access beats force. There is no attack button. No skill check overcomes resistance. Force locks the room.

Structure enables interaction. Without the Signal HUD, Ground meter, and Approach menu, the figure stays unreachable. The interface is the access method.

Safety precedes access. Ground is the first resource the player learns to protect. If Ground breaks, the room closes and the player exits.

Internal work translates outward. Every run ends with a Carry-Out. Insight without translation does not count.

### 1.5 Sample Run, Apprentice Mode

A new player enters. The Onboarding overlay names the Signal HUD, the Ground meter, and the four Approaches. It points at the figure on screen and labels it: "Figure (book term: Presence)."

The player moves toward the figure. The Signal HUD pulses faster as they get closer. They pick Witness. The figure's outline softens. A door opens to the east.

Next room. Two figures. One is loud and forward. One is small and tucked into a corner. The player walks toward the loud one. The HUD shakes. The player backs off. The HUD steadies. The player turns toward the tucked figure instead. They pick Ask. The figure shows a single image: a closed box. The player switches to Offer and gives a gift token from the prior room. The box opens slightly. A Token drops.

Third room. The Carry-Out altar. The player places the Token. The screen reads: "Carry this with you today. Notice when you go quiet in a meeting."

Run complete. The Codex opens the entry for "Witness" and links it to the book chapter on indirect access.

### 1.6 Sample Run, Adept Mode

A reader enters. No overlays. The Signal HUD reads noisier. Figures react faster.

The player meets a figure with a stronger Wall pattern. They try Reflect. The Wall thickens. The player switches to Witness. The Wall softens. They hold Witness across three beats, watching Ground. Ground drops 20 percent. They step out of range, let Ground recover, and step back in. The figure offers a Token without prompting.

The room exits open. Three Tokens wait at the Carry-Out altar. The player picks the one with the heaviest signal weight. The run ends with a carry-out tied to a real action.

### 1.7 What the Game Is Not

It is not a combat game.

It is not a logic puzzle.

It is not a therapy app and gives no clinical advice.

It is not a story-heavy narrative game.

It is not endless. Runs are short and self-contained.

---

## Part 2. Game Design Document

### 2.1 Core Mechanics

#### Signal

Signal is the central reading mechanic. It tells the player where attention belongs and how a figure is responding. Signal has three readable properties.

Strength. How loud the signal is. Shown as a circular pulse meter on the HUD.

Direction. Where the signal points. Shown as a coarse compass arc, not an arrow. Players have to triangulate by moving.

Quality. Sharp, dull, jagged, or steady. Shown through color and animation on the pulse meter. Quality is the hardest property to read and the most informative.

Players see no numerical stats. Signal is a felt read, surfaced through HUD animation.

#### Approach

The player has four interaction verbs. Each affects figures differently.

Witness. Hold attention without acting. Lowers most walls slowly. Costs little Ground. Default safe move.

Reflect. Show the figure back to itself. Works on figures who are loud and unread. Backfires on figures who are guarded.

Offer. Give a Token from inventory. Works on figures who are closed and protective. Limited by inventory.

Ask. Request something explicit. Strong reward on the right figure. Triggers walls on the wrong one.

The player picks one Approach per beat. A beat is roughly three seconds.

#### Ground

Ground is the player's stability resource. It starts each run at 100. It drains under these conditions.

The player stays in a charged room too long. The player uses Ask or Reflect on the wrong figure. The player ignores a wall response and keeps pressing. Two figures are active in the same room.

Ground recovers under these conditions.

The player exits a room to a neutral corridor. The player uses Witness on a stable figure. The player stands at a Ground Pool, a small environmental feature.

If Ground hits zero, the run ends. The player keeps any Tokens earned and exits to the menu. No penalty.

#### Range

Range is the proximity window inside which signal locks on. Too far, and signal goes coarse. Too close, and walls spike. The visual indicator is a ring around the player. The ring color shifts as the player crosses the inner and outer edges of range.

Range is the spatial expression of the stable range concept from the book.

#### Carry-Out

Every successful run ends at the Carry-Out altar. The player places one Token. The game outputs a single Carry-Out line, a behavioral suggestion tied to the Token. Examples.

"Notice when you go quiet in a meeting."

"When the urge to fix arrives, wait one minute first."

"Send the message you wrote yesterday and did not send."

Carry-Out lines come from a curated content table. They are short, concrete, and non-clinical.

### 2.2 Figures

Figures are the inhabitants of the Hold. They map to Presences in the book. Each figure has a type, a protection, a wall pattern, a signal signature, and a set of Approach affinities.

#### Figure Types

Guardian. Stands at thresholds. Blocks entry to deeper rooms. Strong walls. Lowers to Witness held over time.

Watcher. Observes from the edge of a room. Does not block. Drops Tokens when acknowledged with Witness or Reflect.

Carrier. Holds a Token visibly. Will not release it without Offer.

Hidden. Sits behind a screen, mask, or curtain. Signal is faint. Surfaces only when range is exact.

Loud. Dominates a room. Walls drop fast under Reflect. Walls spike under Ask.

Young. Small, low to the ground. Walls fragile. Punishes mismatched approaches. Pairs well with Offer.

#### Walls

Walls are the figure's defenses. The game shows them as a translucent shell around the figure. Wall thickness is visible. Wall behavior responds to player action in real time.

Walls thicken when the player moves fast inside Range, picks a mismatched Approach, or uses Ask without earned trust.

Walls thin when the player holds Witness inside Range, matches Approach to figure type, or exits and returns with a relevant Token.

#### Interaction Outcomes

A completed interaction produces one of four outcomes. The figure opens a door. The figure drops a Token. The figure steps aside, revealing a room feature. The figure speaks, with a short line of text in the book's voice. The fourth outcome is reserved for late-floor figures and Adept mode.

### 2.3 The Hold

The Hold is the inner topology. The book uses "the space." The game uses "the Hold."

#### Room Types

Entry. The first room of every run. Always low-signal. Lets the player calibrate.

Standard. Three to five per run. One to two figures each.

Charged. Higher signal, faster Ground drain. Optional, behind doors marked with a thicker frame.

Quiet. Low-signal rooms with Ground Pools. Optional rest stops.

Carry-Out. The exit room. One altar, no figures.

Wall. A locked room. Returns the player to the prior corridor with a coarse hint.

#### Floor Progression

Each run runs across one floor. The floor holds between five and eight rooms. Layout is procedurally generated from a small set of room templates and a connection graph. The Carry-Out room is always reachable. Charged rooms branch off the main path and are optional.

Later versions add a second floor with deeper figures and harder Wall patterns. Out of MVP scope.

#### Doors and Gates

A door opens when its conditions are met. Most doors open after one figure interaction. Some require a specific Token. A gate is a door with a Codex requirement. The player needs a specific Codex entry to read its signal pattern.

### 2.4 Run Structure

A run has five phases.

Entry. The Entry room. Player calibrates Signal and Ground.

Exploration. Three to five Standard rooms.

Optional depth. The player chooses whether to enter Charged rooms.

Carry-Out. The player picks one Token to translate.

Reflection. A short post-run screen lists the Carry-Out, the Tokens earned, and any Codex entries opened.

#### Exit Conditions

A run ends in three ways. The player reaches the Carry-Out altar and places a Token. Ground hits zero. The player exits the run from the pause menu.

All three are neutral. No "game over" framing. No penalty.

### 2.5 Two-Mode Framework

The game ships with two modes, set at run start.

#### Apprentice Mode

For newcomers. Designed to teach the system through play.

Onboarding overlays name each HUD element on first appearance. The Signal HUD reads cleaner and easier. Figures react slower. Wall responses are more legible. Codex entries open after each interaction with a new figure type. Carry-Out outputs are simpler, with a one-line book reference.

#### Adept Mode

For readers and returning players. No teaching scaffolds.

No overlays. The Signal HUD reads noisier. Figures react in real time. Walls flex faster. Full Codex available from start. Carry-Out outputs are denser. Adept-only Tokens drop in late rooms.

Both modes share the same base content. Adept mode adds Adept-only figures and rooms after the player completes their first ten runs.

### 2.6 Codex System

The Codex is the in-game journal. It is the bridge from game-native names back to Myth-OS terminology. Hybrid mapping lives here.

#### Entry Structure

Each Codex entry has five fields.

Game name. The name used in play, such as Figure, Wall, Signal, Ground.

Book term. The matching Myth-OS term, such as Presence, Defense, Resonance, Safety Layer.

One-line definition. Short, from the book's canonical definitions.

Where it appears. The chapter where the book introduces it.

In-game example. One observed moment from the player's recent runs.

#### How Entries Open

Apprentice mode opens entries automatically after relevant in-game events. The first time the player holds Witness on a Wall and the Wall softens, the Witness entry opens.

Adept mode opens entries on demand. The player marks moments mid-run with a single keypress (V) and reviews them post-run.

#### Mapping

The full mapping table is in the appendix.

### 2.7 Progression and Meta

What persists between runs.

Codex entries opened. Total runs completed. Lifetime Carry-Out log (last 30). Modes available beyond Apprentice and Adept (none in MVP).

What resets every run.

Ground. Tokens. Room layout. Figure placements.

The game does not gate content behind grinding. A focused player reaches all base content in ten to fifteen runs.

### 2.8 UI Flow

#### Title Screen

Three elements: Start Run, Codex, Settings. No story preamble. No splash animation longer than 1.5 seconds.

#### Mode Select

Two buttons: Apprentice, Adept. One line of text under each. No marketing copy.

#### In-Run HUD

Top center: Signal HUD (pulse meter and direction arc).

Bottom center: Approach buttons (Witness, Reflect, Offer, Ask).

Top right: Ground meter.

Bottom right: Token inventory (small slots, max 3).

Bottom left: Pause.

No minimap. No score. No timer.

#### Room Screen

A single screen per room. Top-down view recommended for MVP. Figure is centered or off-center. Range ring follows the player.

#### Codex Screen

Two panels. Left: list of entries. Right: entry detail. Opened entries are full color. Sealed entries are silhouettes with no name.

#### Carry-Out Screen

Altar in center. Tokens float around it. Player picks one. The Carry-Out line appears in large text. Below it: a "Save to log" button.

#### Post-Run Screen

Single page. Carry-Out at top. Tokens earned. Codex entries opened. "Run again" and "Exit" buttons.

### 2.9 Art Direction

#### Visual Style

Flat, restrained. Two-tone color palette per room, shifting by room type. No detailed character art. Figures are silhouettes with distinguishing shapes (a tall narrow Guardian, a small low Young, a wide squat Carrier).

Reference points: Thomas Was Alone, Inside, Mountain (the David OReilly game), Hyper Light Drifter title art.

Avoid: skeuomorphic dungeon art, swords-and-shields imagery, fantasy tropes, anything suggesting violence.

#### Audio Direction

One ambient drone per room, tuned to room type. Signal pulses use a soft tone. Walls produce a low rumble when thick, a quiet hush when thin. The Carry-Out altar sustains a single note when the Token is placed.

No music. No voice acting. No spoken instructions.

#### Tone Reference

The game's tone is the book's tone. Direct. Controlled. Cool at the edges. No motivational language. No celebratory effects on success. A successful interaction is acknowledged with a small visual confirmation, not a particle burst.

### 2.10 Failure Design

The game has no fail state in the conventional sense. Ground depletion ends the run without penalty. The player keeps the Codex entries they opened.

This is intentional. The book's claim is direct: force and pressure trigger defenses. The game enforces the same rule. If the player pushes through, the run ends. The lesson sits in the ending, not in a punishment screen.

### 2.11 Initial Content Targets

Figures: 12 (two of each type).

Room templates: 15.

Approaches: 4 (Witness, Reflect, Offer, Ask).

Tokens: 20, each with art and signal weight.

Carry-Out lines: 60.

Codex entries: 22.

This content set supports 15 to 25 hours of varied play before patterns repeat.

---

## Part 3. Prototype Specification

### 3.1 Tech Stack and Rationale

#### Recommended Stack

Phaser 3 with TypeScript.

Why Phaser 3. Mature 2D browser engine. Built-in scene management, input handling, asset loading, and physics. Strong community. Runs in any modern browser without install.

Why TypeScript. Strong typing for figure definitions, room templates, and Token tables. Catches the kinds of content errors a content-heavy game produces.

Build tool: Vite. Fast, simple, well-suited to small games.

Hosting: Static hosting (Netlify, Vercel, Cloudflare Pages). No backend required for MVP.

#### Alternatives Considered

Vanilla JS plus Canvas. Lighter but more boilerplate. Reject for MVP.

PixiJS. Strong renderer, lacks built-in game systems. Reject.

React plus Canvas. Overhead for a single-canvas game. Reject.

Unity WebGL. Overkill for the visual style. Heavy load times. Reject.

### 3.2 File Structure

```
myth-os-hold/
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
├── public/
│   ├── audio/
│   └── art/
└── src/
    ├── main.ts              # Phaser bootstrap
    ├── config.ts            # Game config, tuning constants
    ├── scenes/
    │   ├── BootScene.ts
    │   ├── TitleScene.ts
    │   ├── ModeSelectScene.ts
    │   ├── RunScene.ts      # Main gameplay loop
    │   ├── CarryOutScene.ts
    │   ├── CodexScene.ts
    │   └── PostRunScene.ts
    ├── systems/
    │   ├── Signal.ts        # Signal HUD logic
    │   ├── Ground.ts        # Ground meter logic
    │   ├── Range.ts         # Range ring logic
    │   ├── Approach.ts      # Approach action handlers
    │   ├── WallEngine.ts    # Figure wall response
    │   └── RunGenerator.ts  # Procedural floor layout
    ├── entities/
    │   ├── Player.ts
    │   ├── Figure.ts
    │   ├── Token.ts
    │   └── Room.ts
    ├── content/
    │   ├── figures.ts       # Figure definitions
    │   ├── rooms.ts         # Room templates
    │   ├── tokens.ts        # Token definitions
    │   ├── carryouts.ts     # Carry-Out lines
    │   └── codex.ts         # Codex entries
    ├── ui/
    │   ├── SignalHUD.ts
    │   ├── GroundMeter.ts
    │   ├── ApproachBar.ts
    │   ├── TokenInventory.ts
    │   └── CodexPanel.ts
    └── persistence/
        └── SaveStore.ts     # LocalStorage wrapper
```

### 3.3 Data Shapes

Figure:

```ts
interface Figure {
  id: string;
  type: 'Guardian' | 'Watcher' | 'Carrier' | 'Hidden' | 'Loud' | 'Young';
  protects: string;              // narrative tag, not used in mechanics
  wallProfile: WallProfile;      // thickness curve, response speed
  signalSignature: SignalPattern;
  affinities: Record<Approach, number>; // -2 to +2
  drops: TokenId[];
  opensCodex: CodexEntryId[];
}
```

Room:

```ts
interface Room {
  id: string;
  template: 'entry' | 'standard' | 'charged' | 'quiet' | 'carryOut' | 'wall';
  figureSlots: FigureSlot[];
  doors: Door[];
  features: RoomFeature[];
  ambientSignal: number; // 0 to 100
}
```

Token:

```ts
interface Token {
  id: string;
  art: string;
  signalWeight: number;       // affects Carry-Out outputs
  associatedFigure?: FigureId;
}
```

Save state:

```ts
interface SaveState {
  codexOpened: CodexEntryId[];
  runsCompleted: number;
  carryOutLog: CarryOutEntry[]; // last 30
  modesAvailable: Mode[];
}
```

Save state writes to LocalStorage. No server.

### 3.4 Build Phases (MVP Cut)

Phase 0. Setup, one week. Vite plus Phaser plus TypeScript scaffold. Empty scenes. Title screen with two buttons. SaveStore stub. Deliverable: Game boots in browser. Title to mode select to empty run scene.

Phase 1. Core room loop, two weeks. One room. One figure. Player movement. Signal HUD. Range ring. Approach bar. Wall engine responds to Approach choice. Door opens on successful interaction. Deliverable: A single room is playable end to end.

Phase 2. Multi-room runs, one week. RunGenerator builds a five-room floor. Doors connect rooms. Carry-Out room ends the run. Post-run screen. Deliverable: A full run is playable.

Phase 3. Content, two weeks. Six figures (one per type). Eight room templates. Twelve Tokens. Thirty Carry-Out lines. Twelve Codex entries. Deliverable: Runs feel varied across three sessions.

Phase 4. Two modes, one week. Apprentice overlays. Adept tuning. Codex auto-open in Apprentice, manual in Adept. Deliverable: Both modes work.

Phase 5. Art and audio polish, two weeks. Final art for figures and rooms. Ambient drones. Signal pulse sounds. Carry-Out altar audio. Deliverable: Game looks and sounds shippable.

Phase 6. Playtest and tune, two weeks. Six external playtesters. Tune Ground drain rates, Wall response curves, Carry-Out output clarity. Deliverable: Shippable build.

Total: about 11 weeks for a solo dev or a pair.

### 3.5 Out of MVP Scope

Second floor with deeper figures. Multiplayer or social features. Account system or cloud save. Mobile-optimized UI (desktop browser only for MVP). Localization. Achievements. Replay system. DID-specific content (Part 3 of the book). Treat the DID module as a post-MVP track with its own design pass and clinical review.

---

## Appendix. Codex Mapping Table

| Game name | Book term | One-line definition |
|---|---|---|
| Figure | Presence | An internal figure, part, or agent within the system. |
| Wall | Defense | Mechanism blocking direct access to protected material. |
| Signal | Resonance | Emotional signal indicating relevance. |
| Ground | Safety Layer | The stable base under which interaction is viable. |
| Range | Stable range | The arousal window inside which the system functions. |
| The Hold | Inner Topology | The internal space where presences exist and interaction occurs. |
| Approach | Interaction Loop | A single interaction beat with a presence. |
| Witness | Interaction primitive | Hold attention without acting. |
| Reflect | Interaction primitive | Show the figure back to itself. |
| Offer | Interaction primitive | Give something earned earlier. |
| Ask | Interaction primitive | Request something explicit. |
| Token | Interaction artifact | Material the figure releases. |
| Carry-Out | Translation | Conversion of internal work into outward behavior. |
| Run | Practice session | One bounded interaction session. |
| Hold opening | Access | Indirect interaction with protected internal states. |
| HUD | Symbolic Interface Layer | Symbolic surface through which internal state becomes legible. |
| Codex and Carry-Out log | Reinforcement | Mechanism by which learning persists across sessions. |

---

End of specification.
