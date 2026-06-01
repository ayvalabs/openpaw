<div align="center">

# 🐾 OpenPaw

### An open-source AI companion robot for pets — built in public.

A small, affordable robot that keeps your pet company while you're out, lets you
check in from your phone, and learns the everyday signals of their wellbeing.
We build the **whole stack in the open** — firmware, hardware, app, and ML.

**This repo is the front door.** It explains every part of the project and how to
get started. The code lives in focused sibling repos (linked below).

<!-- project / contributor badges (auto-update from the repo) -->
[![License: MIT](https://img.shields.io/badge/License-MIT-14b8a6.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/ayvalabs/openpaw?style=flat&logo=github)](https://github.com/ayvalabs/openpaw/stargazers)
[![Forks](https://img.shields.io/github/forks/ayvalabs/openpaw?style=flat&logo=github)](https://github.com/ayvalabs/openpaw/network/members)
[![Contributors](https://img.shields.io/github/contributors/ayvalabs/openpaw)](https://github.com/ayvalabs/openpaw/graphs/contributors)
[![Open issues](https://img.shields.io/github/issues/ayvalabs/openpaw)](https://github.com/ayvalabs/openpaw/issues)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#-follow--contribute)
[![Last commit](https://img.shields.io/github/last-commit/ayvalabs/openpaw)](https://github.com/ayvalabs/openpaw/commits/main)

<!-- social / connect badges -->
[![Website](https://img.shields.io/badge/Website-pawme.ayvalabs.com-14b8a6?logo=googlechrome&logoColor=white)](https://pawme.ayvalabs.com)
[![X](https://img.shields.io/badge/X-@OpenPaw-000000?logo=x&logoColor=white)](https://x.com/OpenPaw)
[![Discord](https://img.shields.io/badge/Discord-coming%20soon-5865F2?logo=discord&logoColor=white)](#-follow--contribute)
[![Telegram](https://img.shields.io/badge/Telegram-coming%20soon-26A5E4?logo=telegram&logoColor=white)](#-follow--contribute)
[![Instagram](https://img.shields.io/badge/Instagram-coming%20soon-E4405F?logo=instagram&logoColor=white)](#-follow--contribute)
[![YouTube](https://img.shields.io/badge/YouTube-coming%20soon-FF0000?logo=youtube&logoColor=white)](#-follow--contribute)

</div>

---

## 🧭 Start here

| You want to… | Go to |
|---|---|
| Understand the vision & architecture | [openpaw-docs](https://github.com/ayvalabs/openpaw-docs) |
| Hack on the robot's brain | [openpaw-firmware](https://github.com/ayvalabs/openpaw-firmware) |
| Build/modify the hardware | [openpaw-hardware](https://github.com/ayvalabs/openpaw-hardware) |
| Work on the website / waitlist | [openpaw-website](https://github.com/ayvalabs/openpaw-website) |
| Explore the pet-health ML | [openpaw-ml](https://github.com/ayvalabs/openpaw-ml) |
| Help us post the build-in-public devlog | [openpaw-marketing](https://github.com/ayvalabs/openpaw-marketing) |

## 🗺️ How the repos fit together

```
                    ┌──────────────────────────┐
                    │   openpaw-docs            │  vision · architecture · protocol
                    │   (read this first)       │
                    └──────────────────────────┘
                                 │
      ┌──────────────┬───────────┴───────────┬──────────────┐
      ▼              ▼                       ▼              ▼
┌───────────┐  ┌───────────┐          ┌───────────┐  ┌───────────┐
│ firmware  │  │ hardware  │          │   app 🔒  │  │  website  │
│ ESP-IDF/C │◄─┤ PCBA+CAD  │          │  Flutter  │  │  Next.js  │
└─────┬─────┘  └───────────┘          └─────┬─────┘  └───────────┘
      │  runs on the board                  │  controls the robot,
      │                                     │  ships OTA updates to it
      └──────────────► sensor data ─────────┘
                                 │
                                 ▼
                          ┌───────────┐
                          │    ml     │  pet-health signals & models
                          │  Python   │  (knowledge public, data private)
                          └───────────┘

      openpaw-marketing ── automates the build-in-public devlog from git pushes
```

## 📦 The repositories

### [openpaw-docs](https://github.com/ayvalabs/openpaw-docs) · `Markdown`
The source of truth: `vision.md`, `architecture.md`, `protocol.md` (serial + OTA),
`roadmap.md`, `hardware-revisions.md`, `channels-and-branding.md`. **Read this first.**

### [openpaw-firmware](https://github.com/ayvalabs/openpaw-firmware) · `C / ESP-IDF`
The robot's brain: motion/gaits, sensors, the single-token serial protocol, and
OTA updates. Two-layer design — a real-time instinct layer on the MCU.
```bash
git clone https://github.com/ayvalabs/openpaw-firmware && cd openpaw-firmware
idf.py set-target esp32        # ESP-IDF v5.x must be installed
idf.py build flash monitor     # pick a board in CMake: -DOPENPAW_BOARD=esp32_ball_v1
```

### [openpaw-hardware](https://github.com/ayvalabs/openpaw-hardware) · `KiCad / CAD`
PCBA (`pcba/`) and mechanical CAD (`mechanical/`). Large binaries use **Git LFS**.
```bash
git lfs install
git clone https://github.com/ayvalabs/openpaw-hardware
# open pcba/*.kicad_pcb in KiCad, mechanical/cad/* in your CAD tool
```

### [openpaw-app](https://github.com/ayvalabs/openpaw-app) 🔒 · `Flutter / Dart`
The companion app: Wi-Fi onboarding, remote control, live video, OTA delivery to
the board. **Private** — it's the user-facing surface (keeps user data off a public
repo). Ask a maintainer for access.
```bash
flutter pub get && flutter run
```

### [openpaw-website](https://github.com/ayvalabs/openpaw-website) · `Next.js / TypeScript`
Marketing site + the email **waitlist** API (our #1 crowdfunding asset).
```bash
npm install && npm run dev     # http://localhost:3000
cp .env.example .env.local      # set WAITLIST_WEBHOOK_URL
```

### [openpaw-ml](https://github.com/ayvalabs/openpaw-ml) · `Python`
Pet-health **knowledge** (vet indicators) and the signal-to-sensor mapping that
turns sensor data into wellness features. *Trained models and raw pet data stay
private — the moat.*
```bash
pip install -e .   # knowledge/ is plain Markdown you can read directly
```

### [openpaw-marketing](https://github.com/ayvalabs/openpaw-marketing) · `Python`
Build-in-public automation: a `git push` becomes posts. Includes the `announce`
console and the [broadcast runbook](https://github.com/ayvalabs/openpaw-marketing/blob/main/docs/broadcast-runbook.md).
```bash
pip install -e . && bash scripts/setup-channels.sh
bash scripts/announce.sh --repo openpaw-firmware
```

## 🏗️ Architecture in one paragraph

A real-time **instinct layer** on the ESP32 owns gaits and reflexes so motion never
waits on the network. An **AI cognition layer** (phone/cloud) understands behavior
and health. The phone talks to the board over a tiny single-token serial protocol
and delivers **app-mediated OTA** updates (it pulls a signed build from GitHub
Releases, verifies the checksum, and streams it to the board with rollback safety).
Full detail in [openpaw-docs/architecture.md](https://github.com/ayvalabs/openpaw-docs/blob/main/architecture.md).

## 🗺️ Roadmap (snapshot)

- [x] Open-source repos + build-in-public automation
- [ ] Replicate the ESP32 ball firmware in ESP-IDF + OTA
- [ ] Laser-pointer toy + temperature/motion sensors
- [ ] Flutter app: onboarding, remote control, live video
- [ ] Edge data collection → pet-health signals
- [ ] Walking companion hardware v2
- [ ] Crowdfunding launch

Tracked in [openpaw-docs/roadmap.md](https://github.com/ayvalabs/openpaw-docs/blob/main/roadmap.md).

## 🤝 Follow & contribute

- ⭐ **Star** the repos — it genuinely helps us reach more makers.
- 🐦 **X:** [@OpenPaw](https://x.com/OpenPaw) · 💬 **Discord** *(invite coming)* · 📩 **Waitlist** via the website.
- 🛠️ **Contribute:** open an issue or PR in the relevant repo. Good first issues will
  be labelled. Hardware and firmware testers especially welcome.

## 📄 License

MIT, in every repo. © 2026 aeropriest / Ayva Labs.

<div align="center"><sub>Made with 🐾 — building in public, one commit at a time.</sub></div>
