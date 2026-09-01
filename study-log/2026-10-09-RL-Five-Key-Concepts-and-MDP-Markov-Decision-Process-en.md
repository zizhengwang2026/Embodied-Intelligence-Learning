# RL Five Key Concepts and MDP Markov Decision Process

> **阶段**：P11 ｜ **今日课程**：208–210
> **日期**：2026-10-09 ｜ **Day 57 / 60**
> 本篇为《黑马程序员·具身智能》223 节配套复习笔记，零基础可读、不失专业；含流程图与易错点。

## 一、今日课程（集号映射）

- **208 RL's 5 key concepts**: Agent / Environment / State / Action / Reward.
- **209 RL concept analysis**: map the five concepts onto an embodied robot.
- **210 MDP state-transition model**: Markov Decision Process, how state transfers one step.

## 二、核心知识点（零基础讲透）

### 2.1 RL's five key concepts (memorize first)
| Concept | Meaning | Embodied-robot example |
|---------|---------|------------------------|
| Agent | the decision-maker | controller / policy network |
| Environment | the world outside Agent | real workspace, table, objects |
| State (s) | current situation | joint angles + camera image |
| Action (a) | Agent's move | torque/angle sent to servo |
| Reward (r) | score from environment | grab object +1, drop -1 |

### 2.2 The RL loop
Agent sees State → outputs Action → environment becomes new State and gives Reward → Agent learns "which Action maximizes cumulative Reward".

### 2.3 MDP (Markov Decision Process)
MDP means: **the next state depends only on "current state + current action", not the past** (Markov property / "memoryless").
- Math: s' ~ P(s'|s,a), transition probability depends only on (s,a).
- Meaning: describe "current state" fully enough and you can ignore history; the problem is solvable.

## 2.5 补充细节：RL's five key concepts & MDP

- Building on the five key concepts in §2.1 (Agent / Environment / State / Action / Reward), RL also commonly uses two **derived quantities** to describe decisions: policy π(a|s) (which action to pick in which state) and value V(s) or Q(s,a) (how valuable a state/action is) — these are built on state/action/reward, not a redefinition of the five key concepts.
- MDP formalism: the 5-tuple (S, A, P, R, γ); P is the state-transition probability, R is the reward, γ∈[0,1] is the discount factor.
- Objective: maximize the expected "cumulative discounted reward" E[Σ γᵗ rᵗ] — the further in the future, the lower the weight.
- Two mainstream families: value-function methods (learn Q/V then derive a policy) and policy-gradient methods (optimize π directly); BC is imitation, RL is trial-and-error optimization.

## 3. 一张图

![MDP Markov Decision Process loop](assets/mdp_loop.svg)

## 三、动手操作（跑通才算学会）

1. Define the five concepts for an "embodied robot" in one or two sentences each (e.g. Agent=controller, State=joint angles+camera, Action=torque to servo, Reward=grab success +1).
2. Draw the RL loop (Agent↔Environment).
3. Explain aloud: why does the MDP assumption "next step only sees current" simplify the problem?

## 四、易错点（前人踩过的坑）

- **Mixing RL "reward" with supervised "label"**: RL has no ready answer, only environment rewards (possibly delayed, sparse).
- **Designing reward for "every step"**: over-dense reward induces shortcut behavior; design reward reflecting the true goal.
- **Incomplete State → violates Markov property**: missing key info (e.g. object velocity) makes the policy unlearnable.

## 五、DEA / 软体机器人交叉链接（轻量）

For DEA soft arms in RL: State includes "deformation/voltage", Action is driving voltage, Reward e.g. "soft hand closes and holds object +1". Light cross-link; main line is generic RL concepts.

## 六、今日小结 & 镜子复述 3 分钟

Today we enter P11 (Reinforcement Learning). First memorize the five concepts Agent/Environment/State/Action/Reward, then understand the RL loop and MDP's "memoryless" property. Core reminder: **RL has no labels, only rewards — the most essential difference from BC**.

> 说明：本系列为通用具身智能学习笔记（不是军事专题）。DEA（介电弹性体驱动器）仅作与本人研究方向的轻量交叉，不展开、不占主线。
