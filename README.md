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
The core timing system is built on `AudioSettings.dspTime` rather than frame-based `Update()` loops. This ensures that beat markers, input windows, and visual cues stay perfectly aligned with the audio track regardless of frame rate fluctuations.

### 2. Tick-Based Quantization
Input windows and gameplay events are calculated using "Ticks" (subdivisions of a beat) rather than raw milliseconds. An abstract base class allows each minigame to subscribe to tick events and implement its own beat-driven logic on top of the shared timing system.

### 3. Modular Minigame System
The game is structured around multiple beat-synced minigames, each with unique mechanics:
* **Whack-a-Mole** — Tap targets that appear on the beat with forgiving input windows.
* Each level inherits from the core timing engine, allowing new minigames to be added without reimplementing audio synchronization.

### 4. State Management & Game Flow
A global state manager handles scene transitions, pausing, volume mixing, and score tracking across all levels.

## Credits
Developed by the **Rhythm Raven Team**:

| Team Member | Role | Contributions |
|---|---|---|
| Kevin Lu | Project Lead & Gameplay Engineer | [View](./CONTRIBUTIONS.md#kevin-lu--project-lead--gameplay-engineer) |
| Hana Kopp | Art & Game Flow Engineer | [View](./CONTRIBUTIONS.md#hana-kopp--art--game-flow-engineer) |
| Carter Ng-Yu | Gameplay Engineer | [View](./CONTRIBUTIONS.md#carter-ng-yu--gameplay-engineer) |
| Kalen Lauring | Gameplay Engineer & Audio Track Producer | [View](./CONTRIBUTIONS.md#kalen-lauring--gameplay-engineer--audio-track-producer) |
| Carlos Schober | Gameplay Engineer & Audio Track Producer | [View](./CONTRIBUTIONS.md#carlos-schober--gameplay-engineer--audio-track-producer) |
| Cindie Li | Art | [View](./CONTRIBUTIONS.md#cindie-li--art) |

---
