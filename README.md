# Rhythm Raven: Precision Audio Engine
![Unity](https://img.shields.io/badge/Unity-100000?style=for-the-badge&logo=unity&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![DSP](https://img.shields.io/badge/Audio-DSP_Sync-blueviolet?style=for-the-badge)

**A modular rhythm game engine built in Unity, featuring accurate DSP-based audio synchronization and a tick-based quantization system.**

![Gameplay Demo](./assets/raven-rhythm-demo.gif)

## About
**Rhythm Raven** is a multi-level rhythm game where players perform tasks to the beat of a soundtrack. Unlike standard game loops that rely on frame-based timing (`Time.deltaTime`), this engine utilizes Unity's **Audio DSP Time** to ensure visual cues never drift from the audio track, even during frame rate drops.

* **Play the Game:** [\[Link to Itch.io\]](https://ravenrhythm.itch.io/raven-rhythm)
* **Watch Trailer:** [\[Link to YouTube\]](https://youtu.be/D2Ttavz53Ag)

## Technical Architecture

### 1. DSP Audio Synchronization
The core of the engine is the `RhythmTimer` class.
* **The Problem:** Standard `Update()` loops cause "drift" because frames are variable, while audio is continuous.
* **The Solution:** Implemented a scheduling system based on `AudioSettings.dspTime` to calculate the exact song position independent of the rendering pipeline.

### 2. Tick-Based Quantization
Input windows are calculated using "Ticks" (1/4 of a beat) rather than milliseconds.
* **Abstract Implementation:** The `BeatmapVisualizerSimple` class listens for tick changes (`curr_tick != lastTick`) and triggers events only on specific quantization steps.
* **Modular Design:** This allows different minigames (like *Whack-a-Mole*) to inherit the timing logic while implementing unique gameplay mechanics.

### 3. State Machine & Input Validation
The `WackamoleManager` handles complex sprite states to provide visual feedback:
* **Dynamic Sprite Swapping:** Manages states for Idle, Snake, Worm, and "Smile Worm" (success state) based on beat triggers.
* **Input Validation:** Implements a "Coyote Time" window (`inputWindowSize`) allowing players to hit notes slightly early or late while maintaining a "Perfect" score streak.
* **Coroutine Management:** Uses coroutines (`PopUpAnimation`) that are strictly timed to the `quarterNoteTime` to ensure animations start and end exactly on the beat.

## Key Scripts (Wackamole Level)
* `RhythmTimer.cs`: The master clock using `AudioSettings.dspTime`.
* `WackamoleManager.cs`: Level controller managing score, input windows, and sprite pooling.
* `BeatmapVisualizerSimple.cs`: Abstract base class for beat interpretation.
* `GameManager.cs`: Global state manager handling pausing, scenes, and volume mixing.

## Credits
Developed by the **Rhythm Raven Team**:
* **Kevin Lu:** Project Lead and Gameplay Engineer.
* **Hana Kopp** Art and Game Flow Engineer.
* **Carter Ng-Yu** Gameplay Engineer.
* **Kalen Lauring** Gampleplay Engineer and Audio Track Producer.
* **Carlos Schober** Gameplay Engineer and Audio Track Producer.
* **Cindie Li** Art

---