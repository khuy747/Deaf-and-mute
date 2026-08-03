# 💻 Software - Gesture Air Piano Application

This directory contains the Python application for the **Gesture Air Piano**.

---

## 📁 Layout

```text
software/
├── README.md                  # This file
├── requirements.txt           # Python dependencies
└── src/                       # Source modules
    ├── __init__.py            # Package initializer
    ├── camera.py              # CameraManager (OpenCV video feed)
    ├── hand_tracker.py        # HandTracker (MediaPipe hand detector)
    ├── gesture_classifier.py  # GestureClassifier (Finger counting & note mapping)
    ├── audio_player.py        # AudioSynthesizer (Pygame & NumPy sine wave generator)
    ├── ui_overlay.py          # UIOverlay (HUD & visual key renderer)
    └── main.py                # Main application entry point
```

---

## 🛠️ Requirements & Setup

- **Python**: 3.10 or higher
- **Dependencies**:
  - `opencv-python` (Webcam capture & UI rendering)
  - `mediapipe` (AI Hand Tracking & 3D Landmark detection)
  - `pygame` (Low-latency audio playback)
  - `numpy` (Real-time audio sine wave calculation)

### Installation:

```bash
# Navigate to repository root
cd PIF_AI_INTEL

# Create & activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Linux/macOS
# OR
.\venv\Scripts\activate   # On Windows PowerShell

# Install required packages
pip install -r software/requirements.txt
```

---

## 🚀 Execution

Run the application using Python from the repository root or inside `software/`:

```bash
python software/src/main.py
```

### Keyboard Shortcuts:
- **`q`**: Quit the application.
- **`m`**: Toggle audio mute / unmute.

---

*Last Updated: 2026-08-03*
