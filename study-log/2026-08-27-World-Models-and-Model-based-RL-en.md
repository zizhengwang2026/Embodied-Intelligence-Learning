# Lecture 14 — World Models & Model-based Reinforcement Learning

> **Meta**
> - Date: 2026-08-27 (Wednesday)
> - Lecture / Day: Lecture 14 — Day 14 of the study plan
> - Plan anchor: `study-plan-60d.md` → **P5 学习范式进阶 (Advanced Learning Paradigms)** — World Models / Deployment
> - Goal of today: understand the **world model** — letting the agent "imagine" what happens next inside its head, so it can learn complex tasks from very little real-robot data. This is the bridge that **welds Day 12's generative policies** and **Day 13's reinforcement learning** together.

---

## 0. One-line summary

> **World Model = a "mini-simulator" the agent learns from data by itself**: feed it "current state + the action I want", and it predicts "what the next state will be, and how much reward I'll get". With it, the agent doesn't have to take real risky trial-and-error — it repeatedly **rehearses in its head** to find the best action. This is the key to the "sample efficiency" that mainstream embodied AI chases.

---

## 1. Core knowledge (what today is about)

| Concept | One line |
|---|---|
| **World model** | a learned state-transition predictor `s' = f(s, a)` — a samplable / differentiable "soft simulator" |
| **Model-based RL (MBRL)** | learn a world model first, then plan/explore inside it — more sample-efficient than model-free |
| **Model-free RL (MFRL)** | learn policy/value directly, no explicit world model (Day 13's PPO / SAC belong here) |
| **Latent imagination** | "dreaming"-style rollout in a compressed latent space, without decoding to real pixels |

### 1.1 Why we need a world model

Real-robot trial-and-error is **expensive, slow, and dangerous** (Day 13: one drop can break the robot). A world model moves "falling into the pit in the real world" to "falling into the pit in your head" — **imagination replaces experience**.

> Analogy: a strong chess player replays a dozen moves in their head before committing; a world model is the robot's "in-head rehearsal engine". It doesn't need to actually knock over a cup ten thousand times — it knocks it over ten thousand times in simulation.

### 1.2 DreamerV3 (flagship, RSS 2023, Haarnoja et al.)

- Core idea: **rollout in latent space**. An encoder compresses the image into a latent state → the world model predicts the next step in latent space → actor-critic makes "dreaming"-style decisions **entirely in latent space, never decoding to real pixels**.
- Track record: from pixels alone, it collected a diamond in Minecraft from scratch, proving extremely high sample efficiency (far cheaper than MFRL).
- Key components: **RSSM** (Recurrent State-Space Model, compresses history into state), **discretized representation**, **critic value estimate** to guide imagination depth.

### 1.3 MBRL vs MFRL — how to choose

| Dimension | Model-based (MBRL) | Model-free (MFRL) |
|---|---|---|
| Sample efficiency | High (imagine in model) | Low (step through reality) |
| Arch-enemy | **model-bias**: model wrong → plan wrong | sample explosion |
| Fits | little real data, imperfect sim | simple env, massive trials |

Modern compromise: **short-horizon imagination in the world model + long-horizon correction with real interaction** — saves samples while resisting drift.

<mark>**📌 Slide supplement | Generative policy ↔ world model are siblings**: Day 12's Diffusion Policy "generates multimodal actions in **action space**"; the world model "generates multi-step futures in **state space**". One handles "how to act", the other "what happens if I act" — together they form the full "imagine + execute" loop. A VLA (Day 12) predicts the action, the world model predicts the consequence; they're often chained into "think about the consequence first, then pick the action".</mark>

### 1.4 World models for soft / DEA robotics (小畅's cross-link)

- A rigid arm's world model ≈ approximate rigid-body dynamics; **soft / DEA bodies are continuously deforming + hysteretic**, extremely hard to write analytically.
- Fix: **differentiable simulation** as a "white-box world model" — `DiffTaichi` / `ChainQueen` / `SoMo` / `PyElastica` compute gradients that backprop straight into material parameters and controllers.
- **Why this matters to 小畅**: the DEA artificial-muscle mapping "voltage → deformation" is, at its core, a **world model that must be learned / modeled**. Building DEA constitutive models and doing model-predictive control (MPC) during your PhD is the *same idea* as MBRL here — except you use a "physical white-box model" while AI usually uses a "data black-box model".

---

## 2. Principles to internalize (why it works)

1. **A world model = a *learnable approximation* of the environment, not a real physics engine.** Good enough is enough; it needn't be perfect.
2. **model-bias is the arch-enemy**: the worse the model, the more the plan drifts; so it must be periodically patched with real-robot data.
3. **Latent imagination ≫ pixel imagination**: cheaper, more stable, less distracted by irrelevant detail.
4. **It patches Day 13's短板**: MFRL (PPO/SAC) eats samples; the world model makes "few-shot" possible — the exact bottleneck of embodied-AI deployment.

---

## 3. One diagram: the world-model-driven RL loop

```mermaid
flowchart LR
    S[Current state s] --> WM[World model<br>s', r = f(s, a)]
    A[Action a] --> WM
    WM --> S2[Predicted next state s']
    WM --> R[Predicted reward r]
    S2 --> PI{Plan / Policy}
    PI -->|pick best a*| A
    R --> PI
```

> This is an **upgraded version** of Day 13's "RL five elements": before, the agent tried inside the real env (env gives s' and r); now the "world model gives s' and r", and the real env only verifies at the last step.

---

## 4. Today's operation steps (study workflow, not coding)

1. **Read this file once** (you are here).
2. **Hand-draw the §3 diagram**: state s + action a → world model → predict s' / r → plan picks action.
3. **Explain out loud**: what a world model is, why it's more sample-efficient than MFRL, what model-bias is.
4. **Watch the world-model chapters** (1.0–1.5× speed); focus on DreamerV3's "latent imagination".
5. **Mirror test (3 min):** *"A world model is ___; why is it sample-efficient ___; MBRL vs MFRL ___; what is model-bias and how to fix it ___; why is a DEA world model hard ___."*
6. **(Later)** run an MBRL baseline (e.g. DreamerV3) in Isaac Lab and compare sample efficiency against PPO.

> ✅ **Definition of "done today":** can explain the world model + draw the loop + pass the mirror test.

---

## 5. Common misconceptions & easy mistakes

| # | Misconception | Reality |
|---|---|---|
| 1 | "A world model is just a game simulator." | Not a ready engine — it's an **approximation learned from data**; it can "hallucinate" nonexistent states. |
| 2 | "With a world model you don't need the real robot." | Wrong. The model drifts; it must be **periodically corrected with real data**, or it goes more wrong the more it imagines. |
| 3 | "MBRL is always better than MFRL." | MBRL wins when data is scarce; MFRL is more stable when the model is inaccurate. Depends on the scene. |
| 4 | "World model and generative policy (Diffusion Policy) are the same." | Siblings, not twins: one generates "future states", the other "current actions". |
| 5 | "Soft robots can't use world models." | The opposite — differentiable sim (DiffTaichi etc.) is the natural world model for soft bodies, and gradients backprop. |

---

## 6. Next steps / checkpoint

- **Checkpoint passed if:** you can explain the world model + draw the loop + pass the 3-min mirror test.
- **Next lecture (Day 15):** **Real-robot deployment & embodied benchmarks** — move the trained policy to the real machine, quantize/compress it, and score it objectively with benchmarks (RLBench / ManiSkill / AgiBot World …).
- **This week's seed:** remember the trio "imagine (world model) + execute (generative policy) + trial-error (RL)" — the standard recipe of modern embodied-AI algorithms.

---

## 7. First-person reflection (from the SO-101 bootcamp, not the textbook)

The bootcamp didn't train a world model directly, but the rhythm of **"try in sim first, then go real"** is everywhere this idea lives:

1. **Sim acts as a cheap world model.** Run ACT in LeRobot / Isaac Lab first, then deploy to the real SO-101 — essentially using "a (good-enough if imperfect) world model" to save real-robot trial-and-error.
2. **The Sim2Real gap *is* model-bias made concrete.** Day 13: friction and latency differ between sim and real, so the policy "fails its imagination" on the real robot. Same root cause as world-model drift.

> If I were to redo it: **get the loop running in a small sim first, then go real and hunt the gap** — exactly isomorphic to "imagine first, verify real".

---

### References (for later, not required today)
- Ha & Schmidhuber (2018). *World Models*. arXiv:1803.10122.
- Hafner et al. (2023). *DreamerV3*. arXiv:2301.04104.
- Hafner et al. (2019). *RSSM / Dream to Control*. ICLR 2020.
- Differentiable sim: DiffTaichi (SIGGRAPH 2021), ChainQueen (RSS 2019), PyElastica, SoMo.
- (Later) Day 15 covers real deployment & benchmarks; Day 16 wraps up to soft / DEA and special-ops applications.