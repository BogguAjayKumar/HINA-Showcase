# HINA (Hyper-Interactive Neural Assistant)
### Next-Generation Multimodal AI Voice Companion & Desktop Automation Agent

[![Status](https://img.shields.io/badge/Status-Under%20Active%20Development-orange?style=for-the-badge&logo=git)](https://github.com/BogguAjayKumar/HINA-Showcase)
[![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python)](https://python.org)
[![CUDA](https://img.shields.io/badge/NVIDIA%20CUDA-12.4-green?style=for-the-badge&logo=nvidia)](https://developer.nvidia.com/cuda-toolkit)
[![Speech](https://img.shields.io/badge/STT-Faster--Whisper-purple?style=for-the-badge)](https://github.com/SYSTRAN/faster-whisper)
[![Voice](https://img.shields.io/badge/TTS-Neural%20British%20Female-red?style=for-the-badge)](https://github.com/rany2/edge-tts)

> **⚠️ PROJECT STATUS: UNDER ACTIVE DEVELOPMENT**  
> *HINA is an ongoing open research and development project inspired by J.A.R.V.I.S. The core voice pipeline, vision engine, and OS automation framework have been developed from scratch with zero vendor lock-in. Active feature enhancements and hardware integrations are currently in progress.*

---

## 🌟 Overview

**HINA** (*Hyper-Interactive Neural Assistant*) is a modular, multimodal desktop companion and smart home controller designed to bridge conversational AI with physical operating system execution. 

Unlike conventional voice bots that rely on bloated third-party agent wrappers (like LangChain or CrewAI), HINA is **architected completely from scratch** around an asynchronous event loop, local CUDA-accelerated speech processing, full-duplex acoustic interruption, and direct OS/IoT tool invocation.

```
                              ┌────────────────────────────────────────┐
                              │      Microphone / Webcam / Screen      │
                              └────────────────────┬───────────────────┘
                                                   │
                        ┌──────────────────────────▼──────────────────────────┐
                        │      Local Perception Core (CUDA Accelerated)       │
                        │   • OpenWakeWord ("Hina") • Silero VAD (Barge-In)   │
                        │   • Faster-Whisper STT    • .NET Screen / Camera    │
                        └──────────────────────────┬──────────────────────────┘
                                                   │
                        ┌──────────────────────────▼──────────────────────────┐
                        │      HINA Agent Engine (Custom Orchestrator)        │
                        │   • SQLite Episodic Memory • Dynamic Tool Registry  │
                        │   • Multimodal Cloud Brain (Gemini 2.5/3.5/Flash)   │
                        └──────────┬────────────────────────────────┬─────────┘
                                   │                                │
        ┌──────────────────────────▼─────────────┐   ┌──────────────▼─────────────┐
        │        Action & Tool Dispatcher        │   │     Speech Output Engine   │
        │ • OS Execution & Powershell Automation │   │ • British Neural Voice     │
        │ • Web Browsing & Deep Search           │   │ • Full-Duplex Barge-In     │
        │ • Calendar & Email Management          │   │ • Acoustic Echo Gating     │
        │ • Home Assistant & MQTT IoT Hub        │   └────────────────────────────┘
        └────────────────────────────────────────┘
```

---

## 🎯 What We Have Achieved So Far

The following core subsystems have been developed, calibrated, and operationalized on local hardware:

### 1. Full-Duplex Voice Engine with Barge-In Interruption
* **Wake Word Trigger:** Instant acoustic activation on *"Hina"* or *"Hey Hina"* with both two-stage confirmation (*"Yes, sir?"*) and fluid one-shot commands (*"Hina, open notepad"*).
* **Barge-In Interruption:** Powered by Silero Voice Activity Detection (VAD). If HINA is actively speaking through your speakers and you start talking, she immediately cuts off playback and listens to you.
* **Acoustic Feedback Protection:** Dynamic energy filtering and buffer draining prevent laptop speaker bleed from triggering false self-interruptions.

### 2. GPU-Accelerated Local Speech-to-Text (STT)
* **Zero Cloud Latency for Voice:** Powered by `faster-whisper` running locally on **NVIDIA RTX GPUs** with FP16 tensor acceleration.
* **Automatic Gain Normalization:** Custom signal amplification boosts quiet laptop microphone arrays by up to 10×, allowing Whisper to accurately transcribe speech from across the room.
* **Prompt Biasing:** Neural decoding is conditioned on domain vocabulary (`Hina`, `system status`, `screen`, `open`) to achieve near-zero false transcription rates.

### 3. Natural British Neural Female Voice (TTS)
* **Primary Engine:** Studio-grade British Neural Female Voice (`en-GB-SoniaNeural`), generating expressive speech with sub-200ms streaming playback.
* **Local Fallback:** Windows Speech API (`Microsoft Zira Desktop`) for offline speech generation.

### 4. Multimodal Screen & Webcam Perception
* **Real-Time Screen Awareness:** High-speed desktop frame grabber using Windows .NET GDI/Graphics, completely immune to display scaling and GPU switching issues.
* **Webcam Integration:** Real-time OpenCV video frame capture.
* **Multimodal Reasoning:** Sends high-resolution visual frames directly into Gemini's vision engine to diagnose compile errors, explain code, read browser tabs, or describe physical objects shown to the camera.

### 5. 20 Dynamic Desktop & OS Automation Tools
* **System Control:** Non-blocking application launcher (`open_application`), PowerShell process runner, and real-time GPU/RAM/CPU hardware monitoring.
* **Web & Search:** Real-time search engine integration (`search_web`), webpage content extraction & summarization (`fetch_webpage`), and browser automation.
* **Calendar & Schedule:** Persistent SQLite-backed calendar manager (`get_calendar_events`, `add_calendar_event`, `delete_calendar_event`).
* **Email Suite:** Live IMAP email reading and SMTP dispatching (`check_emails`, `send_email`).
* **Filesystem:** Direct file search, reading, writing, and directory navigation.

### 6. Smart Home & IoT Hub
* **Home Assistant Integration:** Entity discovery and REST API control for lights, switches, media players, and climate units.
* **Direct MQTT Support:** Raw MQTT payload publishing for local microcontrollers (ESP32, Tasmota, Zigbee2MQTT).

### 7. Persistent Episodic Memory
* **Local Storage:** Automatic SQLite database logging recent conversation turns, user preferences, and persistent facts in `data/hina_memory.db`.

---

## 🗣️ Supported Voice Commands (Live Demonstration)

| Voice Command | Action Executed by HINA |
| :--- | :--- |
| *"Hina, open my notepad."* | Cleans conversational prefixes, resolves `notepad.exe`, launches it non-blockingly, and confirms speech output. |
| *"Hina, open youtube.com."* | Detects web domain and opens YouTube in the default system browser. |
| *"Hina, what is my system status?"* | Queries `nvidia-smi` and Windows CIM instances; speaks back GPU temperature, VRAM usage, and RAM load. |
| *"Hina, look at my screen and tell me what you see."* | Snaps desktop display, analyzes the window layout and code with multimodal vision, and provides verbal feedback. |
| *"Hina, schedule Project Demo for tomorrow at 3 PM."* | Stores the meeting in the persistent SQLite calendar database and confirms the time. |
| *"Hina, search the web for the latest Python news."* | Runs live DuckDuckGo query, extracts the top search snippets, and speaks a concise 2-sentence summary. |

---

## ⚡ Latency & Performance Benchmarks

*Benchmarked on an Intel Core i7 / NVIDIA GeForce RTX 5050 Laptop GPU (8GB VRAM) running Windows 11:*

| Pipeline Stage | Technology | Average Latency |
| :--- | :--- | :--- |
| **Wake Word Detection** | OpenWakeWord + VAD Spotting | ~35 ms |
| **Speech-to-Text (STT)** | Faster-Whisper (`base.en` on CUDA) | ~110 ms |
| **Reasoning & Tool Selection** | Gemini Flash-Lite / 3.5-Flash | ~450 ms |
| **Text-to-Speech (TTS)** | Edge-TTS Neural Streaming | ~180 ms |
| **Total Voice-to-Voice Loop** | Full Duplex Pipeline | **~775 ms** |

---

## 🗺️ Project Roadmap

- [x] Architecture design from scratch (Zero LangChain / CrewAI bloat)
- [x] GPU-accelerated local STT (Faster-Whisper on CUDA)
- [x] Full-duplex audio stream with barge-in interruption & echo suppression
- [x] British Neural Female Speech Synthesizer
- [x] Desktop & OS Automation suite (20 registered tools)
- [x] Multimodal screen and webcam perception
- [x] Smart home integration (Home Assistant & MQTT)
- [ ] 3D Cybernetic holographic UI overlay (DirectX / Modern Web HUD)
- [ ] Fully offline local LLM brain option (Llama 3.2 8B / Qwen 2.5 on RTX GPU)
- [ ] Proactive situational awareness (Time-based autonomous check-ins)

---

## 🔒 Privacy & Data Ownership

* **RAM-Only Voice Processing:** Voice input is processed exclusively in transient RAM buffers. **Zero audio recordings are saved to disk.**
* **Local GPU Inference:** Whisper transcription runs 100% offline on your local GPU. Raw microphone audio is never uploaded to any cloud server.
* **Local Memory Database:** Conversation history and calendar items remain strictly within your local machine.

---

## 📜 License & Acknowledgments

This showcase repository is distributed under the **MIT License**.  
Developed by **Boggu Ajay Kumar** as an advanced exploration of agentic computing, real-time audio systems, and multimodal human-machine interaction.
