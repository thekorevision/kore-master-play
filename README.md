# kore-master-play

The master repository for Kore games: home of **Kore Town**, a cozy pixel RPG, and the foundation for future Kore game work.

**Owner:** Kristian Brown, founder of Kore ("Keeping Our Roots Enriched")
**Status:** Concept stage. Kore is unincorporated and pre-revenue. This repository is the clean master design, built from logic first. It does not replace or modify any earlier repository; it stands beside them as the reference architecture.

## The end-state vision

Designed as if resources were unlimited:

- **Kore Town**: a warm, walkable pixel town where the Kore world lives at human scale: neighbors, workshops, gardens, seasons, small kindnesses with real weight. A place players return to the way they return to a hometown, not a level they finish.
- A town that can grow for years: new districts, festivals, and stories added as content packs without invalidating anyone's save or memories.
- Characters with schedules, relationships, and memory, so the town feels lived in rather than scripted.
- A bridge, used carefully, between play and the real Kore world: town events can echo real community life (a community garden, a repair day) without ever turning the game into an advertisement.

## Engine choice

**Godot** is the engine. The rationale is documented in full in [ARCHITECTURE.md](ARCHITECTURE.md); in short: it is free and open source with no royalty or license cliff, it exports to every platform Kore cares about from one project, its 2D tooling is first class for pixel work, and a solo founder can own the whole stack without a vendor relationship deciding the game's future.

## Design principles

1. **Cozy is a discipline, not a lack of stakes.** No fail states that punish; stakes live in relationships, seasons, and choices that matter to the town.
2. **The save file is a promise.** Saves are versioned, migratable, and never silently broken by an update. A player's years in the town outrank any refactor.
3. **Content is data.** Dialogue, quests, festivals, and items are data files creators can edit without touching engine code.
4. **Art discipline.** One pixel density, one palette discipline, one animation standard across the whole town, enforced by the asset pipeline, so districts built years apart still belong to the same place.
5. **Offline and owned.** The game is fully playable offline; no account is required to live in Kore Town.

## Repository layout

- `game/` The Godot project: scenes, scripts, systems.
- `content/` Data-driven content: dialogue, quests, items, festivals, town data.
- `assets/` Art and audio pipeline: source art, palette, export rules, processed assets.
- `world/` World architecture: districts, schedules, seasons, simulation state.
- `saves/` Save format specification, migration chain, test saves.
- `docs/` Design documents, art standards, content authoring guides.

## Relationship to other masters

- Kore Town characters and lore draw on canon maintained for the story work executed in **kore-master-forge**; the game interprets the world for play, it does not rewrite canon.
- Trailers and town films are produced by kore-master-forge from this repo's builds and asset discipline.

## License

MIT for code and tooling. Game art, music, characters, and authored content remain the owner's work and are not covered by the code license. See [LICENSE](LICENSE).
