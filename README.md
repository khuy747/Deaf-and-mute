# 🎹 Gesture Air Piano - Computer Vision & ML

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

---

## 📖 Overview

**Gesture Air Piano** is a Computer Vision and Machine Learning project that translates real-time hand gestures captured via camera into musical notes (piano tones). By analyzing hand landmarks and finger counts, users can play musical notes in the air without physical instruments.

---

## 🏗️ System Architecture

```
┌──────────────┐     ┌──────────────────────┐     ┌────────────────────┐
│ Webcam Input │ ──► │  Hand Tracker        │ ──► │ Gesture Classifier │
└──────────────┘     │  (MediaPipe Hands)   │     │ (Finger Counting)  │
                     └──────────────────────┘     └─────────┬──────────┘
                                                            │
                     ┌──────────────────────┐               │
                     │  Audio Synthesizer   │ ◄─────────────┤
                     │  (Pygame/NumPy Sine) │               │
                     └──────────────────────┘               │
                                                            ▼
                     ┌──────────────────────┐     ┌────────────────────┐
                     │ On-Screen Display    │ ◄── │ Note Mapper & UI   │
                     │ (OpenCV Window)      │     └────────────────────┘
                     └──────────────────────┘
```

---

## 📁 Repository Structure

```text
PIF_AI_INTEL/
├── README.md                  # Project overview & quick start
├── PROJECT_RULES.md            # Naming conventions & coding standards
├── LICENSE                    # MIT License
│
├── docs/                      # Project documentation & design specs
│   ├── specs.md               # Functional & non-functional specifications
│   ├── architecture.md        # System architecture & component contracts
│   └── task_tracking.md       # Milestones & task tracking
│
├── software/                  # Core Python application
│   ├── README.md              # Software documentation & usage guide
│   ├── requirements.txt       # Dependencies (OpenCV, MediaPipe, Pygame, NumPy)
│   └── src/                   # Source code
│       ├── camera.py          # Video capture manager
│       ├── hand_tracker.py    # MediaPipe hand detector
│       ├── gesture_classifier.py # Finger counting & gesture mapping
│       ├── audio_player.py    # Real-time sine wave audio synthesizer
│       ├── ui_overlay.py      # HUD visualizer & landmark renderer
│       └── main.py            # Application entry point
│
└── tools/                     # Utility scripts & helpers
```

---

## 🛠️ Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/khuy747/Deaf-and-mute.git
   cd Deaf-and-mute
   ```

2. **Set up a Python virtual environment (Python 3.10+ recommended):**
   ```bash
   python -m venv venv
   # On Windows:
   .\venv\Scripts\activate
   # On Linux/macOS:
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r software/requirements.txt
   ```

4. **Run the Air Piano application:**
   ```bash
   python software/src/main.py
   ```

---

## 📋 Documentation Links

- [System Specifications](docs/specs.md)
- [System Architecture](docs/architecture.md)
- [Project Rules & Conventions](PROJECT_RULES.md)
- [Task Tracking](docs/task_tracking.md)

---

## 📄 License

Distributed under the [MIT License](LICENSE).
