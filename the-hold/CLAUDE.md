# CLAUDE.md. Myth-OS: The Hold.

This file orients Claude Code for work on **Myth-OS: The Hold**, a browser dungeon crawler built from the design spec in `../Myth-OS-The-Hold-Spec.md`.

Read the spec before doing any non-trivial work. The spec is the source of truth. This file is conventions, guardrails, and operational guidance only.

---

## 1. What This Project Is

A short browser game (15 to 25 minute runs) where the player moves through inner-space rooms, meets Figures who guard parts of themselves, and earns access through indirect interaction. No combat. No fail screens. Every run ends with one behavioral Carry-Out into the player's real day.

The game teaches Myth-OS by enforcing its rules. Pressure raises walls. Force ends the run. The mechanics ARE the lessons.

---

## 2. Tech Stack

- **Phaser 3**. 2D browser game engine.
- **TypeScript**. Strict mode on.
- **Vite**. Dev server and build.
- **LocalStorage**. Save state. No backend.
- **Vitest**. Unit tests.
- **ESLint + Prettier**. Lint and format.
- **Static hosting**. Netlify, Vercel, or Cloudflare Pages.

No frameworks beyond Phaser. No React. No Redux. No state libraries.

---

## 3. Commands

```
npm install          # install deps
npm run dev          # start Vite dev server on localhost:5173
npm run build        # production build to dist/
npm run preview      # preview production build locally
npm run typecheck    # tsc --noEmit
npm run lint         # eslint src/
npm run format       # prettier --write src/
npm test             # vitest
npm run test:watch   # vitest --watch
```

Run `npm run typecheck` and `npm test` before every commit.

---

## 4. File Structure

```
the-hold/
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
├── public/
│   ├── audio/
│   └── art/
└── src/
    ├── main.ts              # Phaser bootstrap
    ├── config.ts            # tuning constants. All magic numbers live here.
    ├── scenes/              # one file per Phaser scene
    ├── systems/             # gameplay systems (Signal, Ground, Range, etc.)
    ├── entities/            # Player, Figure, Token, Room classes
    ├── content/             # typed content tables (figures, rooms, tokens, codex, carryouts)
    ├── ui/                  # HUD widgets
    └── persistence/         # SaveStore (LocalStorage wrapper)
```

Full breakdown is in Part 3.2 of the spec.

---

## 5. Coding Conventions

- TypeScript strict mode. No `any` without a comment explaining why.
- Filenames: PascalCase for classes (`SignalHUD.ts`), camelCase for content tables (`figures.ts`).
- Each Phaser scene is its own file in `src/scenes/`.
- Each gameplay system is its own file in `src/systems/`.
- All tuning constants live in `src/config.ts`. No magic numbers in scenes or systems.
- Imports use the `@/` alias for `src/` (configure in `tsconfig.json` and `vite.config.ts`).
- Content tables export typed arrays. Define the type once in `src/entities/` and reuse.
- No global mutable state outside `SaveStore` and Phaser's scene registry.
- Use Phaser's built-in scene transitions. Do not roll a custom router.

Indentation: 2 spaces. Line length: 100. Single quotes for strings.

---

## 6. Design Constraints (Hard Rules)

These are not preferences. They come from the book. Violating them breaks the game's purpose.

1. **No attack button. No combat verb.** If asked to add one, refuse and link to Section 1.4 of the spec.
2. **No fail or game-over screen.** Run end is neutral. Ground depletion exits the run without penalty.
3. **No numerical stats shown to the player.** Signal is felt, not measured. HUDs show pulses, rings, arcs, not numbers.
4. **No motivational text. No celebratory effects on success.** A successful interaction shows a small visual confirmation, not a particle burst.
5. **No traditional dungeon imagery.** No swords, monsters, treasure chests, skulls, or fantasy tropes.
6. **No story preamble longer than 1.5 seconds** on the title screen.
7. **Tone: direct, controlled, cool at the edges.** The game speaks the way the book speaks.

When designing new content, run it past these seven rules first.

---

## 7. Player-Facing Text Rules

Any text the player sees (HUD labels, Carry-Out lines, Codex entries, room hints) follows the book's writing rules.

**Forbidden words** in player-facing text: can, may, just, very, really, literally, actually, certainly, probably, basically, could, maybe, delve, embark, craft, crafting, imagine, realm, game-changer, unlock, discover, skyrocket, abyss, revolutionize, disruptive, utilize, tapestry, illuminate, unveil, pivotal, intricate, elucidate, hence, furthermore, harness, exciting, groundbreaking, cutting-edge, remarkable, navigating, landscape, stark, testament, in summary, in conclusion, moreover, boost, powerful, inquiries, ever-evolving, however.

**Other rules** for player text: no em dashes (use commas, periods), no semicolons, no exclamation points, no second-person enthusiasm ("you've got this", "great job"), no hand-holding.

Add a `scripts/check-text.ts` linter that scans `src/content/*.ts` for forbidden words and fails the build if found.

---

## 8. How to Add Content

### A new Figure

1. Pick a type from the six existing types (`Guardian`, `Watcher`, `Carrier`, `Hidden`, `Loud`, `Young`). Do not invent a seventh without spec update.
2. Add an entry to `src/content/figures.ts` following the `Figure` interface (Section 3.3 of spec).
3. Set `wallProfile`, `signalSignature`, and `affinities` so the figure responds to one Approach well, one Approach poorly, and the other two neutrally.
4. Add Codex entry to `src/content/codex.ts` linking to the relevant book chapter.
5. Add unit test in `tests/figures.spec.ts` verifying affinity values are in the -2 to +2 range.

### A new Room Template

1. Pick a template type from the six existing types (`entry`, `standard`, `charged`, `quiet`, `carryOut`, `wall`).
2. Add to `src/content/rooms.ts`.
3. Define `figureSlots`, `doors`, `features`, `ambientSignal`.
4. Verify `RunGenerator.spec.ts` still produces floors with a reachable Carry-Out.

### A new Token

1. Add to `src/content/tokens.ts`.
2. Set `signalWeight` between 1 and 10 (1 = light, 10 = heavy).
3. Associate with at least one Figure via `associatedFigure`.
4. Add token art under `public/art/tokens/`.

### A new Carry-Out Line

1. Add to `src/content/carryouts.ts`.
2. Keep under 15 words.
3. Make it concrete and behavioral. Example: "Send the message you wrote yesterday and did not send." Counter-example (do not write): "Believe in yourself today."
4. Run `npm run check-text` to verify no forbidden words.

---

## 9. Testing

- Use Vitest for unit tests under `tests/`.
- Test data transformations and systems. Do not test Phaser rendering.
- Required test coverage:
  - `WallEngine` response curves
  - `Ground` drain and recovery rates
  - `RunGenerator` floor reachability (property test: every generated floor has a path to Carry-Out)
  - Content table validation (figure affinities in range, no duplicate IDs, all Codex entries reference real concepts)
- Playtesting is done by hand. Build a debug overlay in development mode showing Ground value and Wall thickness for tuning.

---

## 10. Build Order

Follow Phase 0 through Phase 6 from Section 3.4 of the spec. Do not skip ahead.

Current phase: **Phase 0 (not started)**. Update this line as work progresses.

Each phase has a clear deliverable. Treat the deliverable as a stopping point. Get feedback before starting the next phase.

---

## 11. Out of Scope

Do not build these without explicit approval:

- Combat or attack mechanics
- Multiplayer or social features
- Account system or cloud save
- Mobile-optimized UI
- Achievements or score systems
- Replay system
- Localization
- DID-specific content (Part 3 module of the book, requires clinical review)
- Story mode or narrative cutscenes
- Procedurally generated Carry-Out lines (must come from the curated table)

---

## 12. When in Doubt

Re-read the spec. The book's rules govern the design. If a proposed feature would violate "indirect access beats force," or "safety precedes access," or "resonance beats logic," do not implement it. Flag the conflict and ask.

Default to simplicity. Default to consistency. If two interpretations of the spec are viable, pick the one closer to the book's tone (direct, controlled, no padding).

---

## 13. Communication

When reporting progress, name the phase (e.g., "Phase 2, multi-room runs"), the system or scene touched, and the next blocker. No motivational framing. No marketing tone.

When asking the user for input, give two or three options with trade-offs. Do not ask open-ended "what do you want?" questions when a focused choice would unblock the work.
