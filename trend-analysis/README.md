# Soft Robotics × Embodied AI：写给做 DEA/软体方向的趋势分析

> 副标题：从《Emerging Frontiers and Technological Challenges in Soft Robotics》(ACS Nano 2026) 看软体机器人怎么变成"具身物理智能"的载体
>
> 文档定位：本文是给一位做介电弹性体（DEA）人工肌肉的浙大机械硕士写的"师兄笔记"。大白话、带比喻，不堆 AI 腔。所有【事实】都给了可核验来源（DOI / arXiv / 官网），带"※以官方渠道为准，需要复核"的都是时效性/商业数据，别直接当结论用。

---

## English Title

**Soft Robotics × Embodied AI: A Trend Analysis for DEA and Soft-Robotics Researchers**

## Abstract

Soft robotics and embodied artificial intelligence (embodied AI) are converging. Once valued mainly for safe, compliant contact, soft robots are now being reframed as physical substrates for intelligence: their nonlinear dynamics can serve as computation (morphological computation, physical reservoir computing) and as touch-rich perception. This analysis is anchored on the 2026 *ACS Nano* review *"Emerging Frontiers and Technological Challenges in Soft Robotics"* (Su, Magdassi, Chen et al., DOI: 10.1021/acsnano.6c13106), which argues that the field is moving from compliant mechanisms toward **Embodied Physical Intelligence**. We map the terrain for researchers working on Dielectric Elastomer Actuators (DEA, 介电弹性体驱动器) and artificial muscles. We summarize milestone papers (2020–2026), enabling technologies (DEA/HASEL artificial muscles, vision-based tactile sensing, soft Vision-Language-Action models, sim-to-real transfer), leading labs, and commercial players (soft grippers, flexible surgical robots, humanoid compliance). We argue that the rigid-to-soft "embodiment gap" is the key barrier for foundation models, that tactile sensing is the modality most likely to be absorbed by foundation models, and that high-performance DEA must be paired with learning-based control to leave the lab. The document closes with trend judgments, implications for a DEA-focused master's thesis, and channels for continuous tracking.

**Keywords:** soft robotics; embodied physical intelligence; dielectric elastomer actuator (DEA); artificial muscle; morphological computation; physical reservoir computing; tactile foundation model; vision-language-action (VLA)

---

## 一、一句话结论（先看这句）

**软体机器人不再只是"软的安全"，而正在变成"会自己算、自己摸、自己适应的智能身体"——你手里那块 DEA 人工肌肉，恰恰是这套具身物理智能（Embodied Physical Intelligence）最理想的发动机之一。**

---

## 二、为什么"软体 × 具身"现在交汇了

打个比方：以前机器人界像在造"钢筋铁骨的工人"，强调精度、刚度、可预测。大模型（LLM/VLM）火了以后，大家发现"脑子"够聪明了，但**身体**还是个短板——它既不会安全地贴着人干活，也不会在被推一下时顺势让一让。软体机器人（soft robotics，用硅胶、水凝胶、弹性体这类软材料做的机器人）天生柔顺、抗撞、能适应不规则物体，正好补这个窟窿。

而反过来，软体自己也有老大难：太软 → 建模难、控制难、不知道自己弯成啥样。过去这是缺点，现在被重新讲成了一个机会——**既然身体这么"活"，能不能让身体本身参与思考和感知？** 这就是"具身物理智能"的核心想法。

2026 年那篇 ACS Nano 综述（Su/Magdassi/Chen 等，37 位作者、28 家机构，DOI: 10.1021/acsnano.6c13106）把这个转向讲得很清楚：软体机器人正从"柔性机构 + 仿生运动"走向更广义的 Embodied Physical Intelligence，并列出了具身力学、自适应材料、分布式感知、physics-integrated AI、生物混合系统等前沿。

> **对 DEA/软体 × 具身方向的启示**：DEA 高比能量、毫秒响应、本身就是"肌肉"，是让软体身体"既能动又能算"的天然候选。你的课题如果只盯材料性能，建议同时想一句：这块肌肉，怎么让它"带脑子"？

---

## 三、学术脉络：里程碑论文时间线（带 DOI）

下面这几篇是 2020–2026 的骨架，按"理念 → 使能技术"排。所有编号 [R1]–[R12] 对应文末参考文献。

- **[R1] 2026 · 坐标轴论文**：Su J. et al., *Emerging Frontiers and Technological Challenges in Soft Robotics*, **ACS Nano 2026**, DOI: **10.1021/acsnano.6c13106**。提出 Embodied Physical Intelligence 范式，本文的"学术原点"。
- **[R2] 2024 · 综述**：Zhao Z. et al., *Exploring Embodied Intelligence in Soft Robotics: A Review*, **Biomimetics 2024, 9(4):248**, DOI: 10.3390/biomimetics9040248。系统梳理形态计算、具身演化、感知-控制-决策。
- **[R3] 2024 · 机械智能**：Kortman V.G., Mazzolai B., *Perspectives on Intelligence in Soft Robotics*, **Adv. Intell. Syst. 2024**, DOI: 10.1002/aisy.202400294。提出"机械智能（mechanical intelligence）"：身体靠自适应形状/功能/力学来应付环境。
- **[R4] 2023 · 感知综述**：Hegde C., Su J., Chen X.*, Magdassi S.*, *Sensing in Soft Robotics*, **ACS Nano 2023, 17, 15277–15307**, DOI: 10.1021/acsnano.3c04089。
- **[R5] 2025 · 感知-运动综述**：Su J., He K. et al., *Soft Materials and Devices Enabling Sensorimotor Functions in Soft Robots*, **Chemical Reviews 2025, 125, 5848–5977**, DOI: 10.1021/acs.chemrev.4c00906。
- **[R6] 2024 · 物理储备池(PRC)**：Wang J. et al., *…Physical Reservoir Computing…*, **Adv. Intell. Syst. 2024**；arXiv: **2411.07309**。只靠内部分布式压力，就能估姿态和负载。
- **[R7] 2024 · PRC 游动器**：He S., Musgrave P., *Physical reservoir computing on a soft bio-inspired swimmer*, **Neural Networks 2024**, DOI: 10.1016/j.neunet.2024.106766。
- **[R8] 2024 · 机械智能+PRC**：Zhang Y. et al., *Embodying Multifunctional Mechano-Intelligence…*, **Adv. Sci. 2024**, DOI: 10.1002/advs.202305074。把感知-决策-指令直接塞进力学域。
- **[R9] 2025 · 软体 VLA**：Su H. et al., *Bridging Embodiment Gaps: Deploying Vision-Language-Action Models on Soft Robots*, **NeurIPS 2025 Workshop**；arXiv: **2510.17369**。第一次把 VLA 部署到软体连续体机械臂，开源了第一个软体演示数据集。
- **[R10] 2025 · 触觉 VLA**：Huang J. et al., *Tactile-VLA…*, **arXiv:2507.09160**。把触觉反馈灌进 VLA，插拔任务成功率 90% vs 基线 40%/25%。
- **[R11] 2025 · 软手学习**：Yoo U. et al., *KineSoft…*, **arXiv:2503.01078**。本体应变感知 + 形状扩散模仿，控制欠驱动软手。
- **[R12] 关于 GPT-4o 类大模型做软体操作**：现在主流不是直接拿 GPT-4o 开车，而是用 **OpenVLA、π₀、RT-2、Helix** 这类 VLA/VLM 当骨干，再小样本微调桥接"刚-软本体鸿沟"（来源：arXiv:2510.17369）。

> **对 DEA/软体 × 具身方向的启示**：时间线说明一个趋势——论文重心从"材料/结构能软"转到"身体能算、能摸、能听指令"。做 DEA 的你，引用文献时别只堆材料学论文，[R6]–[R12] 这几篇"身体即计算/感知"的工作才是和具身 AI 真正对得上的。

---

## 四、关键使能技术

### 4.1 DEA / HASEL / 人工肌肉

- **[R13] 清华高比能 DE（2024 标杆）**：Feng W. et al., *A large-strain and ultrahigh energy density dielectric elastomer for fast moving soft robot*, **Nature Communications 2024, 15:4222**, DOI: **10.1038/s41467-024-48243-y**。46 MV/m 低电场下 253% 面积应变，比能量 **225 J/kg**（约天然肌肉 6 倍），软体机器人速度 **20.6 BL/s**（迄今最快 DEA 软体机器人）。
- **HASEL（水力学放大自修复静电人工肌肉）**：[R14] Rumley E. et al., *Biodegradable electrohydraulic actuators…*, **Science Advances 2023**, DOI: 10.1126/sciadv.adf5551（可生物降解，10 万次循环不失效）；ETH 的 **F-HASEL** 加了专用电容传感电极，能在 20 Hz 高频驱动下自感知位移（IROS 2024，来源：srl.ethz.ch/platforms/ems/pele1.html）；2024 年低电压 HASEL 把驱动电压压到 **1100 V**、功率密度 50.5 W/kg（综述来源 PMC12942800）。

> **对 DEA/软体 × 具身方向的启示**：DEA 比能量已经打过天然肌肉，但高电压 + 迟滞是硬伤。材料再卷，不解决"怎么被聪明地控制"，就还是实验室里的肌肉标本。

### 4.2 软体感知与触觉

- **GelSight（视触觉）**：MIT CSAIL 的 Edward Adelson 团队 2009 年提出（三色光 + 凝胶 + 相机）；后续 GelSlim（2018）、GelSlim 3.0（2022）；GelSight Inc. 2022 年出 GelSight Mini（$499）。
- **Meta DIGIT（2020 开源）** 指尖触觉传感器，后和 GelSight 合作商业化。
- **触觉基础模型 Sparsh**：[R15] Higuera C. et al., *Sparsh: Self-supervised touch representations…*, **CoRL 2024**（Meta FAIR + UW + CMU）。在 **46 万+** 张触觉图上自监督预训练，有限标注下平均比任务专用模型强 **95.1%**（来源：ai.meta.com/research/publications/sparsh-…）。
- **Digit 360 / Digit Plexus（Meta，2024-10-31）**：指尖 800 万+ taxels、18+ 感知特征、片上 AI，与 GelSight、Wonik 合作量产（来源：venturebeat.com/…）。
- **国内视触觉**：纬钛机器人（Adelson 团队李瑞博士创立，2024-01 成立，2025 获小米系融资）、戴盟机器人（2025 推 DM-Tac W，每平方厘米 4 万感知单元）、叠动科技、一目科技。※ 融资与产能**以官方渠道为准，需要复核**。

> **对 DEA/软体 × 具身方向的启示**：触觉是软体最该有的"超能力"，但视触觉传感器大多是刚性小模块。做 DEA 手/驱动器时，把传感电极做进驱动器本体（像 F-HASEL 那样）比外挂摄像头更"具身"。

### 4.3 形态计算 / 物理储备池计算（PRC）

[R6][R7][R8] 是一类很"反直觉"的工作：不写复杂控制器，而是**让软体本身的动力学当计算机**——输入信号过一遍身体的非线性，输出端做个简单线性回归就能估状态。相当于把"算"这件事外包给了材料。

> **对 DEA/软体 × 具身方向的启示**：PRC 对你是个现成抓手——DEA 驱动器的电压-形变-电容耦合本身就是强非线性，完全可以当储备池用，做本体感知（proprioception）几乎零额外传感器。

### 4.4 软体 VLA / Sim-to-Real

[R9] 证明：预训练在刚性臂上的 VLA 直接搬去软体臂会"完全不会动"，但用几十个演示小样本微调就能拉平差距。[R11] 用软手本体感知 + 扩散策略做模仿。[R10] 把触觉塞进 VLA 做力控泛化。Sim-to-real 方面，[R16] Lahariya et al., *Learning physics-informed simulation models… with DEA*, **IROS 2022**, DOI: 10.1109/IROS47612.2022.9981373，给 DEA 学可微分仿真再做 MPC，误差 ≤5%；[R17] 2025 年有人用 **DDPG** 控制 DE 最小能量结构（DEMES）人脸微表情，无模型补偿迟滞（*Precision actuation…*, Sensors and Actuators A, 2025）。

> **对 DEA/软体 × 具身方向的启示**：别再只做"建模 + PID"。RL / 可微分仿真 / MPC 已经有人跑通 DEA，你做控制实验时直接站在这几条肩膀上。

---

## 五、全球实验室与团队地图

- **陈晓东（Xiaodong Chen，NTU）**：ACS Nano 主编，iFLEX 中心主任，Max Planck–NTU 联合人工感官实验室；做 mechanomaterials（机械材料）、电子皮肤、人工感觉神经元（来源：everybodywiki.com/Chen_Xiaodong）。
- **Robert Shepherd（Cornell）**：DEA / 软材料与软体制造。
- **Barbara Mazzolai（IIT，意大利）** & **Cecilia Laschi**：植物启发软体、具身智能分类（见 [R3]）。
- **Robert Katzschmann（ETH Zurich）Soft Robotics Lab**：SoFi 软体鱼（Science Robotics 2018）、Nature 2023 多材料 3D 打印机械手、Nat. Commun. 2024 电液肌肉腿、Sci. Adv. 2024 低电压电液驱动器。
- **Josie Hughes（EPFL）Soft Robotic Systems Lab**：软体连续体 + VLA（[R9]）。
- **Zhigang Suo（Harvard）**：DEA 理论奠基（*Theory of dielectric elastomers*, Acta Mech. Solida Sin. 2010）；**清华团队**（王超等）做了 [R13] 那篇高比能 DE。
- **MIT CSAIL（Adelson）**：GelSight 体系；**Stanford（Allison Okamura 等）**：触觉 / 柔顺交互。
- **国内可核验锚点**：**南方科技大学 葛锜（Qi Ge）** 是 ACS Nano 2026 综述共同作者（软体 3D 打印与驱动）；**清华大学**（王超 / 化学系 DE 材料）；**浙江大学**（柔性电子 / 软体，徐凯臣等与 NTU Chen 组有合作，来源 me110anniv.zju.edu.cn）。西安交大、哈工大、北航等也有软体 / 柔性驱动团队，※ **具体名单以各单位官网为准，需要复核**。

> **对 DEA/软体 × 具身方向的启示**：想找合作 / 申博 / 求职，上面这些组就是地图。做 DEA 的优先看 Suo、清华、Katzschmann（电液）、Shepherd；做"身体即感知"优先看 Chen（NTU）、Hughes。

---

## 六、产业化现状与玩家

**软体夹爪（最成熟的一层）**
- Soft Robotics Inc.（波士顿）mGrip 食品级气动软夹爪，推 mGripAI/SuperPick。※ **2024 年 8 月 Schmalz 收购了 mGrip 手指夹爪家族（含专利）**（来源：pmarketresearch.com）。
- OnRobot（丹麦）软夹爪 + 视觉 / 力控，2017 收 Robotiq、2019 战略投资 Soft Robotics。
- Festo（德）BionicSoftGripper、FinGripper；※ **2025 年 12 月推 HPSX 卫生型软夹爪**（来源：pmarketresearch.com、dataintelo.com）。
- ※ 行业报告称 2024 年 Soft Robotics Inc. 营收约 $48.6M、OnRobot 约 $62M，**市场数据以官方 / 财报为准，需要复核**。

**软体 / 柔性手术与内窥镜**
- Medrobotics（美，2005 成立，累计融资约 $179.74M，来源 CB Insights）做蛇形柔性手术机器人，用于头颈 / 结直肠等难达解剖。
- 柔性内镜手术机器人市场 2024 年约 $3.26 亿（美），预计 2034 年 $13 亿，CAGR 14.7%，玩家含 Intuitive Surgical、Medtronic、J&J/Auris(Monarch)、Olympus、Medrobotics（来源：gminsights.com）。※ **融资 / 估值 / 产能以官方渠道为准，需要复核**。

**人形机器人里的柔顺 / 软体部件**
- **Figure 03**（2025-10）每只手有掌心摄像头 + 自研指尖触觉（可感 3 克力），接 **Helix** VLA（来源：runtimewire.com）。
- **1X NEO**：肌腱驱动、软体、22 自由度手，2025-10 开启预订、目标 $20k；※ 2026-07 发布 25 DoF 新手的发布与产能**以 1X 官方为准，需要复核**（来源：fourweekmba.com）。
- **宇树（Unitree）**：公开产业链资料显示其灵巧手 / 柔性触觉传感器由 **苏州能斯达（汉威科技子公司）** 供应，赋予 0.1 N 级力感知（来源：finance.sina.cn/2025-07-19）。※ **供应商与量产以官方渠道为准，需要复核**。
- 普遍趋势：Figure、1X、宇树、特斯拉 Optimus 都在手端加"柔顺 / 力控 / 触觉"，但大多是"刚性骨架 + 弹性覆盖 / 力控"，还不是全软体。

> **对 DEA/软体 × 具身方向的启示**：产业化是"夹爪先行、手术稳健、人形渗透"三层。DEA 想进产业链，短期最现实的是做灵巧手的柔顺指节 / 触觉皮肤，而不是和电机硬刚大力矩。

---

## 七、5–10 年趋势判断（以下均为"判断"，非事实）

1. **软体会从"安全件"升级成"智能体"**：非线性动力学既是控制负担，也是计算和感知资源，这条线和 ACS Nano 2026 的 Embodied Physical Intelligence 一脉相承。
2. **"刚-软本体鸿沟"是 VLA 落地的头号坑**：刚性臂预训练策略在软体上几乎全废，但小样本微调能桥接（[R9]）。未来拼的是"软体专属数据集 + cross-embodiment 微调"。
3. **触觉是最先被基础模型"吃掉"的模态**：Sparsh、Digit 360、Tactile-VLA 已成型，国内纬钛 / 戴盟也冒头，值得重点盯。
4. **DEA/HASEL 必须绑定学习控制才能出实验室**：高电压 + 迟滞决定了 RL / 可微分仿真 / MPC 不是可选项。
5. **软体不会取代刚性，而是当"柔顺关节 / 软体手 / 触觉皮肤"嵌进去**：人形和工业链都会这么用。

---

## 八、对本人课题与求职的启示

- **课题层面**：你是做 DEA 人工肌肉的，最值钱的切入点是"让驱动器自带感知 + 自带一点脑子"。具体可落地的三件事：(a) 用 PRC 思路把 DEA 的电容 / 形变耦合当储备池做本体感知（接 [R6][R7]）；(b) 用 [R16][R17] 的可微分仿真 / DDPG 框架做 DEA 控制，别再手写模型；(c) 把传感电极嵌进 DEA 本体，呼应 F-HASEL 的"驱动-感知一体化"。
- **文献层面**：引用时把 [R1]（ACS Nano 2026）当坐标原点，再拉 [R2]–[R5] 综述 + [R6]–[R12] 使能技术，故事就立得住。
- **求职 / 申博层面**：上面第五节那张地图就是你的目标池。做材料偏底层看 Suo、清华；做"身体即智能"看 Chen(NTU)、Hughes(EPFL)、Katzschmann(ETH)；产业界看 Soft Robotics Inc.、Festo、以及国内视触觉创业（纬钛 / 戴盟）——这些公司正缺"既懂 DEA 又懂学习控制"的人。
- **一句话送你**：别把自己定位成"做块软肌肉的材料人"，定位成"给具身智能造会算会摸的身体的人"，身价立刻不一样。

---

## 九、检索与持续跟踪渠道

**中文检索词**：软体机器人；具身物理智能；介电弹性体驱动器（DEA）；人工肌肉；HASEL；视触觉 / 光学触觉；电子皮肤；形态计算；物理储备池计算；柔顺关节 / 软体灵巧手。
**英文检索词**：soft robotics; embodied physical intelligence; morphological computation; physical reservoir computing; mechanomaterials; dielectric elastomer actuator (DEA); HASEL artificial muscle; vision-language-action (VLA); tactile foundation model; GelSight; soft robotic hand; reinforcement learning soft robot。
**期刊（RSS）**：*Science Robotics*、*Soft Robotics (SORO)*、*Advanced Intelligent Systems*、*ACS Nano*、*Nature Communications*、*Advanced Science*、*Chemical Reviews*、*Nature Machine Intelligence*、*IEEE RA-L*。
**会议**：RoboSoft、ICRA、IROS、CoRL、NeurIPS（Embodied AI / SpaVLE workshops）、RSS。
**预印本**：arXiv **cs.RO** / **cs.AI** / **cs.LG**（以及 cs.ET 软体电子）；Hugging Face（如 HCSuMoss 软体机器人数据集）。
**人 / 社区**：X 上跟 Xiaodong Chen、R. Katzschmann、R. Shepherd、Barbara Mazzolai、Josie Hughes；中文跟"机器人大讲堂""leaderobot（青榴）""智东西""量子位"对综述与产业动态的转述（社媒信息需回原始论文 / 官网交叉核验）。

---

## 十、参考文献

- [R1] Su J., Magdassi S., Chen X. et al. *Emerging Frontiers and Technological Challenges in Soft Robotics*. **ACS Nano 2026**. DOI: 10.1021/acsnano.6c13106
- [R2] Zhao Z., Wu Q., Wang J. et al. *Exploring Embodied Intelligence in Soft Robotics: A Review*. **Biomimetics 2024, 9(4):248**. DOI: 10.3390/biomimetics9040248
- [R3] Kortman V.G., Mazzolai B. *Perspectives on Intelligence in Soft Robotics*. **Adv. Intell. Syst. 2024**. DOI: 10.1002/aisy.202400294
- [R4] Hegde C., Su J., Chen X.*, Magdassi S.* *Sensing in Soft Robotics*. **ACS Nano 2023, 17, 15277–15307**. DOI: 10.1021/acsnano.3c04089
- [R5] Su J., He K. et al. *Soft Materials and Devices Enabling Sensorimotor Functions in Soft Robots*. **Chemical Reviews 2025, 125, 5848–5977**. DOI: 10.1021/acs.chemrev.4c00906
- [R6] Wang J. et al. *…Physical Reservoir Computing…*. **Adv. Intell. Syst. 2024**; arXiv: 2411.07309
- [R7] He S., Musgrave P. *Physical reservoir computing on a soft bio-inspired swimmer*. **Neural Networks 2024**. DOI: 10.1016/j.neunet.2024.106766
- [R8] Zhang Y. et al. *Embodying Multifunctional Mechano-Intelligence…*. **Adv. Sci. 2024**. DOI: 10.1002/advs.202305074
- [R9] Su H. et al. *Bridging Embodiment Gaps: Deploying VLA Models on Soft Robots*. **NeurIPS 2025 Workshop**; arXiv: 2510.17369
- [R10] Huang J. et al. *Tactile-VLA…*. **arXiv:2507.09160 (2025)**
- [R11] Yoo U. et al. *KineSoft…*. **arXiv:2503.01078 (2025)**
- [R12] OpenVLA / π₀ / RT-2 / Helix 等 VLA 框架；刚-软本体鸿沟来源：arXiv:2510.17369
- [R13] Feng W. et al. *A large-strain and ultrahigh energy density dielectric elastomer…*. **Nat. Commun. 2024, 15:4222**. DOI: 10.1038/s41467-024-48243-y
- [R14] Rumley E. et al. *Biodegradable electrohydraulic actuators…*. **Sci. Adv. 2023**. DOI: 10.1126/sciadv.adf5551
- [R15] Higuera C. et al. *Sparsh: Self-supervised touch representations…*. **CoRL 2024**. ai.meta.com/research/publications/sparsh-self-supervised-touch-representations-for-vision-based-tactile-sensing
- [R16] Lahariya M. et al. *Learning physics-informed simulation models… with DEA*. **IROS 2022**. DOI: 10.1109/IROS47612.2022.9981373
- [R17] *Precision actuation… integrating deep reinforcement learning* (DEMES + DDPG). **Sensors and Actuators A, 2025**. sciencedirect.com/science/article/abs/pii/S0924424725005680
- 软手学习：Zhou K. et al. *Cable-Actuated Soft Manipulator… DRL*. **Adv. Intell. Syst. 2024**. DOI: 10.1002/aisy.202400112 ｜ Li L. et al. *Continual Policy Distillation… In-Hand Manipulation*. **RoboSoft 2024**. DOI: 10.1109/RoboSoft60065.2024.10522027 ｜ Suske G. et al. *Open-loop DRL Control of Soft Robotic In-hand Manipulations*. **IROS 2025**. DOI: 10.1109/IROS60139.2025.11245997
- DEA + RL 早期证据：Yang T. et al. *A soft artificial muscle driven robot with reinforcement learning*. **Sci. Rep. 2018, 8:14518**. DOI: 10.1038/s41598-018-32757-9

---

*本文件为仓库内分析文档，未做 git push。所有【事实】均附来源；带"※…以官方渠道为准，需要复核"者为时效性 / 商业数据，引用前请二次核实。*