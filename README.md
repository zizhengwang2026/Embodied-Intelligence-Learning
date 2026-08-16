<div align="center">

<h1 style="font-size:42px; margin-bottom:4px;">🤖 Embodied Intelligence</h1>

<p style="font-size:17px; color:#475569;"><i>Open-source, hands-on notes & reproducible projects for learning Embodied AI from zero — built by a mechanical-engineering grad student crossing into robotics.</i></p>

<br/>

<p>
  <a href="#-what-is-this"><img src="https://img.shields.io/badge/About-6366F1?style=for-the-badge" alt="about"/></a>
  <a href="so101-act/README.md"><img src="https://img.shields.io/badge/SO--101%20%E3%80%9C%20ACT-22C55E?style=for-the-badge" alt="so101"/></a>
  <a href="#-study-log--plan"><img src="https://img.shields.io/badge/Study%20Log-F59E0B?style=for-the-badge" alt="studylog"/></a>
  <a href="#-roadmap"><img src="https://img.shields.io/badge/Roadmap-F59E0B?style=for-the-badge" alt="roadmap"/></a>
  <a href="mailto:zizhengwang2026@gmail.com"><img src="https://img.shields.io/badge/Contact-EA4335?style=for-the-badge" alt="contact"/></a>
</p>

<p>
  <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" alt="license"/>
  <img src="https://img.shields.io/badge/last%20updated-2026--08--16-blue?style=flat-square" alt="updated"/>
  <img src="https://img.shields.io/badge/language-English-8B5CF6?style=flat-square" alt="lang"/>
  <img src="https://komarev.com/ghpvc/?feed=zizhengwang2026-embodied-intelligence" alt="views"/>
</p>

</div>

---

## 🧭 What is this

This repository is a **public learning lab** for *Embodied Intelligence* — the branch of AI where an agent carries a **body** and closes the loop of **perceive → decide → act** in the physical world.

Everything here is written from real, hands-on experience (a two-day on-site robotics bootcamp), not from textbooks. The goal is simple: **let anyone clone this and reproduce a working embodied-AI pipeline on real hardware**, and understand *why* each step exists.

> 💡 *"Embodied intelligence is the discipline of the body. You cannot learn it by reading papers — you have to bend a servo with your own hands."*

> 🚀 **My end-to-end embodied-intelligence journey (the red thread of this repo):** I ran the *whole* stack on real SO-101 hardware — **environment → flashing firmware → wiring → calibration → teleoperation & data collection → imitation learning (BC) → ACT / Diffusion-Policy algorithms → real-hardware deployment & on-site debugging**. The [`so101-act/`](so101-act/README.md) project documents every single stage.

## 📦 Projects in this repo

| Project | What it is | Status |
|---|---|---|
| **[`so101-act/`](so101-act/README.md)** | Full pipeline: SO-101 dual-arm + D-Robotics S600 + LeRobot + ACT imitation learning, run on **real hardware** | ✅ Complete |
| `soft-gripper-il` | (Planned) Soft gripper + force/tactile feedback + ACT — bridging to soft-robotics research | 🔜 Soon |

## 📓 Study Log & Plan

A structured **60-day learning track** built on the 黑马程序员《具身智能》223-ep course, plus day-by-day lecture notes (knowledge points, principles, hands-on steps, pitfalls, and first-person reflections).

- **[`study-plan-60d.md`](study-plan-60d.md)** — the full 60-day, 11-phase plan (all 223 episodes mapped to days).
- **Lecture notes (`study-log/`):**
  - [Lecture 01 — What is Embodied Intelligence? (EN)](study-log/2026-08-15-lecture-01-en.md) · [中文](study-log/2026-08-15-lecture-01-zh.md)
  - [Lecture 02 — Actuators, Gears, Sensors & 3D Printing (EN)](study-log/2026-08-15-lecture-02-en.md) · [中文](study-log/2026-08-15-lecture-02-zh.md)
  - [Lecture 03 — Virtual Simulation & URDF (EN)](study-log/2026-08-16-lecture-03-en.md) · [中文](study-log/2026-08-16-lecture-03-zh.md)

## 🗺️ Roadmap

- [x] Reproducible SO-101 × ACT pipeline (collect → train → infer)
- [x] Algorithm deep-dives: ACT, IL, RL, VLA, World Model
- [x] Real troubleshooting log from the field
- [ ] Force / tactile sensing demo
- [ ] Soft-gripper imitation grasping with compliance control
- [ ] Sim-to-Real gap analysis for soft bodies

## 👤 Author

**Zizheng Wang** — MSc candidate, Mechanical Engineering, Zhejiang University.
Background in soft robotics; currently building toward the intersection of **soft bodies + embodied AI**.

<p>
  <a href="https://github.com/zizhengwang2026">GitHub</a> ·
  <a href="mailto:zizhengwang2026@gmail.com">Email</a> ·
  <a href="https://blog.csdn.net/ZizhengWang2023">Blog</a>
</p>

<sub>Built with curiosity. Last updated 2026-08-16.</sub>
