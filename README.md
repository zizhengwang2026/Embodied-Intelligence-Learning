<div align="center">

<h1 style="font-size:42px; margin-bottom:4px;">🤖 Embodied Intelligence</h1>

<p style="font-size:17px; color:#475569;"><i>Open-source, hands-on notes & reproducible projects for learning Embodied AI from zero — built by a mechanical-engineering grad student crossing into robotics.</i></p>

<br/>

<p>
  <a href="#-what-is-this"><img src="https://img.shields.io/badge/About-6366F1?style=for-the-badge" alt="about"/></a>
  <a href="so101-act/README.md"><img src="https://img.shields.io/badge/SO--101%20%E3%80%9C%20ACT-22C55E?style=for-the-badge" alt="so101"/></a>
  <a href="#-study-log--plan"><img src="https://img.shields.io/badge/Study%20Log-F59E0B?style=for-the-badge" alt="studylog"/></a>
  <a href="#-60-day-learning-roadmap"><img src="https://img.shields.io/badge/Roadmap-F59E0B?style=for-the-badge" alt="roadmap"/></a>
  <a href="mailto:zizhengwang2026@gmail.com"><img src="https://img.shields.io/badge/Contact-EA4335?style=for-the-badge" alt="contact"/></a>
</p>

<p>
  <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" alt="license"/>
  <img src="https://img.shields.io/badge/last%20updated-2026--10--15-blue?style=flat-square" alt="updated"/>
  <img src="https://img.shields.io/badge/language-English%20%2F%20%E4%B8%AD%E6%96%87-8B5CF6?style=flat-square" alt="lang"/>
  <img src="https://komarev.com/ghpvc/?feed=zizhengwang2026-embodied-intelligence" alt="views"/>
</p>

</div>

---

## 🧭 What is this

This repository is a **public learning lab** for *Embodied Intelligence* — the branch of AI where an agent carries a **body** and closes the loop of **perceive → decide → act** in the physical world.

Everything here is written from real, hands-on experience (a two-day on-site robotics bootcamp + a structured 60-day course study), not from textbooks. The goal is simple: **let anyone clone this and reproduce a working embodied-AI pipeline on real hardware**, and understand *why* each step exists.

> 💡 *"Embodied intelligence is the discipline of the body. You cannot learn it by reading papers — you have to bend a servo with your own hands."*

> 🚀 **My end-to-end embodied-intelligence journey (the red thread of this repo):** I ran the *whole* stack on real SO-101 hardware — **environment → flashing firmware → wiring → calibration → teleoperation & data collection → imitation learning (BC) → ACT / Diffusion-Policy algorithms → real-hardware deployment & on-site debugging**. The [`so101-act/`](so101-act/README.md) project documents every single stage.

## 📦 Projects in this repo

| Project | What it is | Status |
|---|---|---|
| **[`so101-act/`](so101-act/README.md)** | Full pipeline: SO-101 dual-arm + D-Robotics S600 + LeRobot + ACT imitation learning, run on **real hardware** | ✅ Complete |
| `soft-gripper-il` | (Planned) Soft gripper + force/tactile feedback + ACT — bridging to soft-robotics research (DEA actuators) | 🔜 Soon |

## 📓 Study Log & Plan

A structured **60-day learning track** built on the 黑马程序员《具身智能》223-ep course, plus day-by-day lecture notes (knowledge points, principles, hands-on steps, pitfalls, and first-person reflections). **All 126 notes (Day 1–63) are bilingual (中文 / English).** That's 120 notes for the 60-day course (Day 1–60), plus 6 more across 3 self-study extension chapters (Day 61–63) on deployment, integration, and connecting the material to my own soft-robotics research.

- **[`study-plan-60d.md`](study-plan-60d.md)** — the full 60-day, 11-phase plan (all 223 episodes mapped to days).
- **[`study-log/README.md`](study-log/README.md)** — the complete index of all 126 notes (Day 1–63), grouped by phase.
- **Lecture notes (`study-log/`):** every day has a 中文 and an English version, e.g.
  - [Day 1 — Embodied-Intelligence Definition & Research Landscape (EN)](study-log/2026-08-15-Embodied-Intelligence-Definition-and-Research-Landscape-en.md) · [中文](study-log/2026-08-15-具身智能定义与研究版图-zh.md)
  - [Day 2 — Robot Hardware: Actuators, Gears, Sensors & 3D (EN)](study-log/2026-08-15-Robot-Hardware-Actuators-Reduction-Encoders-en.md) · [中文](study-log/2026-08-15-机器人硬件实体-执行器减速编码器-zh.md)
  - [Day 57 — RL Five Key Concepts & MDP (EN)](study-log/2026-10-09-RL-Five-Key-Concepts-and-MDP-Markov-Decision-Process-en.md) · [中文](study-log/2026-10-09-强化学习五大概念与MDP马尔可夫决策过程-zh.md)
  - [Day 63 — Soft Actuators × Embodied AI (EN)](study-log/2026-10-15-Soft-Actuators-and-Embodied-AI-Research-Direction-DEA-en.md) · [中文](study-log/2026-10-15-软体执行器与具身智能研究方向衔接DEA-zh.md)

## 🗺️ 60-Day Learning Roadmap

The 223-lecture course is re-arranged into **11 phases (P1–P11)** by difficulty. Each phase maps to a range of days and episode numbers.

| Phase | Theme | Episodes | Days | What you'll learn |
|------|-------|----------|------|-------------------|
| P1 | Concepts & system architecture | 001–007 | Day 1 | What embodied AI *is*; the perceive→decide→act loop |
| P2 | Hardware: actuators, gears, sensors, 3D | 008–012 | Day 2 | Servos, motors, encoders, printed structures |
| P3 | Virtual simulation & URDF modeling | 013–026 | Day 3–5 | Build a robot arm in simulation |
| P4 | Comms / calibration / WebSocket | 027–050 | Day 6–11 | Talk to real hardware, calibrate, stream angles |
| P5 | Kinematics: FK & IK | 051–067 | Day 12–16 | Map joint angles ↔ end-effector pose |
| P6 | Control theory & PID | 068–080 | Day 17–20 | Closed-loop control, tune a PID, teleop |
| P7 | Computer vision (OpenCV) | 081–115 | Day 21–28 | Cameras, color/shape detection, hand-eye calibration |
| P8 | ML / DL / YOLO | 116–160 | Day 29–41 | Supervised learning, CNNs, real-time detection |
| P9 | Speech / LLM / Ollama / MCP | 161–187 | Day 42–50 | Make the robot hear, think (local LLM), and act via MCP |
| P10 | Behavior Cloning (ALOHA / data / train) | 188–207 | Day 51–56 | Imitation learning end-to-end on real arms |
| P11 | Reinforcement Learning / Genetic NN | 208–223 | Day 57–60 | Q-learning, DQN, the RL mindset, wrap-up |
| ➕ | **Extension (self-study)** | — | Day 61–63 | Sim-to-Real, integrated-project design, soft-actuator research link |

> Full episode-to-day mapping: see [`study-plan-60d.md`](study-plan-60d.md). Full note index: see [`study-log/README.md`](study-log/README.md).

## 🧭 Project Roadmap

- [x] Reproducible SO-101 × ACT pipeline (collect → train → infer)
- [x] Algorithm deep-dives: ACT, IL, RL, VLA, World Model
- [x] Real troubleshooting log from the field
- [x] 60-day / 120-note course study + 3 extension chapters (Day 61–63)
- [ ] Force / tactile sensing demo
- [ ] Soft-gripper imitation grasping with compliance control
- [ ] Sim-to-Real gap analysis for soft bodies

## 📌 Notes

- **Zero military content.** This is a general embodied-AI study repo — no defense or weapons material.
- **DEA cross-link.** The author's research is in soft robotics (Dielectric Elastomer Actuators). DEA appears only as a *light* cross-link inside the notes, never on the main line.

## 👤 Author

**Zizheng Wang** — MSc candidate, Mechanical Engineering, Zhejiang University.
Background in soft robotics; currently building toward the intersection of **soft bodies + embodied AI**.

<p>
  <a href="https://github.com/zizhengwang2026">GitHub</a> ·
  <a href="mailto:zizhengwang2026@gmail.com">Email</a> ·
  <a href="https://blog.csdn.net/ZizhengWang2023">Blog</a>
</p>

<sub>Built with curiosity. Last updated 2026-10-15.</sub>
