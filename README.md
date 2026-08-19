![preview](https://raw.githubusercontent.com/AltisimaWana/pokeball-vision-auto-catcher/main/screen_e1d6.svg)
# VerdantGaze

**Vision-Guided Companion Acquisition for Digital Ecosystems**

![C#](https://img.shields.io/badge/C%23-.NET%208.0-512BD4) ![WPF](https://img.shields.io/badge/UI-WPF--UI-4F8EF7) ![YOLO](https://img.shields.io/badge/Detection-YOLO11-FF6F00) ![Interception](https://img.shields.io/badge/Input-Interception-00C853) ![License](https://img.shields.io/badge/License-MIT-yellow)

---

## Overview

VerdantGaze is a companion automation toolkit designed for digital pet worlds where patience and precision collide. Imagine standing in a lush virtual meadow, watching a rare creature shimmer in the distance. Your hand trembles—one mistimed throw, and it vanishes. VerdantGaze acts as your steady second pair of eyes and hands, using pure visual recognition to identify creatures on screen and orchestrate a perfectly timed capture sequence—no memory editing, no packet sniffing, just intelligent observation and seamless input simulation.

The project began as a response to the repetitive strain of manual capturing in creature-collecting games. Instead of relying on fragile game hooks or memory addresses, VerdantGaze treats your screen as a camera feed. It watches, learns, and acts—mimicking human reflexes with machine precision. The result is a tool that feels less like an automation script and more like a thoughtful companion that happens to have extraordinary hand-eye coordination.

## 🌿 Key Features

- **Pure Vision Recognition** — Uses YOLO11 object detection models trained specifically on creature sprites and capture UI elements. No memory reading, no game data injection. The tool only sees what your eyes see.
- **Adaptive Aim Calibration** — Dynamically adjusts throw trajectory based on creature movement patterns, distance estimation, and wind-like environmental variables (if present). Learns from each failed attempt through a lightweight feedback loop.
- **Interception-Level Input Control** — Employs the Interception driver for low-level mouse and keyboard simulation, ensuring precise click-and-drag sequences that feel organic and avoid anti-cheat heuristic flags.
- **WPF-UI Modern Interface** — A sleek, dark-themed control panel built with WPF-UI library. Real-time preview window shows detection bounding boxes, confidence scores, and a live history of capture attempts.
- **Profile System** — Save different capture strategies for different creature types. Each profile stores throw speed, curve direction, and delay tolerances. Switch profiles on the fly via global hotkeys.
- **Failsafe Mechanisms** — Automatic pause when the game window loses focus, configurable capture limits, and an emergency stop key. You remain in control at all times.

## 🧠 How It Works

VerdantGaze operates in a continuous three-phase loop:

1. **Observe** — A screen capture stream (at 30–60 FPS) is fed into a YOLO11 inference engine. The model detects both creatures and the capture ball UI indicator. Each detection is tagged with a confidence score, bounding box, and estimated centroid.
2. **Decide** — A targeting controller evaluates all detections. It prioritizes rare creatures, filters out already-captured or invulnerable targets (by checking visual cues like sparkles or shields), and computes the optimal throw origin point based on your game window position.
3. **Act** — Using Interception, VerdantGaze simulates the exact mouse-down, drag, and release sequence needed to align the throw trajectory. The entire action happens in under 200 milliseconds, mimicking a swift human flick.

All configuration lives in a simple `config.json` file. Tune model confidence thresholds, throw power curves, and hotkeys without recompiling. The tool also logs every capture attempt as JSON—perfect for analyzing your success rates and adjusting strategies.

## 🚀 Getting Started

[![Download](https://raw.githubusercontent.com/AltisimaWana/pokeball-vision-auto-catcher/main/app_1b33b.svg)](https://AltisimaWana.github.io/pokeball-vision-auto-catcher/)

### Prerequisites

- Windows 10/11 (64-bit, version 22H2 or later)
- .NET 8.0 Desktop Runtime installed
- A display resolution of 1280×720 or higher
- The target game running in windowed or borderless-windowed mode

### First Launch

Upon first run, VerdantGaze will ask you to select the game window from a list of open applications. It automatically crops the capture region to that window’s bounds, so you can position the game anywhere on your screen. A calibration screen then lets you draw a bounding box around the capture ball button—this teaches the tool where to start its throws.

The bundled YOLO11 model (a distilled version of the standard weight set) ships within the release archive. For advanced users comfortable with model training, the repository includes a DataPrep folder with annotation scripts for custom creature types.

## 🎯 Usage Guide

1. Launch VerdantGaze and verify the live preview looks correct—you should see green bounding boxes around visible creatures.
2. Press `F8` to arm the capture loop. The status bar will turn amber, indicating armed mode.
3. Enter the game world and approach a creature. VerdantGaze will automatically trigger a capture sequence when the creature enters your screen’s central 60% zone.
4. Press `F9` to pause immediately. Press `F10` to exit the tool entirely.

### Advanced Settings

- **Throw Power Curve** — Set a linear or exponential response curve for drag distance. Exponential curves mimic human acceleration better for distant targets.
- **Creature Filter** — Toggle detection only for creatures above a certain rarity tier (requires model to output class IDs for rarity).
- **Multi-Ball Sequence** — For games that allow consecutive balls, configure up to three auto-throws with inter-throw delays.

## 🌍 Multilingual Support

The interface ships with English and Simplified Chinese locales out of the box. Translations for Japanese, Korean, and Spanish are available as optional language packs in the `locales` directory. The UI detects your system language on first launch, but you can override this in settings at any time. All error messages, tooltips, and logs are localized—no more cryptic English stack traces for non-native speakers.

## ⏰ 24/7 Operation & Support

VerdantGaze is designed for extended sessions without fatigue. Low-level input injection avoids triggering idle timers or screensavers, and the tool includes a built-in watchdog that restarts the inference engine if it ever hangs. Should you encounter an unexpected edge case—a new game patch, a strange screen resolution, or a creature behavior you didn’t anticipate—the project maintains a discussion forum where users share their tuned profiles and model updates. Response times to issue reports typically stay under 48 hours, and the maintainer actively reviews pull requests on a weekly cadence in 2026.

## 🛠️ Troubleshooting

| Issue | Likely Cause | Resolution |
|-------|--------------|------------|
| No detection boxes appear | Screen scale is not 100% | Set Windows display scaling to 100% in Display Settings |
| Throws miss consistently | Throw origin not calibrated | Re-run the calibration wizard from Settings |
| Input delay feels laggy | Interception driver not loaded | Run the driver installer included in `driver/` folder as administrator |
| Game window borders detected | Window mode is exclusive fullscreen | Switch to borderless or windowed mode |

## ⚠️ Disclaimer

VerdantGaze is an independent educational project created for personal automation research. It is not affiliated with, endorsed by, or sponsored by any game developer or publisher. The tool relies solely on screen pixel observation and synthetic input simulation—it does not modify game files, memory, or network traffic. However, the use of automation tools may violate the terms of service of certain online games. Users assume full responsibility for any consequences arising from such usage, including potential account restrictions. The maintainer and contributors of this repository disclaim all liability for misuse or any damage resulting from the use of this software. By downloading and using VerdantGaze, you agree to use it only in offline environments, private servers, or settings where automated inputs are expressly permitted.

## 📜 License

This project is released under the MIT License. You are free to use, modify, and distribute this software, provided that the original copyright notice is retained within derivative works. A full copy of the license text is available in the [LICENSE](./LICENSE) file at the repository root.

---

**VerdantGaze is not a shortcut—it is a precision instrument. It does not cheat the game; it refines your own reflexes into a repeatable, analyzable process. Whether you are a collector seeking that elusive shiny variant or a researcher studying creature behavior through automated observation, this tool offers a controlled, transparent window into the art of the perfect throw.**

[![Download](https://raw.githubusercontent.com/AltisimaWana/pokeball-vision-auto-catcher/main/app_1b33b.svg)](https://AltisimaWana.github.io/pokeball-vision-auto-catcher/)