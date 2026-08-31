# Q-learning Tabular Method Principle and Code

> **阶段**：P11 ｜ **今日课程**：215–218
> **日期**：2026-10-11 ｜ **Day 59 / 60**
> 本篇为《黑马程序员·具身智能》223 节配套复习笔记，零基础可读、不失专业；含流程图与易错点。

## 一、今日课程（集号映射）

- **215 Init RL q-table**: build a "state × action" table.
- **216 Q-table update principle**: how Q-values update.
- **217 Q-table reward backprop update**: reward propagates backward along the path.
- **218 Final Q-learning code**: write runnable Q-learning.

## 二、核心知识点（零基础讲透）

### 2.1 What the Q-table is
When states/actions are **discrete and few**, use a table storing "how good is action a in state s":
- rows = state s, cols = action a, cell = Q(s,a) = expected cumulative reward.
- After learning, pick the max-Q action per state (greedy policy).

### 2.2 Update formula (core)
Each step, use the just-received reward to correct the Q estimate:

```
Q(s,a) <- Q(s,a) + α [ r + γ·max_a' Q(s',a') - Q(s,a) ]
```
- α (learning rate): step size; γ (discount): how much to value future reward.
- `r + γ·max Q(s',a')` is the "TD target"; left of minus is old estimate, right is new target, difference is "error".

### 2.3 Reward backpropagates along the path
Because each step uses "next step's max Q", **the terminal reward propagates backward step by step**, so far states gradually learn "this path eventually pays".

## 2.5 补充细节：Q-learning tabular method

- Tabular method: store Q(s,a) as a lookup table; fits discrete, not-too-large state/action spaces.
- Update rule (Bellman): `Q(s,a) ← Q(s,a) + α[ r + γ·max_a' Q(s',a') − Q(s,a) ]`.
- Meaning: use "the max Q reachable in the next state" as the target, pull the current estimate toward it; α is the learning rate, γ is the discount.
- off-policy: the target uses the greedy action corresponding to "next-state max Q"; it does not require the current step to actually follow it.
- Exploration: ε-greedy — with probability ε pick a random action to explore; with 1−ε pick the greedy max-Q action.

## 3. 一张图

![Q-learning tabular method](assets/qlearning_table.svg)

## 三、动手操作（跑通才算学会）

1. Init FrozenLake's Q-table (num_states × num_actions, all zero).
2. Write the Q-learning training loop (ε-greedy exploration + the update formula above).
3. Print the Q-table before/after training; see if Q near the goal rises and the path improves.

## 四、易错点（前人踩过的坑）

- **γ (discount) = 0 → only greedy for now**: terminal reward can't reach far states; they never learn. Usually 0.9~0.99.
- **ε-greedy too low → never tries new actions, stuck in local optimum**: explore with large ε early, shrink later for exploitation.
- **Huge state count but still using a table**: when states are continuous/too many, the Q-table can't fit → exactly the motivation for Day60 DQN (neural net replaces table).

## 五、DEA / 软体机器人交叉链接（轻量）

After discretizing DEA soft-posture, you can first try tabular Q-learning; but deformation is continuous, so ultimately DQN/policy-gradient is needed. Light cross-link; main line is tabular Q-learning.

## 六、今日小结 & 镜子复述 3 分钟

Today we write the first runnable RL algorithm — tabular Q-learning: a Q(s,a) table stores "state-action value", updated by the TD formula, reward backpropagates along the path. Two knobs: γ for future, ε for exploration; too many states → tomorrow's DQN.

> 说明：本系列为通用具身智能学习笔记（不是军事专题）。DEA（介电弹性体驱动器）仅作与本人研究方向的轻量交叉，不展开、不占主线。
