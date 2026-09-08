---
layout: project
title: "Pokémon Battle"
description: "6v6 Pokémon battle game with a Tkinter GUI powered by PokeAPI - build teams, choose moves, and fight turn-based battles with type matchups and status effects"
technologies:
  - Python
  - Tkinter
  - PokeAPI
  - requests-cache
  - pytest
github_url: https://github.com/Liam-A-Wallace/PokemonBattle
---

## Project Overview

I built a 6v6 Pokémon battle game with a desktop GUI, powered entirely by the
[PokéAPI](https://pokeapi.co/). You can battle a built-in AI or a friend on the
same machine (pass-and-play), build teams of six Pokémon from across all nine
generations, and fight turn-based battles with faithful mechanics - type
matchups, STAB, physical/special split, critical hits, stat changes, switching,
and full status conditions.

## Key Features

- **Two game modes:** battle an AI opponent, or a second player in hot-seat mode.
- **Full team building:** generate random teams or hand-pick from all 1025 Pokémon
  (Gen 1-9), with an option to exclude legendary and mythical Pokémon for fairer
  random matches.
- **Move selection:** auto-assign the best four moves, or browse a Pokémon's full
  level-up learnset and pick manually.
- **Faithful battle mechanics:** the standard damage formula, type-effectiveness
  chart, STAB, physical/special split, critical hits, accuracy checks, and
  stat stages.
- **Full status conditions:** burn, paralysis, poison, bad poison, sleep, freeze,
  confusion, and flinch - all driven by each move's data from the API.
- **Live type information:** Pokémon and move types are shown with colour-coded
  badges, and every move button displays its effectiveness against the opponent's
  active Pokémon before you commit to it.
- **2D sprites:** the Pokémon HOME artwork for all 1025 Pokémon, downloaded on
  demand and rendered in the battle view.
- **Local caching:** every API response is cached to SQLite (via `requests-cache`),
  honouring PokéAPI's fair-use policy and making repeat runs fast.

## Technical Implementation

The project is a modular Python package with a clean separation between the game
engine and the presentation layer:

- **`api.py`** - a thin, cached HTTP client for PokéAPI (SQLite-backed via
  `requests-cache`).
- **`models.py`** - dataclasses for Pokémon, moves, and stats, plus level-50 stat
  calculation and learnset parsing.
- **`types.py`** - the 18×18 type-effectiveness chart, built from each type's
  `damage_relations` so matchup multipliers are always current.
- **`status.py`** - status conditions and their end-of-turn effects.
- **`battle.py`** - the turn-based battle engine (ordering by priority/speed,
  damage formula, secondary effects, switching, fainting, and win detection).
- **`ai.py`** - an AI that scores moves by expected damage × type effectiveness
  and switches out when hard-countered.
- **`ui.py`** - the Tkinter GUI, styled after the games with a Poké Ball-inspired
  palette, type badges, HP bars, and a colour-coded battle log.
- **`download_sprites.py`** - a one-time utility that fetches the 2D HOME sprites.

Network requests run on background threads with a queue, so the UI stays
responsive while teams are being fetched and built.

## Challenges & Solutions

**Handling alternate forms:** the Pokémon list endpoint returns form variants
(such as `jellicent-male`) that the species endpoint doesn't recognise, which
broke the legendary filter. I switched the team pool to the species list and
resolved each species to its default form before fetching battle data.

**Responsive UI during network I/O:** fetching and building teams can take time,
so all API calls run in worker threads with results delivered back to the Tk
event loop via a queue, avoiding any frozen UI.

**Modelling status effects from raw data:** each move's `meta` field provides
ailment, chance, and turn counts. I built a status layer that respects type
immunities (Electric can't be paralysed, Fire can't be burned, etc.) and applies
end-of-turn effects like burn and poison chip damage.

**Testability of a GUI app:** the battle engine is completely UI-agnostic, so the
core logic is verified with offline unit tests using fake API fixtures - no
network or display required.

## Learning Outcomes

This project strengthened my understanding of consuming a large REST API at
scale (caching, fair use, resolving nested resources) and of GUI development
with Tkinter, including threading to keep interfaces responsive. Separating the
battle engine from the presentation layer made the logic unit-testable and
demonstrated the value of clean architecture. Writing an effective AI opponent
also gave me practical experience with heuristic evaluation functions.

## Conclusion

Pokémon Battle combines a faithful battle simulation with a polished,
game-styled desktop interface. The clean separation between the engine, the AI,
and the UI means new features - such as held items, natures, or animated
sprites - can be added incrementally without reworking the core logic.
