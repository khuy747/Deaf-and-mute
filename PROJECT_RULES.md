# 📏 PROJECT_RULES — Project Guidelines & Standards

> This document contains all conventions and guidelines for this repository.
> It serves as the **Single Source of Truth**. Other README files describe directory structures and link back here.

---

## 1. File Naming Rules

- **NEVER** place raw source code files (`.c`, `.h`, `.py`) directly at the repository root.
- **Third-Party Libraries**: Place in appropriate subdirectories or `software/src/` or `tools/`.

### Permitted files at root:
- `README.md`
- `.gitignore`
- `LICENSE`
- `PROJECT_RULES.md`

---

## 2. Code Architecture & Conventions

### Directory Naming Rules:
- All source directories inside `software/` use lower `snake_case` or standard Python package layout (`software/src/`).
- Assets and sound files reside in `software/assets/`.

### File Naming Rules:
**All code and documentation files MUST use `snake_case` (lowercase with underscores `_`).**

| Category | Rule | Good Example ✅ | Bad Example ❌ |
|----------|------|-----------------|----------------|
| Python script | `<module_function>.py` | `hand_tracker.py` | `HandTracker.py` |
| Documentation | `<topic_name>.md` | `task_tracking.md` | `TaskTracking.md` |
| Asset | `<note_name>.wav` | `c4_tone.wav` | `NoteC4.wav` |

### Python Code Conventions (PEP 8 Compliant):
- **Classes**: `PascalCase` (e.g., `HandTracker`, `GestureClassifier`, `AudioSynthesizer`).
- **Functions/Methods**: `snake_case()` (e.g., `detect_hands()`, `count_fingers()`, `play_note()`).
- **Variables**: `snake_case` (e.g., `finger_count`, `active_note`).
- **Constants**: `UPPER_SNAKE_CASE` (e.g., `NOTE_FREQUENCIES`, `MAX_HANDS`, `WEBCAM_ID`).
- **Private methods**: Prefix with single underscore `_snake_case()` (e.g., `_generate_sine_wave()`).

---

## 3. Documentation Rules

### Directory Level Docs:
Every main component folder (`docs/`, `software/`, `tools/`) contains a `README.md` describing:
- Purpose and structure of the directory.
- Prerequisites, setup steps, and usage instructions.

### Module Level Docs:
Each major module or script should contain docstrings detailing:
- Module purpose.
- Inputs, outputs, and parameters.
- Dependencies and usage notes.

---

## 4. Git Commit Message Conventions

Commit messages must follow the structured format:
```
[PREFIX] Concise description in English
```

### Prefix Table:

| Prefix | Usage | Example |
|--------|-------|---------|
| `[SW]` | Software changes (Python scripts, UI, Audio) | `[SW] Add MediaPipe HandTracker module` |
| `[DOC]` | Documentation updates | `[DOC] Update specifications and architecture` |
| `[TOOL]` | Internal tools or helper scripts | `[TOOL] Add audio generator test script` |
| `[CFG]` | Configuration files (.gitignore, project rules) | `[CFG] Update project rules to English` |
| `[FIX]` | Bug fixes | `[FIX] Resolve audio clipping in sine wave generator` |
| `[REFAC]` | Refactoring / Code cleanup | `[REFAC] Modularize UI overlay logic` |
| `[STRUC]` | Project structure modifications | `[STRUC] Reorganize software directory` |

---

*Any modifications to these rules require team approval prior to committing.*
