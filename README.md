# ⚓ Athena at the Helm — Multimodal FaceTime AI Naval Co-Pilot

> **Built for HackUTA 2026 — Homer's Odyssey Track**  
> *Surviving perilous waters not through brute force, but through cunning, strategy, and real-time divine guidance.*

---

## 🌊 Overview

**Athena at the Helm** turns a live **FaceTime voice & video call** into an interactive, multimodal co-pilot for a 3D naval combat game built in **Unreal Engine**. 

When manual sailing isn't enough to survive enemy broadsides, players call upon an AI co-pilot powered by **Gemini Live** over FaceTime. Instead of just chatting, the AI acts as an **Athena / Oracle navigator** with two real-time superpowers:
1. **Hands-Free Ship Piloting:** It takes direct control of the helm—chaining rapid combat maneuvers (`steer`, `accelerate`, `fire`) to turn a losing battle into a victory.
2. **Live On-Call Visuals:** Whenever you ask, the AI **renders and displays custom visuals directly inside the FaceTime call**—from Odyssey voyage maps and tactical flanking diagrams to celebratory victory cards.

---

## ✨ Key Features

- **🎙️ Live FaceTime AI Co-Pilot:** Talk naturally with a low-latency Gemini Live voice agent over FaceTime (`barge-in` enabled for instant tactical overrides).
- **🖼️ Live On-Call Visual Generation & Display:** Ask the AI to show you whatever you need mid-call—voyage charts, battle breakdowns, or custom graphics pop up directly on your FaceTime screen in real time.
- **⚡ Burst Command Piloting:** Overcomes voice/network latency by chaining multi-step tactical sequences (`steer_left`, `steer_right`, `accelerate`, `fire`, `combat_burst`) in a single tool execution.
- **🚢 3D Unreal Engine Naval Combat:** Real-time ship physics, cannon broadsides, and enemy fleet AI built in Unreal Engine.
- **🔇 Silent Observer Architecture:** Browser/bridge audio stays muted while the game listens to LiveKit data channels, ensuring zero echo and clean FaceTime audio.

---

## 🏗️ System Architecture

Two decoupled applications communicate in real time over a shared **LiveKit** room (`pirate-battle`):

```text
┌───────────────────────────┐       ┌──────────────────────────┐       ┌──────────────────────────┐
│   FaceTime Call (User)    │──────▶│  Gemini Live Voice Agent │──────▶│   LiveKit Data Channel   │
│  Voice + Live Visual UI   │◀──────│  (Chert + control_ship + │       │  Room: "pirate-battle"   │
│  (Maps, Charts, Graphics) │       │   Visual Display Tool)   │       └────────────┬─────────────┘
└───────────────────────────┘       └──────────────────────────┘                    │
                                                                       Reliable JSON Packets
                                                                         (`ship_command`)
                                                                                    ▼
                                                                       ┌──────────────────────────┐
                                                                       │  Unreal Engine 3D Game   │
                                                                       │   (Silent Listener +     │
                                                                       │    Live Ship Controls)   │
                                                                       └──────────────────────────┘
