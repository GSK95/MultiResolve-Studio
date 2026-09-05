# MultiResolve Studio

A lightweight, high-performance multicam live production switcher and isolated recording suite built with C++ and Qt6. MultiResolve Studio bridges the gap between live switching and post-production by combining multi-source ingestion, hardware-accelerated ISO recording, and browser-based remote control with automatic FCP7 XML generation—turning your live cuts into ready-to-edit Adobe Premiere Pro timelines instantly.

---

## Overview
MultiResolve Studio is an advanced live production, recording, and mixing suite (multicam video switcher) built with C++ and the Qt6 framework. It provides a studio-grade interface reminiscent of vMix, OBS Studio, and ATEM Software Control, with a dedicated focus on hardware-accelerated **ISO recording** (isolated track recording) and automated **Timeline XML (FCP7)** generation for fast post-production workflows in NLEs like Adobe Premiere Pro.

## Project Status: Beta-Ready
The application is stable and fully functional for capturing, switching, and synchronizing multi-channel video and audio inputs.

**Recent Updates:**
* Overhauled interface into a classic **Studio Mode** layout (left-hand PREVIEW Multiview Grid, right-hand PROGRAM monitor).
* Corrected color space handling with native BGRA/RGBA channel mapping.
* Integrated SDL2 for enhanced low-latency audio capture and management.
* Optimized frame switching logic for the CUT transition bus.

---

## Core Features

### 1. Studio Interface
* **Multicam Grid (Preview):** Real-time monitoring grid displaying all active input feeds simultaneously.
* **Program Monitor:** Dedicated master display for the live switched output.
* **Transition Controls:** Centralized switching deck featuring hardware-style CUT and REC buttons, with hotkey triggers (`1`–`9`) for instant camera switching.

### 2. Source Management
* **DirectShow & Media Foundation Ingestion:** Native capture pipeline for USB capture cards, webcams, and professional video inputs with custom resolution and framerate negotiation.
* **Screen Capture:** Low-overhead desktop display capture powered by Windows GDI integration with automatic pixel format conversion.
* **Audio Capture & Mixing:** Multi-device master audio input via WASAPI, complete with real-time peak-level metering and master gain controls.

### 3. ISO Recording & Synchronization
* **Simultaneous Track Recording:** Activating master REC spins up parallel isolated capture pipelines:
  * Generates independent MP4 files for every active video source via hardware-accelerated Windows Media Foundation encoders (`MFEncoder`).
  * Captures a synchronized, uncompressed master WAV audio track.
* **Cut Event Logging:** In-memory metadata logger tracking frame-accurate switching timestamps across the entire session.

### 4. Premiere Pro Timeline Integration
* **Instant XML Assembly:** Automates multi-camera post-production by exporting industry-standard FCP7 XML files on session completion.
* **Synchronized Conforming:** Importing the XML into Adobe Premiere Pro automatically stacks all ISO video and audio tracks, applying pre-cut timeline edits that match live switching decisions frame-for-frame.

### 5. Remote Web Control
* **Embedded Web Server:** Lightweight, integrated HTTP server (`cpp-httplib`) listening on port `8080` for remote tablet and smartphone operation.
* **Low-Latency Video Preview:** Delivers a compressed 480p MJPEG preview feed to the browser to preserve local rendering resources.
* **REST API Control:** Web endpoints for triggering CUT actions and toggling ISO recording.
* **Instant Pairing:** In-app QR code generation allows mobile devices on the local network to pair instantly without manual IP entry.

### 6. Engine Optimization
* Multithreaded UI and ingestion pipeline decoupling frame processing from the Qt6 event loop.
* Dynamic aspect ratio preservation using custom `QSizePolicy` bounds to eliminate display distortion.

---

## Build Instructions

MultiResolve uses **CMake** as its build generation system and targets the **MSVC** toolchain on Windows.

### Dependencies
* **Qt 6.x** (`Core`, `Gui`, `Widgets`, `OpenGLWidgets`, `Network`, `Concurrent`)
* **SDL2** (Fetched automatically during configuration via CMake `FetchContent`)
* **qrcodegen** (Included in `vendor/`)
* **cpp-httplib** (Included in `vendor/`)
* **Windows SDK** (`DirectShow`, `mfplat`, `mfreadwrite`, `mfuuid`)

### Windows Build Steps
1. Clone the repository:
   ```bash
   git clone [https://github.com/your-username/MultiResolve-Studio.git](https://github.com/your-username/MultiResolve-Studio.git)
   cd MultiResolve-Studio
