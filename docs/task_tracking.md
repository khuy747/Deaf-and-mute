# 📌 Task Tracking — Project Roadmap & Progress

> **This document tracks overall project milestones and learning module progress.**

---

## 📊 Overall Progress Summary

| Phase | Description | Status | Notes |
|-------|-------------|--------|-------|
| 0 | Project Initialization | ✅ Done | Directory layout, rules & initial templates created |
| 1 | Specs & Architecture | ✅ Done | Specs, architecture & module contracts defined in English |
| 2 | Environment Setup | ✅ Done | `software/requirements.txt` ready for installation |
| 3 | Code Module | 🔨 In Progress | Coding step-by-step with pair programming |
| 4 | Integration & Testing | ⬜ Todo | End-to-end testing & HUD polishing |
| 5 | Release v1.0 | ⬜ Todo | Project completion & showcase |

**Status Icons**: ✅ Done · 🔨 In Progress · ⚠️ Blocked · ⬜ Todo

---

## 🔧 Detailed Task Breakdown

### Phase 2 — Environment Setup ✅
- [x] Create `software/requirements.txt` dependency file

---

### Phase 3 — Step-by-Step Learning & Coding 🔨

- [ ] **Module 1: Camera Stream (`software/src/camera.py`)**
  - Learn OpenCV `VideoCapture`, resolution setup, frame flipping, and loop handling.

- [ ] **Module 2: Hand Tracking (`software/src/hand_tracker.py`)**
  - Learn MediaPipe Hands model, 21 3D landmarks, normalized coordinates to pixel coordinates mapping.

- [ ] **Module 3: Finger Gesture Classifier (`software/src/gesture_classifier.py`)**
  - Learn landmark position comparison algorithms (TIP vs PIP joints) to detect extended fingers & count fingers.

- [ ] **Module 4: Audio Synthesizer (`software/src/audio_player.py`)**
  - Learn sine wave math generation ($f(t) = A \sin(2\pi f t)$), exponential decay envelopes, and Pygame sound playback.

- [ ] **Module 5: UI Overlay & Main App (`software/src/ui_overlay.py` & `software/src/main.py`)**
  - Learn OpenCV text/rectangle/landmark drawing, FPS calculation, keyboard events, and building the final application.

---

## 🏁 Major Milestones

| # | Milestone | Phase | Status |
|---|-----------|-------|--------|
| M1 | Complete Repo Architecture & Specs | 1 | ✅ |
| M2 | Module 1: Camera Stream Running | 3 | 🔨 |
| M3 | Module 2: Hand Tracking Working | 3 | ⬜ |
| M4 | Module 3: Gesture & Finger Count Working | 3 | ⬜ |
| M5 | Module 4: Real-time Audio Playing | 3 | ⬜ |
| M6 | Module 5: Complete Air Piano Application | 4 | ⬜ |

---

*Last Updated: 2026-08-03*
