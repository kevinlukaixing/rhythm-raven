# Contributions

Individual technical contributions from each member of the Rhythm Raven team, based on the project's commit history.

---

## How the core rhythm engine came together

The shared timing system was built collaboratively over November 2025:

1. **Carlos** built the first music/beat synchronization (DSP-scheduled playback), the tick grid that converts song time into sixteenth-note ticks, and the `Measure → qNote → sNote` beatmap data model.
2. **Kalen** generalized it into a reusable architecture: the abstract `BeatmapVisualizer` base class (`OnBeatTriggered`) that lets any level react to beats without reimplementing timing, plus the `beatmapBuilder` / `beatmapHelper` authoring tools for writing charts in musical terms.
3. **Kevin** packaged the timing logic into `RhythmTimer.cs` and adapted Kalen's base class as `BeatmapVisualizerSimple` for the Whack-a-Mole level.

---

## Kevin Lu — Project Lead & Gameplay Engineer

### Project Setup & Tutorial
Created the Unity project and repository structure, and implemented the original tutorial level.

### RhythmTimer
Built `RhythmTimer.cs`, a reusable clock component that tracks song position in ticks, plays an on-beat tambourine cue, and handles pause/resume/stop.

### Whack-a-Mole Level
Implemented the `WackamoleManager`, which handles sprite states and beat-synced gameplay:
* **Dynamic Sprite Swapping:** Manages states for Idle, Snake, Worm, and "Smile Worm" (success state) based on beat triggers.
* **Input Validation:** Implements a "Coyote Time" window (`inputWindowSize`) allowing players to hit notes slightly early or late.
* **Coroutine Management:** Uses coroutines (`PopUpAnimation`) timed to `quarterNoteTime` so animations start and end on the beat.

### Game Flow & Polish
Level locking and progression, build settings, and code cleanup across shared scripts.

### Key Scripts
* `RhythmTimer.cs`, `BeatmapVisualizerSimple.cs`, `WackamoleManager.cs`, `GameManager.cs`

---

## Kalen Lauring — Gameplay Engineer & Audio Track Producer

### Rhythm Engine Architecture
Designed the extensible layer of the shared rhythm engine:
* **Abstract beat-reaction class:** `BeatmapVisualizer` fires `OnBeatTriggered(noteValue)` exactly once per tick, so each level or NPC only defines *how* to react to a beat. This pattern became the base for other levels (adapted as `BeatmapVisualizerSimple`).
* **Beatmap authoring API:** `beatmapBuilder` is a fluent builder (`.PlaceQuarterNote(2, 4, 1).PlaceHalfNote(6, 3, 1)…`) that lets charts be written by measure, beat, and note length instead of raw array indices, with bounds validation. `beatmapHelper` handles note durations from sixteenth to whole notes.

### Level: Telephone Line
Built the level's game manager and gameplay systems on top of the shared engine:
* **Variable tempo map:** The song accelerates from 150 to 170 BPM and back. Ticks are accumulated per tempo segment so the beat grid stays continuous across tempo changes.
* **Tempo-adaptive input windows:** Timing leniency shifts as the song speeds up (wider early window at high BPM, where players tend to rush).
* **Input judgment state machine:** Handles perfect, late, early-and-held, and off-beat inputs. A look-ahead (`GetTicksUntilNextNote`) prevents early presses for an upcoming note from being penalized.
* **Hold-length notes:** Note durations are read from the beatmap, and the player returns to idle when a note ends.
* **Reactive NPC feedback:** Three NPC birds follow their own beatmaps and switch to a "judgy" state for a minimum duration after a miss or bad input.

### Music, Audio & Cutscenes
* Composed and produced music for the tutorial, the bossa nova track, cutscenes, the win screen, and pause-menu music across levels.
* Built player feedback sounds and the intro and final cutscenes, including audio, animation, and text.

### Integration & Polish
Scene animations, fonts and UI text, level select and player progress (PlayerPrefs), and routing between cutscenes and levels.

### Key Scripts
* `BeatMapVisualizer.cs`, `beatmapBuilder.cs`, `beatmapHelper.cs`, `kalenGameManager.cs`, `kalenTrigger*.cs`, `npcAnimation.cs`

---

## Carlos Schober — Gameplay Engineer & Audio Track Producer

### Original Beat Synchronization
Built the first synchronized music and beat system using DSP-scheduled playback (`PlayScheduled` / `AudioSettings.dspTime`), and the tick-based song position (sixteenth-note ticks per measure).

### Beatmap Data Model
Defined the `Measure → qNote → sNote` beatmap structure and the `MakeBeatmap` system for modularly defining per-level beatmaps.

### Game Architecture
Built the `GameHandler` / `SceneHandler` prefabs so any level gets pause, volume, and scene switching by dropping in one prefab. Created the pause menu, end-level, and credits scenes.

### Levels
Built the Wine Connoisseur and Mosh Pit levels.

---

## Hana Kopp — Art & Game Flow Engineer

### Game Flow Between Scenes
Built the flow that connects the game: main menu, level select (including completion tracking), level complete and level failed scenes, and the pause flow for level and non-level scenes.

### Cutscenes
Edited and finalized cutscenes, including the level complete and failed cutscenes.

### Art & UI
Created artwork and backgrounds, level art, the custom wing cursor, and fonts and text styling across menus and levels.

---

## Carter Ng-Yu — Gameplay Engineer & Game Designer

### Game Design
Contributed to the overall game design of Rhythm Raven, shaping how the minigames fit together as one experience.

### Level: Star Collector
Built the conveyor-belt level, including its beatmap, player movement, art, animation, and in-level instructions.

### Shared Gameplay Systems
Added the scoring UI and the player cue system used across levels, and handled build setup for publishing on itch.io.

### Trailer
Designed the game's trailer.

---

## Cindie Li — Art

### Level & Character Art
Created art for the tutorial (enemy bird and background sprites) and Level 3, including the singing birds.

---
