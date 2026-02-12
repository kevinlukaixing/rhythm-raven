# Contributions

Individual technical contributions from each member of the Rhythm Raven team.

---

## Kevin Lu — Project Lead & Gameplay Engineer

### DSP Audio Synchronization
Built the core timing engine (`RhythmTimer.cs`) using `AudioSettings.dspTime` to solve audio drift caused by frame-based `Update()` loops. The scheduling system calculates exact song position independent of the rendering pipeline, keeping all visual cues locked to the audio track.

### Tick-Based Quantization
Designed an input system based on "Ticks" (1/4 of a beat) rather than milliseconds. The `BeatmapVisualizerSimple` class listens for tick changes (`curr_tick != lastTick`) and triggers events only on specific quantization steps, serving as the abstract base class that all minigames inherit from.

### Whack-a-Mole State Machine & Input Validation
Implemented the `WackamoleManager`, which handles complex sprite states and beat-synced gameplay:
* **Dynamic Sprite Swapping:** Manages states for Idle, Snake, Worm, and "Smile Worm" (success state) based on beat triggers.
* **Input Validation:** Implements a "Coyote Time" window (`inputWindowSize`) allowing players to hit notes slightly early or late while maintaining a "Perfect" score streak.
* **Coroutine Management:** Uses coroutines (`PopUpAnimation`) strictly timed to `quarterNoteTime` to ensure animations start and end exactly on the beat.

### Global State Management
Built `GameManager.cs` to handle pausing, scene transitions, and volume mixing across all levels.

### Key Scripts
* `RhythmTimer.cs` — Master clock using `AudioSettings.dspTime`.
* `WackamoleManager.cs` — Level controller managing score, input windows, and sprite pooling.

---

## Hana Kopp — Art & Game Flow Engineer

*Section to be filled in by Hana.*

---

## Carter Ng-Yu — Gameplay Engineer

*Section to be filled in by Carter.*

---

## Kalen Lauring — Gameplay Engineer & Audio Track Producer

*Section to be filled in by Kalen.*

---

## Carlos Schober — Gameplay Engineer & Audio Track Producer

*Section to be filled in by Carlos.*

---

## Cindie Li — Art

*Section to be filled in by Cindie.*

---
