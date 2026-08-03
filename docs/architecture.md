# 🏗️ System Architecture

> *Status: APPROVED.* This document details the software architecture, modular breakdown, and component contracts for the **Gesture Air Piano** application.
> Technical specifications and requirements are located in [specs.md](specs.md).

---

## Table of Contents

- [1. Architectural Principles](#1-architectural-principles)
- [2. System Overview](#2-system-overview)
  - [2.1 Block Diagram](#21-block-diagram)
  - [2.2 Data Pipeline & Execution Flow](#22-data-pipeline--execution-flow)
- [3. Component Descriptions & Contracts](#3-component-descriptions--contracts)

---

## 1. Architectural Principles

| # | Principle | Explanation |
|---|-----------|-------------|
| 1 | **Modular Separation of Concerns** | Camera capture, AI landmark extraction, gesture classification, audio synthesis, and UI rendering operate as independent, decoupled modules. |
| 2 | **Low Latency Pipeline** | All frame processing occurs synchronously in a tight main loop with zero file I/O during runtime. Audio synthesis uses pre-allocated memory buffers. |
| 3 | **Stateful Note Triggering** | Audio notes are triggered on edge transitions (finger state change from folded to extended) to avoid audio clutter or continuous re-triggering artifacts. |

---

## 2. System Overview

### 2.1 Block Diagram

```text
               ┌──────────────────────────────┐
               │    CameraManager (OpenCV)    │
               └──────────────┬───────────────┘
                              │  raw BGR frame
                              ▼
               ┌──────────────────────────────┐
               │  HandTracker (MediaPipe)     │
               └──────────────┬───────────────┘
                              │  hand landmarks (21 points) + handedness
                              ▼
               ┌──────────────────────────────┐
               │     GestureClassifier        │
               └──────┬────────────────┬──────┘
                      │                │
     active note state│                │ landmark data & note label
                      ▼                ▼
┌──────────────────────────┐      ┌──────────────────────────┐
│ AudioSynthesizer         │      │ UIOverlay (Heads-Up)     │
│ (Pygame Mixer / Sine)    │      │ (OpenCV Render)          │
└──────────────────────────┘      └────────────┬─────────────┘
                                               │ annotated BGR frame
                                               ▼
                                  ┌──────────────────────────┐
                                  │   On-Screen Display      │
                                  └──────────────────────────┘
```

---

## 2.2 Data Pipeline & Execution Flow

1. **Frame Capture**: `CameraManager` fetches raw BGR frame from webcam.
2. **Landmark Detection**: `HandTracker` converts frame to RGB and passes it to MediaPipe Hands model, extracting 21 normalized 3D landmarks for each detected hand.
3. **Gesture Classification**: `GestureClassifier` compares finger tip landmark coordinates against PIP/MCP joints to determine which fingers are extended. It calculates the extended finger count and maps it to a musical note (e.g., 1 finger ➔ C4, 2 fingers ➔ D4).
4. **Audio Playback**: `AudioSynthesizer` checks if a new note transition occurred. If a new note is triggered, it plays the generated sine wave sound channel via Pygame.
5. **UI HUD Rendering**: `UIOverlay` overlays hand skeleton landmarks, bounding boxes, hand labels (Left/Right), active finger count, active note text, and virtual piano key indicators onto the OpenCV window frame.

---

## 3. Component Descriptions & Contracts

### 3.1 `CameraManager` (`software/src/camera.py`)
- **Responsibility**: Manages OpenCV `VideoCapture` pipeline, frame acquisition, resolution setting, and clean release.
- **Key Method**: `get_frame() -> Tuple[bool, np.ndarray]`

### 3.2 `HandTracker` (`software/src/hand_tracker.py`)
- **Responsibility**: Wraps MediaPipe Hands solution. Detects up to 2 hands and returns structured landmark objects.
- **Key Method**: `process(frame: np.ndarray) -> List[HandData]`

### 3.3 `GestureClassifier` (`software/src/gesture_classifier.py`)
- **Responsibility**: Analyzes `HandData` to calculate finger status (extended/folded), total finger count, and corresponding piano note frequency/label.
- **Key Method**: `classify(hand_data: HandData) -> GestureResult`

### 3.4 `AudioSynthesizer` (`software/src/audio_player.py`)
- **Responsibility**: Initializes Pygame Mixer audio subsystem. Generates floating-point sine wave audio buffers for musical frequencies and manages note playback channels.
- **Key Method**: `play_note(note_name: str)`, `stop_note(note_name: str)`

### 3.5 `UIOverlay` (`software/src/ui_overlay.py`)
- **Responsibility**: Renders visual HUD elements, landmark connections, active note text, and piano keyboard visualizers.
- **Key Method**: `draw(frame: np.ndarray, hands_data: List[HandData], gesture_results: List[GestureResult], fps: float) -> np.ndarray`

---

*Last Updated: 2026-08-03*
