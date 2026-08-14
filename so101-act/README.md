<div align="center">

<style>
@keyframes pulse { 0%{opacity:.4} 50%{opacity:1} 100%{opacity:.4} }
.live { display:inline-block; width:9px; height:9px; border-radius:50%; background:#22C55E; animation:pulse 1.6s infinite; margin-right:6px; vertical-align:middle; }
</style>

<h1 style="font-size:38px; margin-bottom:2px;">🦾 SO-101 × ACT</h1>
<h3 style="font-weight:400; color:#475569; margin-top:0;">Real-Hardware Imitation Learning Pipeline</h3>

<p style="font-size:15px; color:#334155;"><i>SO-101 dual-arm · D-Robotics S600 · HuggingFace LeRobot · ACT (Action Chunking Transformer)</i></p>

<p>
  <a href="#-why-this-is-embodied-intelligence">Why</a> ·
  <a href="#-hardware-stack">Hardware</a> ·
  <a href="#-software-stack">Software</a> ·
  <a href="#-the-teleoperation-loop">Teleop</a> ·
  <a href="#-full-pipeline">Pipeline</a> ·
  <a href="#-act-deep-dive">ACT</a> ·
  <a href="#-troubleshooting">Fixes</a> ·
  <a href="#-star-for-your-resume">STAR</a>
</p>

<p>
  <span class="live"></span><b>Status: reproducible on real hardware</b>
  &nbsp;·&nbsp; <img src="https://img.shields.io/badge/DOF-6-brightgreen" alt="dof"/>
  &nbsp; <img src="https://img.shields.io/badge/algorithm-ACT-8B5CF6" alt="algo"/>
  &nbsp; <img src="https://img.shields.io/badge/framework-LeRobot-FFD21E" alt="fw"/>
</p>

</div>

---

## 🌟 What you will build

A robotic arm that **sees an object with cameras and grasps it autonomously** — learned purely from your own demonstrations, no hand-coded control.

This is the canonical **perceive → decide → act** embodied-AI loop, executed on **physical hardware**, not a simulation.

> ⚑ *Not a tutorial you watch. A pipeline you run. Every command, voltage, and error below came from a real two-day bootcamp.*

---

## 🧠 Why this IS "Embodied Intelligence"

<div style="background:linear-gradient(135deg,#0f172a,#312e81); padding:22px 26px; border-radius:16px; color:#E2E8F0;">

**Embodied Intelligence** = an agent that carries a *body* and closes the loop **sense → decide → act** in the physical world.

Its key difference from "ordinary AI" (which only processes pixels or text): **the intelligence lives on the body, and it learns by trying with the body.**

| Ordinary AI | Embodied AI |
|---|---|
| Input: image / text | Input: **camera pixels + joint angles (proprioception)** |
| Output: label / sentence | Output: **motor commands (torque / target angle)** |
| Lives in a server | **Lives on a physical body** in the real world |
| No consequence of error | Error = the arm hits itself |

The SO-101 pipeline *is* this loop made physical: cameras sense → ACT decides → servos act → cameras sense again.

</div>

---

## 🛠️ Hardware Stack

### 🧠 D-Robotics S600 (RDK edge-AI board)
The robot's **"brain computer"** — runs the model, talks to servos, receives cameras.

| Property | Detail | Interview point |
|---|---|---|
| Arch | ARM **aarch64** (64-bit ARM) | Must install **aarch64** Miniconda — x86 build won't run (real pitfall) |
| OS | RDK OS (custom Linux, real-time rt-patch) | Real-time matters for robot control |
| Role | Run LeRobot, load ACT, do inference | All training/inference here; your laptop is just a display |
| I/O | UART (servo bus) · USB (cameras) · Ethernet/WiFi (SSH) | Two media differ: PC↔S600 = network(SSH), S600↔servo = UART wire |
| AI accel | On-board BPU/NPU | Faster than CPU for real-time vision policy |

**Field milestone:** `XBurn` flash `product.zip` (~7.9 GB firmware) → board reboots → SSH in (MobaXterm / VS Code / serial `plink`) → run LeRobot. That *is* a micro embedded-deployment exercise.

### 🦾 SO-101 manipulator (HuggingFace LeRobot reference arm)
Open-source, desktop-class, 6-DOF, ideal for imitation-learning data collection.

| Param | Value | Note |
|---|---|---|
| DOF | **6 DOF** | 5 arm joints + 1 gripper |
| Actuator | Feetech **STS3215** serial-bus servo | 12-bit magnetic encoder, daisy-chain |
| Reach | ~500 mm | base → gripper tip |
| Payload | ~250–500 g | enough for soft grasping |
| Weight | ~800 g | PLA structure |
| Joints | all revolute | URDF open → MuJoCo / PyBullet sim |
| Comm | USB serial `/dev/ttyACM*` | bus baud 1 Mbps |
| Power | see voltage below | Std = 5V all; Pro = leader 5V / follower 12V |

**The 6 joints** (you calibrate these): `shoulder_pan`, `shoulder_lift`, `elbow_flex`, `wrist_flex`, `wrist_roll`, `gripper`. Note `wrist_roll` is continuous-rotation — calibrated separately.

### ⚡ Voltage detail — Leader 5V / Follower 12V (memorize this)

<div style="background:#FEF3C7; border-left:5px solid #F59E0B; padding:14px 18px; border-radius:10px;">

**SO-101 Pro kit (bootcamp standard):** Leader arm = **5V** supply + 7.4V servo; Follower arm = **12V** supply + 12V servo. Standard kit: both 5V.

**Why (must be able to explain):** the *follower* must generate large torque to actually grasp objects → 12V high-torque servo. The *leader* is only guided by your hand and must feel *compliant/smooth* → 5V/7.4V low-voltage servo.

**⚠ Danger:** a 12V servo on 5V = weak; a 7.4V servo on 12V = **burned out!** Always match leader/follower to its correct supply.

**Mnemonic:** *"The mover (follower) needs power → 12V; the one being bent (leader) needs smoothness → 5V."*

</div>

### 🔁 Leader vs Follower — a "demo hand" and an "executor hand"

| | Leader (you bend) | Follower (acts automatically) |
|---|---|---|
| Who moves | your hand | commanded |
| Gripper | usually none | yes (real grasp) |
| Voltage / servo | 5V / 7.4V compliant | 12V / high-torque |
| Servo mode | low torque, reports angle when bent | high torque, rotates to target |
| Role | **sensor** (reports angle) | **actuator** (does motion) |
| Port | `leader_port` (e.g. `/dev/ttyACM1`) | `follower_port` (e.g. `/dev/ttyACM0`) |

The two arms look identical (both 6-joint) and joints pair 1-to-1, but they are **not physically linked** — both connect to the S600, which relays between them.

### 📷 Cameras — the robot's "eyes"
- **Top camera** `topcam`: above the table, `/dev/video0`
- **Wrist camera** `wristcam`: on follower wrist, `/dev/video1`
- Both USB to S600; code uses `cv2.VideoCapture(0)` / `(1)`.
- A camera only turns light into a pixel matrix — **it does not think**. Learning happens in the model, not the camera.

### 🔌 Connection topology (one diagram to remember)

```
        Network (SSH)                UART wire (TTL)              USB
  PC ───────────────► S600 ───────────────────► Servo bus ──► 6× STS3215
                       │  (relay: read leader → write follower)
                       └────────────────────► Cameras (top + wrist)
```

> **One sentence:** PC↔S600 = network(SSH) · S600↔servo = UART wire · S600↔camera = USB. Three media, each its own job.

---

## 💻 Software Stack

| Tool | Role | Why it matters |
|---|---|---|
| **LeRobot** (HuggingFace) | Unified framework: calibrate / record / train / deploy | No need to write comm protocol — framework handles servo read/write/dataset |
| **Miniconda** | Isolated Python env | Avoids `externally-managed-environment` (PEP 668) on Debian |
| **MobaXterm** | SSH terminal + SFTP drag-drop | Log into S600, drag model folder |
| **VS Code Remote-SSH** | Graphical remote edit/run | Same `drobot`, nicer to code in |
| **plink / serial** | Console when no network | `plink -serial COM10` to read IP |
| **XBurn** | Flash S600 firmware | "Reinstall the OS" on the board |
| **OpenCV (cv2)** | Camera capture | `VideoCapture(0/1)` → frames |
| **ACT** | The trained model | Action Chunking + CVAE + Transformer |

Dataset format: **Parquet** (joint states) + **video** (camera frames) → push to HuggingFace Hub. Device flag: `--teleop.type=so101_leader / so101_follower`.

---

## 🔁 The Teleoperation Loop

You asked *"what connects the two arms?"* — answer: **both connect to S600**, and the board synchronizes them ~30–50×/sec by **read → copy → send**. Not a physical rod.

```
  read      copy      send
leader ──► S600 ──► follower
(30–50 Hz)
```

1. **READ:** S600 sends `read ID:1` on bus A; leader servo 1 replies `30°`; read all 6 joints → `[30°,45°,10°,…]`
2. **COPY:** use that angle vector directly as the follower's 6-joint target
3. **SEND:** S600 sends `write ID:1→30°…` on bus B; follower servos PID to target and lock

Because one cycle is only milliseconds, the two *feel* synchronized. Leader = the **sensor** you bend; follower = the **actuator** commanded.

### Servo bus & encoder
Each STS3215 has a **12-bit magnetic encoder** — always knows its own angle. Six servos share one 3-wire bus (red=VCC, black=GND, yellow/white=DATA) on one S600 serial port. The board shouts `read ID:3`; only servo 3 answers (others ignore) — addressed by unique ID, like a walkie-talkie call sign. Data travels as **UART electrical signals (0/1 levels)**, lower & more deterministic than WiFi — ideal for real-time control. `FEETECH SCServo Debug` software: *debug page* reads angle/temp/voltage live; *program page* writes ID/limit/center to servo EEPROM.

### Calibration — why it is mandatory
`lerobot-calibrate` measures each joint's **MIN/MAX** (prevents the arm hitting itself), builds **"same pose = same number"** (so leader↔follower teleop maps correctly), and sets center/zero (natural droop = 0 or 2047). Flow: move arm to center → Enter → bend each joint (except `wrist_roll`) to extremes → Enter. Follower calibrated separately. This is the **physical baseline** for everything after.

---

## 🔄 Full Pipeline

Three stages of **Imitation Learning** (a.k.a. Behavior Cloning). Analogy: master demos (collect) → you find the pattern (train) → you cook yourself (infer).

```
   collect ─────► train ─────► infer
(demonstrate)   (learn f)     (act autonomously)
```

### ① Collect
You bend the leader, follower follows (teleop); the program records **dual-camera frames + leader angles + follower angles**. One *episode* = a long list of `(observation, action)` pairs. Do a few dozen → a dataset.

> ⚑ *Data quality sets the ceiling:* shaky body / bad calibration → noisy demos → shaky policy. (Ties to "stable body = foundation of embodied AI".)

### ② Train (ACT)
Feed the dataset to the ACT network; learn `f(camera + joint state) → action` by reducing loss (prediction vs demo). Output: a policy checkpoint.

### ③ Infer
No more bending. Closed loop: live frame + state → model → action → follower executes → sense again. You only launch **two scripts**:

| Step script | Role | Stage |
|---|---|---|
| `1_calibrate_follower` | calibrate follower | prep |
| `2_replay_episode` | replay recorded data (audit) | collect-check |
| download / audit data | get clean dataset | ① |
| `train` | train ACT | ② |
| `check` | inspect loss curve | ② |
| `3_start_policy_server` | load model as "brain" service | ②→③ |
| `4_run_act_client` | read camera+arm, drive follower ("hands") | ③ |

**Policy server = brain** (holds model); **ACT client = hands** (reads camera/arm, asks brain, writes follower). Launch both → the arm loops on its own.

---

## 🧬 ACT Deep Dive

**ACT (Action Chunking Transformer)** — imitation-learning algorithm from Stanford's **Aloha** project. Core problem: let a manipulator learn *smooth, robust* manipulation from *few* demonstrations.

<div style="background:linear-gradient(135deg,#EEF2FF,#C7D2FE); padding:16px 20px; border-radius:14px; border:2px solid #6366F1;">

**Input → Output**
- **Image in:** top + wrist camera → vision backbone (ResNet / DinoViT) features
- **Proprioception in:** 6 joint angles (the arm's "self-feeling")
- **Output:** a **chunk** of future actions (e.g. next 30 steps of target angles)

</div>

### Three design highlights (interview gold)

1. **⚑ Action Chunking** — predict a *sequence* of future actions at once, not step-by-step. Avoids **compounding error** (one wrong step cascades); motion stays coherent, not jittery.
2. **⚑ CVAE head** — one view often has multiple valid solutions (grab left / grab right). VAE models this *multimodality* into a latent variable → more natural motion. Train: encode demo actions; infer: sample latent → decode action.
3. **⚑ Transformer backbone** — self/cross-attention fuses *dual-camera images + joint state* (heterogeneous inputs) into global context.

### Training mechanics
- Paradigm: **Behavior Cloning (BC)** — treat demos as supervised `(obs, action)` labels.
- **Loss** = MSE (predicted chunk vs demo chunk) + **KL** (keep VAE latent near standard normal).
- Backprop tunes weights until predictions match.
- **Data efficiency:** vs pure RL, imitation learns a desktop task from *dozens* of demos — perfect for a short bootcamp.

### vs naive imitation learning
Plain BC predicts *single-step* actions → easily suffers compounding error → task collapses mid-way. ACT's *chunking + CVAE + Transformer* upgrades "fragile single-step" into "robust multi-step, natural multimodal" — the key to Aloha's two-hand assembly.

---

## 🗺️ Algorithm Map (IL / RL / VLA / World Model)

| Concept | In bootcamp? | Interview priority | Your link |
|---|---|---|---|
| **IL / Behavior Cloning** | ✅ (ACT = BC) | ★★★★★ | main skill |
| **ACT** | ✅ (trained) | ★★★★★ | core |
| Teleop / data collection | ✅ | ★★★★★ | done hands-on |
| **RL** | partial (your side-line) | ★★★★ | side-line |
| **VLA** | ✅ (loaded pretrained) | ★★★★ | touched |
| **World Model** | ❌ (frontier) | ★★★ | know it |
| **Point Cloud / 3D** | ❌ (other track) | ★★★ | future |

- **IL:** learn from expert demos, not rewards. BC = supervised on `(obs,action)`. **DAgger** = learner tries, expert relabels, fixes distribution shift. Pain: *compounding error* / *distribution shift*. ACT's chunking attacks exactly this.
- **RL:** learn optimal policy by trial+reward. PPO / SAC / TD3 / DDPG. Hard in robotics: costly real trials, tricky reward, low sample efficiency. Combine: BC pretrain → RL finetune (RLPD, AWAC, DPO).
- **VLA (Vision-Language-Action):** foundation model, input `image + language` → `action sequence`, understands human commands. RT-1/RT-2, OpenVLA, Octo, π0. ACT can't take language; VLA can, but heavier. Your `vla_class_pub2` is this class — load & run directly.
- **World Model:** learns dynamics `given (state,action) predict next state` — an internal simulator. Dreamer, JEPA, UniSim, Genie. Use: model-based RL in latent space, data augmentation, "what happens if I do this" safety. More upstream than ACT.

---

## 🛠️ Troubleshooting (real field errors)

<details style="border:1px solid #e2e8f0; border-radius:10px; padding:8px 14px; margin:8px 0;">
<summary><b>🔥 S600 SSH refused after flashing</b></summary>

**Cause:** board is rebooting/flashing, port 22 not up.<br/>
**Fix:** wait for the flash bar to finish & board fully boot, then `Test-NetConnection` port 22.
</details>

<details style="border:1px solid #e2e8f0; border-radius:10px; padding:8px 14px; margin:8px 0;">
<summary><b>🔥 <code>conda: command not found</code></b></summary>

**Cause:** fresh-flashed system, conda not installed.<br/>
**Fix:** install **Miniconda (aarch64)**, then `source ~/.bashrc`.
</details>

<details style="border:1px solid #e2e8f0; border-radius:10px; padding:8px 14px; margin:8px 0;">
<summary><b>🔥 <code>externally-managed-environment</code> (pip blocked)</b></summary>

**Cause:** Debian forbids pip polluting system Python (PEP 668).<br/>
**Fix:** create conda/venv, `pip` inside the env.
</details>

<details style="border:1px solid #e2e8f0; border-radius:10px; padding:8px 14px; margin:8px 0;">
<summary><b>🔥 Wrong Miniconda arch (x86 on aarch64)</b></summary>

**Cause:** installed x86 wheel on ARM board → won't run.<br/>
**Fix:** re-download **aarch64** build; if half-installed, `rm -rf ~/miniconda3` then reinstall.
</details>

<details style="border:1px solid #e2e8f0; border-radius? no">

</details>

<details style="border:1px solid #e2e8f0; border-radius:10px; padding:8px 14px; margin:8px 0;">
<summary><b>🔥 <code>scp</code> folder fails "is not a regular file"</b></summary>

**Cause:** plain `scp` moves one file; folders need `-r`.<br/>
**Fix:** `scp -r` or `Compress-Archive` to zip first.
</details>

<details style="border:1px solid #e2e8f0; border-radius:10px; padding:8px 14px; margin:8px 0;">
<summary><b>🔥 <code>git clone</code> GitHub port 443 blocked</b></summary>

**Cause:** camp network limits external internet.<br/>
**Fix:** code pre-installed in `lerobot-main`; ask instructor for intranet mirror if needed.
</details>

<details style="border:1px solid #e2e8f0; border-radius:10px; padding:8px 14px; margin:8px 0;">
<summary><b>🔥 Only see docker0 IP (172.17.0.1)</b></summary>

**Cause:** that's Docker's virtual NIC, not the real IP.<br/>
**Fix:** `ip a` → look at `eth0` / `wlan0` real IP.
</details>

> 💡 *80% of robotics engineering is "getting the environment to run". Read the **last real error line** — don't panic at the ENOENT noise.*

---

## ⭐ STAR for your resume

Package the bootcamp as one tellable project. Interviewers want: *what you did, how, result, what it shows.*

| STAR | Say |
|---|---|
| **S**ituation | Zero-base mechanical grad; joined on-site embodied-AI bootcamp to run the robot-learning pipeline hands-on |
| **T**ask | On SO-101 dual-arm + S600, complete servo tuning → calibration → teleop collection → ACT training → deployment |
| **A**ction | FEETECH per-servo ID/limit/center; XBurn flash S600; SSH + conda + LeRobot; calibrate leader/follower; teleop-collect demos; train ACT; deploy server+client for autonomous grasp. *Solved SSH drops, wrong conda arch, Debian pip block.* |
| **R**esult | Arm autonomously grasps from dual-camera vision; systematic grasp of the collect→train→infer loop; clear plan to deepen force/tactile sensing |

**Interview Q&A you must own:**
- *How do leader/follower sync?* → both on S600; board reads leader & writes follower ~30–50 Hz; bus addressed by servo ID; not physically linked.
- *Why 12V follower / 5V leader?* → follower needs torque to grasp; leader needs compliance to be guided; reverse = burnout.
- *Why ACT > plain IL?* → chunking stops error cascade + CVAE handles multimodality + Transformer fuses views.
- *How does the camera "know" the arm?* → it only outputs pixels; the model learns the (frame,action) association from data.

---

## 🚀 What's next

Port this IL pipeline onto **DEA (Dielectric Elastomer Actuator)** soft actuators — self-sensing → policy → voltage. That is where soft-robotics **body** meets learning **brain**.

<sub>Built from a real Xbotics bootcamp report. Last updated 2026-08-15.</sub>
