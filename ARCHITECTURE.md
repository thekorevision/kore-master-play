# Architecture: kore-master-play

The full end-state design for Kore Town and future Kore games, derived from logic.

## 1. Engine decision record

**Decision: Godot (4.x line), GDScript for game logic, with performance-critical systems isolated so they can be ported to C# or GDExtension without redesign.**

Alternatives considered:

- **Unity**: strong tooling and asset store, rejected on license risk. A solo founder's life's work cannot sit under terms a vendor can revise retroactively, as the industry saw with the 2023 runtime fee episode.
- **Unreal**: rejected as oversized for 2D pixel work; its strengths (high-end 3D) are not this game's needs, and its weight slows a small team's iteration.
- **RPG Maker**: fast for a first game, rejected as a ceiling: scripting, simulation depth, and export control are too constrained for a town meant to grow for a decade.
- **Custom engine**: rejected on time. The game is the product, not the engine.
- **Godot**: MIT licensed, no royalties, first-class 2D, scene system that maps naturally onto districts and interiors, exports to desktop, mobile, and web from one project. Its community (well over one hundred thousand stars on GitHub) is the support network.

Revisit triggers: a future 3D Kore title reopens the decision for that title only. Kore Town stays Godot.

## 2. World architecture

### Districts and cells
The town is a set of districts, each a Godot scene tree with a stable district id. Districts load by adjacency: the player's district and its neighbors are live; the rest of the town runs in simulation-lite (schedules and state advance without rendering). Interiors are cells attached to building entries, so the town can grow new buildings without reworking the map.

### Time and seasons
One world clock drives: day and night, NPC schedules, shop hours, crop and garden growth, and the season wheel. Festivals are scheduled events on the town calendar, defined in content data. Time never moves faster than the design allows; there is no energy system and no waiting monetization.

### NPC simulation
Each named NPC has: a home, a schedule (data), a relationship graph with the player and other NPCs, and a memory store of significant interactions. Dialogue selection reads schedule, season, relationship, and memory, in that order, so a neighbor remembers the repair day you helped with and asks about the garden you planted. Simulation-lite advances off-screen NPCs on the same data, so the town is consistent when you arrive.

## 3. Save architecture

- **Format**: a versioned document (header with format version, world state, player state, NPC states, town calendar position, content pack manifest).
- **Migration chain**: every format version has a tested migrator to the next. The test suite carries golden saves from every shipped version; an update that cannot migrate a golden save does not ship.
- **Slots and autosaves**: multiple manual slots plus a rotating autosave; saves are atomic writes (write to temp, verify, rename) so a power cut cannot corrupt a life in the town.
- **Content packs**: saves record which packs they were made with. Missing-pack content degrades to safe placeholders, never to a failed load.

## 4. Content pipeline

- Dialogue, quests, items, festivals, and schedules live as structured data files under `content/`, validated by schema in CI.
- A content authoring guide lets a writer add a festival or a quest line without opening the engine.
- Localization is structural from day one: all player-facing strings are keys, even while only English ships.

## 5. Asset pipeline

- **Source art** is kept at working resolution under `assets/source/`; the pipeline exports at the town's single pixel density with the shared palette applied and checked.
- Palette and density violations fail the build, not a reviewer's mood.
- Animation standards: frame counts and timing conventions per action class (walk, work, idle, celebrate), documented with examples.
- Audio: original music and ambience only, mastered to the shared loudness standard used across Kore media.

## 6. Systems

Farming and gardens, repair and crafting (the town's way of honoring the reclaimed-materials ethic of the real Kore), fishing and foraging, home decoration, town projects (multi-week community builds the player contributes to), and a gentle economy with no premium currency, ever.

## 7. Platform plan

Desktop first (Windows, macOS, Linux), then mobile, then web demo. One project, per-platform export presets, input abstraction so touch and controller are first-class alongside keyboard.
