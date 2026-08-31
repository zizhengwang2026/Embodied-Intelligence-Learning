# 具身智能 60 天学习笔记 · 导航索引

> 配套视频：B 站《黑马程序员 · 具身智能》全套 **223 节**。

> 本仓库 `study-log/` 含 **Day 1–60 共 120 篇**复习笔记，每讲中英双语各一篇（zh / en）。

> 严格按 `study-plan-60d.md` 的集号映射编写；全文零军事内容；含 Mermaid 图、易错点与 DEA 轻量交叉链接。

> 注：下方「Day N」对齐 `study-plan-60d.md`（计划 Day）。2026-08-15 当天含两讲——「具身智能定义与研究版图」为 Day 1（P1），「硬件实体」为 Day 2（P2），其余按日期顺序顺延。


## 阶段总览（P1–P11）

| 阶段 | 主题 | 集号范围 | 天数 | 篇数 |
|------|------|---------|------|------|
| P1 | 概念入门（具身智能定义/体系） | 001–007 | Day 1 | 2 |
| P2 | 硬件实体（电机/舵机/传感器/3D） | 008–012 | Day 2 | 2 |
| P3 | 虚拟仿真与 URDF 建模 | 013–026 | Day 3–5 | 6 |
| P4 | 上下位机通讯 / 标定 / WebSocket | 027–050 | Day 6–11 | 12 |
| P5 | 运动学 正解FK / 逆解IK | 051–067 | Day 12–16 | 10 |
| P6 | 控制论与 PID | 068–080 | Day 17–20 | 8 |
| P7 | 计算机视觉 OpenCV | 081–115 | Day 21–28 | 16 |
| P8 | 机器学习 / 深度学习 / YOLO | 116–160 | Day 29–41 | 26 |
| P9 | 语音 / 大模型 / Ollama / MCP | 161–187 | Day 42–50 | 18 |
| P10 | 行为克隆 BC（ALOHA / 数据采集 / 训练） | 188–207 | Day 51–56 | 12 |
| P11 | 强化学习 / 遗传神经网络 | 208–223 | Day 57–60 | 8 |

## 笔记清单（按阶段）

### P1 · 概念入门（具身智能定义/体系）（Day 1，集号 001–007）

- **Day 1**（2026-08-15）：[2026-08-15-Embodied-Intelligence-Definition-and-Research-Landscape-en](2026-08-15-Embodied-Intelligence-Definition-and-Research-Landscape-en.md)
- **Day 1**（2026-08-15）：[2026-08-15-具身智能定义与研究版图-zh](2026-08-15-具身智能定义与研究版图-zh.md)

### P2 · 硬件实体（电机/舵机/传感器/3D）（Day 2，集号 008–012）

- **Day 2**（2026-08-15）：[2026-08-15-Robot-Hardware-Actuators-Reduction-Encoders-en](2026-08-15-Robot-Hardware-Actuators-Reduction-Encoders-en.md)
- **Day 2**（2026-08-15）：[2026-08-15-机器人硬件实体-执行器减速编码器-zh](2026-08-15-机器人硬件实体-执行器减速编码器-zh.md)

### P3 · 虚拟仿真与 URDF 建模（Day 3–5，集号 013–026）

- **Day 3**（2026-08-16）：[2026-08-16-Simulation-and-URDF-Fundamentals-en](2026-08-16-Simulation-and-URDF-Fundamentals-en.md)
- **Day 3**（2026-08-16）：[2026-08-16-虚拟仿真与URDF入门-zh](2026-08-16-虚拟仿真与URDF入门-zh.md)
- **Day 4**（2026-08-17）：[2026-08-17-URDF-Tags-and-Node.js-Simulation-Environment-en](2026-08-17-URDF-Tags-and-Node.js-Simulation-Environment-en.md)
- **Day 4**（2026-08-17）：[2026-08-17-URDF标签详解与Node.js仿真环境-zh](2026-08-17-URDF标签详解与Node.js仿真环境-zh.md)
- **Day 5**（2026-08-18）：[2026-08-18-URDF-Robot-Arm-Model-Assembly-en](2026-08-18-URDF-Robot-Arm-Model-Assembly-en.md)
- **Day 5**（2026-08-18）：[2026-08-18-URDF机械臂模型拼装实战-zh](2026-08-18-URDF机械臂模型拼装实战-zh.md)

### P4 · 上下位机通讯 / 标定 / WebSocket（Day 6–11，集号 027–050）

- **Day 6**（2026-08-19）：[2026-08-19-Upper-Lower-Computer-Comm-and-Servo-ID-Scanning-en](2026-08-19-Upper-Lower-Computer-Comm-and-Servo-ID-Scanning-en.md)
- **Day 6**（2026-08-19）：[2026-08-19-上下位机通讯与舵机ID扫描配置-zh](2026-08-19-上下位机通讯与舵机ID扫描配置-zh.md)
- **Day 7**（2026-08-20）：[2026-08-20-Python-Dependency-and-conda-Environment-Setup-en](2026-08-20-Python-Dependency-and-conda-Environment-Setup-en.md)
- **Day 7**（2026-08-20）：[2026-08-20-Python依赖安装与conda环境搭建-zh](2026-08-20-Python依赖安装与conda环境搭建-zh.md)
- **Day 8**（2026-08-21）：[2026-08-21-Calibration-Principle-and-Servo-Calibration-Algorithm-en](2026-08-21-Calibration-Principle-and-Servo-Calibration-Algorithm-en.md)
- **Day 8**（2026-08-21）：[2026-08-21-标定原理与舵机标定算法-zh](2026-08-21-标定原理与舵机标定算法-zh.md)
- **Day 9**（2026-08-22）：[2026-08-22-Teleoperation-Concepts-and-Teacher-Arm-Calibration-Completion-en](2026-08-22-Teleoperation-Concepts-and-Teacher-Arm-Calibration-Completion-en.md)
- **Day 9**（2026-08-22）：[2026-08-22-遥操作概念与教师端标定完成-zh](2026-08-22-遥操作概念与教师端标定完成-zh.md)
- **Day 10**（2026-08-23）：[2026-08-23-AI-Generated Servo-Angle Monitoring + WebSocket Real-Time Communication-en](2026-08-23-AI-Generated Servo-Angle Monitoring + WebSocket Real-Time Communication-en.md)
- **Day 10**（2026-08-23）：[2026-08-23-AI生成角度监控程序与WebSocket实时通讯-zh](2026-08-23-AI生成角度监控程序与WebSocket实时通讯-zh.md)
- **Day 11**（2026-08-24）：[2026-08-24-Real-Arm-Angles-and-Action-Recording-en](2026-08-24-Real-Arm-Angles-and-Action-Recording-en.md)
- **Day 11**（2026-08-24）：[2026-08-24-读取真实机械臂角度与动作录制回放-zh](2026-08-24-读取真实机械臂角度与动作录制回放-zh.md)

### P5 · 运动学 正解FK / 逆解IK（Day 12–16，集号 051–067）

- **Day 12**（2026-08-25）：[2026-08-25-Forward-Kinematics-FK-en](2026-08-25-Forward-Kinematics-FK-en.md)
- **Day 12**（2026-08-25）：[2026-08-25-机器人运动学正运动学FK-zh](2026-08-25-机器人运动学正运动学FK-zh.md)
- **Day 13**（2026-08-26）：[2026-08-26-Matrix-Math-and-Homogeneous-Transform-en](2026-08-26-Matrix-Math-and-Homogeneous-Transform-en.md)
- **Day 13**（2026-08-26）：[2026-08-26-矩阵运算与末端求解齐次变换-zh](2026-08-26-矩阵运算与末端求解齐次变换-zh.md)
- **Day 14**（2026-08-27）：[2026-08-27-Inverse-Kinematics-Multiplicity-en](2026-08-27-Inverse-Kinematics-Multiplicity-en.md)
- **Day 14**（2026-08-27）：[2026-08-27-逆运动学多解性与难题-zh](2026-08-27-逆运动学多解性与难题-zh.md)
- **Day 15**（2026-08-28）：[2026-08-28-IK-Solving-Methods-Geometric-vs-Numerical-en](2026-08-28-IK-Solving-Methods-Geometric-vs-Numerical-en.md)
- **Day 15**（2026-08-28）：[2026-08-28-逆解求解方法几何法数值法-zh](2026-08-28-逆解求解方法几何法数值法-zh.md)
- **Day 16**（2026-08-29）：[2026-08-29-IK-Application-and-Keyboard-Control-en](2026-08-29-IK-Application-and-Keyboard-Control-en.md)
- **Day 16**（2026-08-29）：[2026-08-29-逆解应用与键盘控制-zh](2026-08-29-逆解应用与键盘控制-zh.md)

### P6 · 控制论与 PID（Day 17–20，集号 068–080）

- **Day 17**（2026-08-30）：[2026-08-30-Control-Theory-Open-loop-vs-Closed-loop-en](2026-08-30-Control-Theory-Open-loop-vs-Closed-loop-en.md)
- **Day 17**（2026-08-30）：[2026-08-30-控制理论开环与闭环系统-zh](2026-08-30-控制理论开环与闭环系统-zh.md)
- **Day 18**（2026-08-31）：[2026-08-31-PID-Algorithm-Proportional-Integral-Derivative-en](2026-08-31-PID-Algorithm-Proportional-Integral-Derivative-en.md)
- **Day 18**（2026-08-31）：[2026-08-31-PID算法比例积分微分-zh](2026-08-31-PID算法比例积分微分-zh.md)
- **Day 19**（2026-09-01）：[2026-09-01-Motor-ID-and-Student-Side-Mid-Calibration-en](2026-09-01-Motor-ID-and-Student-Side-Mid-Calibration-en.md)
- **Day 19**（2026-09-01）：[2026-09-01-电机ID设置与学生端中位校准-zh](2026-09-01-电机ID设置与学生端中位校准-zh.md)
- **Day 20**（2026-09-02）：[2026-09-02-Student-Side-Angle-Control-and-Teleoperation-en](2026-09-02-Student-Side-Angle-Control-and-Teleoperation-en.md)
- **Day 20**（2026-09-02）：[2026-09-02-学生端角度控制与遥操作-zh](2026-09-02-学生端角度控制与遥操作-zh.md)

### P7 · 计算机视觉 OpenCV（Day 21–28，集号 081–115）

- **Day 21**（2026-09-03）：[2026-09-03-Computer-Vision-Intro-and-OpenCV-en](2026-09-03-Computer-Vision-Intro-and-OpenCV-en.md)
- **Day 21**（2026-09-03）：[2026-09-03-计算机视觉入门与OpenCV-zh](2026-09-03-计算机视觉入门与OpenCV-zh.md)
- **Day 22**（2026-09-04）：[2026-09-04-ROI-and-Color-Sorting-HSV-Mean-Filter-en](2026-09-04-ROI-and-Color-Sorting-HSV-Mean-Filter-en.md)
- **Day 22**（2026-09-04）：[2026-09-04-ROI与颜色分拣HSV均值滤波-zh](2026-09-04-ROI与颜色分拣HSV均值滤波-zh.md)
- **Day 23**（2026-09-05）：[2026-09-05-Hand-Eye-Calibration-and-Pixel-to-Physical-Mapping-en](2026-09-05-Hand-Eye-Calibration-and-Pixel-to-Physical-Mapping-en.md)
- **Day 23**（2026-09-05）：[2026-09-05-手眼标定与像素物理坐标映射-zh](2026-09-05-手眼标定与像素物理坐标映射-zh.md)
- **Day 24**（2026-09-06）：[2026-09-06-FK-IK-Example-Code-and-Arm-Control-Landing-en](2026-09-06-FK-IK-Example-Code-and-Arm-Control-Landing-en.md)
- **Day 24**（2026-09-06）：[2026-09-06-正解反解示例与机械臂控制落地-zh](2026-09-06-正解反解示例与机械臂控制落地-zh.md)
- **Day 25**（2026-09-07）：[2026-09-07-Shape-Detection-Difference-and-Color-Tracking-en](2026-09-07-Shape-Detection-Difference-and-Color-Tracking-en.md)
- **Day 25**（2026-09-07）：[2026-09-07-形状侦测差值识别与颜色追踪-zh](2026-09-07-形状侦测差值识别与颜色追踪-zh.md)
- **Day 26**（2026-09-08）：[2026-09-08-Eye-in-Hand-Follow-Control-and-Vision-Kinematics-Integration-en](2026-09-08-Eye-in-Hand-Follow-Control-and-Vision-Kinematics-Integration-en.md)
- **Day 26**（2026-09-08）：[2026-09-08-眼在手上跟随控制与视觉运动学联调-zh](2026-09-08-眼在手上跟随控制与视觉运动学联调-zh.md)
- **Day 27**（2026-09-09）：[2026-09-09-Bird-eye-Affine-Object-Pose-and-QR-Recognition-en](2026-09-09-Bird-eye-Affine-Object-Pose-and-QR-Recognition-en.md)
- **Day 27**（2026-09-09）：[2026-09-09-鸟瞰仿射物体姿态与二维码识别-zh](2026-09-09-鸟瞰仿射物体姿态与二维码识别-zh.md)
- **Day 28**（2026-09-10）：[2026-09-10-Face-Emotion-Part-Counting-and-Traditional-CV-Limits-en](2026-09-10-Face-Emotion-Part-Counting-and-Traditional-CV-Limits-en.md)
- **Day 28**（2026-09-10）：[2026-09-10-人脸情绪零件计数与传统机器视觉缺陷-zh](2026-09-10-人脸情绪零件计数与传统机器视觉缺陷-zh.md)

### P8 · 机器学习 / 深度学习 / YOLO（Day 29–41，集号 116–160）

- **Day 29**（2026-09-11）：[2026-09-11-Machine-Learning-Basics-Features-and-Labels-en](2026-09-11-Machine-Learning-Basics-Features-and-Labels-en.md)
- **Day 29**（2026-09-11）：[2026-09-11-机器学习入门与端到端三要素-zh](2026-09-11-机器学习入门与端到端三要素-zh.md)
- **Day 30**（2026-09-12）：[2026-09-12-Dataset-Splitting-Modeling-Flow-and-Feature-Engineering-en](2026-09-12-Dataset-Splitting-Modeling-Flow-and-Feature-Engineering-en.md)
- **Day 30**（2026-09-12）：[2026-09-12-数据集划分与建模流程特征工程-zh](2026-09-12-数据集划分与建模流程特征工程-zh.md)
- **Day 31**（2026-09-13）：[2026-09-13-MSE-Gradient-Descent-and-Cross-Entropy-en](2026-09-13-MSE-Gradient-Descent-and-Cross-Entropy-en.md)
- **Day 31**（2026-09-13）：[2026-09-13-MSE梯度下降与分类交叉熵-zh](2026-09-13-MSE梯度下降与分类交叉熵-zh.md)
- **Day 32**（2026-09-14）：[2026-09-14-Linear-Regression-and-the-XOR-Problem-en](2026-09-14-Linear-Regression-and-the-XOR-Problem-en.md)
- **Day 32**（2026-09-14）：[2026-09-14-sklearn线性回归与异或问题-zh](2026-09-14-sklearn线性回归与异或问题-zh.md)
- **Day 33**（2026-09-15）：[2026-09-15-Feature-Engineering-Neural-Nets-and-MNIST-en](2026-09-15-Feature-Engineering-Neural-Nets-and-MNIST-en.md)
- **Day 33**（2026-09-15）：[2026-09-15-特征工程神经网络组拼与MNIST-zh](2026-09-15-特征工程神经网络组拼与MNIST-zh.md)
- **Day 34**（2026-09-16）：[2026-09-16-Training-Saving-and-Camera-Capture-Preprocessing-en](2026-09-16-Training-Saving-and-Camera-Capture-Preprocessing-en.md)
- **Day 34**（2026-09-16）：[2026-09-16-神经网络训练保存与摄像头捕获预处理-zh](2026-09-16-神经网络训练保存与摄像头捕获预处理-zh.md)
- **Day 35**（2026-09-17）：[2026-09-17-Handwritten-Digit-Inference-and-Full-Case-en](2026-09-17-Handwritten-Digit-Inference-and-Full-Case-en.md)
- **Day 35**（2026-09-17）：[2026-09-17-手写数字识别推理与综合案例-zh](2026-09-17-手写数字识别推理与综合案例-zh.md)
- **Day 36**（2026-09-18）：[2026-09-18-Confusion-Matrix-Precision-Recall-and-F1-en](2026-09-18-Confusion-Matrix-Precision-Recall-and-F1-en.md)
- **Day 36**（2026-09-18）：[2026-09-18-混淆矩阵与查准率查全率F1-zh](2026-09-18-混淆矩阵与查准率查全率F1-zh.md)
- **Day 37**（2026-09-19）：[2026-09-19-YOLO-Installation-Inference-and-Usage-en](2026-09-19-YOLO-Installation-Inference-and-Usage-en.md)
- **Day 37**（2026-09-19）：[2026-09-19-YOLO安装推理与使用说明-zh](2026-09-19-YOLO安装推理与使用说明-zh.md)
- **Day 38**（2026-09-20）：[2026-09-20-YOLO-Annotation-Dataset-and-Training-Config-en](2026-09-20-YOLO-Annotation-Dataset-and-Training-Config-en.md)
- **Day 38**（2026-09-20）：[2026-09-20-YOLO数据标注与训练配置-zh](2026-09-20-YOLO数据标注与训练配置-zh.md)
- **Day 39**（2026-09-21）：[2026-09-21-YOLO-Training-and-CNN-Convolution-Basics-en](2026-09-21-YOLO-Training-and-CNN-Convolution-Basics-en.md)
- **Day 39**（2026-09-21）：[2026-09-21-YOLO训练与CNN卷积入门-zh](2026-09-21-YOLO训练与CNN卷积入门-zh.md)
- **Day 40**（2026-09-22）：[2026-09-22-CNN-Pooling-Flatten-and-Data-Collection-Planning-en](2026-09-22-CNN-Pooling-Flatten-and-Data-Collection-Planning-en.md)
- **Day 40**（2026-09-22）：[2026-09-22-CNN池化打平与数据收集需求-zh](2026-09-22-CNN池化打平与数据收集需求-zh.md)
- **Day 41**（2026-09-23）：[2026-09-23-Image-Synthesis-Auto-Labeling-and-YOLO-Launch-en](2026-09-23-Image-Synthesis-Auto-Labeling-and-YOLO-Launch-en.md)
- **Day 41**（2026-09-23）：[2026-09-23-图像合成自动标注与YOLO训练启动-zh](2026-09-23-图像合成自动标注与YOLO训练启动-zh.md)

### P9 · 语音 / 大模型 / Ollama / MCP（Day 42–50，集号 161–187）

- **Day 42**（2026-09-24）：[2026-09-24-Audio-Recording-ASR-and-Rule-Based-Dialogue-en](2026-09-24-Audio-Recording-ASR-and-Rule-Based-Dialogue-en.md)
- **Day 42**（2026-09-24）：[2026-09-24-音频录制语音转文本与规则语音对答-zh](2026-09-24-音频录制语音转文本与规则语音对答-zh.md)
- **Day 43**（2026-09-25）：[2026-09-25-Voice-Chat-System-TTS-and-Full-Dialogue-Flow-en](2026-09-25-Voice-Chat-System-TTS-and-Full-Dialogue-Flow-en.md)
- **Day 43**（2026-09-25）：[2026-09-25-语音聊天系统与TTS语音对话全流程-zh](2026-09-25-语音聊天系统与TTS语音对话全流程-zh.md)
- **Day 44**（2026-09-26）：[2026-09-26-Integrating-an-LLM-and-Flow-Limitations-en](2026-09-26-Integrating-an-LLM-and-Flow-Limitations-en.md)
- **Day 44**（2026-09-26）：[2026-09-26-对接大模型语音开发与流程缺陷-zh](2026-09-26-对接大模型语音开发与流程缺陷-zh.md)
- **Day 45**（2026-09-27）：[2026-09-27-LLM-Concepts-Transformer-DeepSeek-and-Distillation-en](2026-09-27-LLM-Concepts-Transformer-DeepSeek-and-Distillation-en.md)
- **Day 45**（2026-09-27）：[2026-09-27-大模型概念底层原理与DeepSeek蒸馏-zh](2026-09-27-大模型概念底层原理与DeepSeek蒸馏-zh.md)
- **Day 46**（2026-09-28）：[2026-09-28-Ollama-Installation-Model-Loading-and-Commands-en](2026-09-28-Ollama-Installation-Model-Loading-and-Commands-en.md)
- **Day 46**（2026-09-28）：[2026-09-28-Ollama安装模型加载与常用命令-zh](2026-09-28-Ollama安装模型加载与常用命令-zh.md)
- **Day 47**（2026-09-29）：[2026-09-29-Hyperparameter-Tuning-Chatbox-and-Ollama-API-en](2026-09-29-Hyperparameter-Tuning-Chatbox-and-Ollama-API-en.md)
- **Day 47**（2026-09-29）：[2026-09-29-大模型超参调整与代码调用Ollama-zh](2026-09-09-大模型超参调整与代码调用Ollama-zh.md)
- **Day 48**（2026-09-30）：[2026-09-30-Web-and-GUI-Chat-Assistant-en](2026-09-30-Web-and-GUI-Chat-Assistant-en.md)
- **Day 48**（2026-09-30）：[2026-09-30-网页与GUI聊天助手-zh](2026-09-30-网页与GUI聊天助手-zh.md)
- **Day 49**（2026-10-01）：[2026-10-01-MCP-Model-Context-Protocol-and-Hardware-Control-en](2026-10-01-MCP-Model-Context-Protocol-and-Hardware-Control-en.md)
- **Day 49**（2026-10-01）：[2026-10-01-MCP模型上下文协议与大模型控硬件-zh](2026-10-01-MCP模型上下文协议与大模型控硬件-zh.md)
- **Day 50**（2026-10-02）：[2026-10-02-MCP-Effect-Demo-and-ALOHA-Bimanual-Teleop-Intro-en](2026-10-02-MCP-Effect-Demo-and-ALOHA-Bimanual-Teleop-Intro-en.md)
- **Day 50**（2026-10-02）：[2026-10-02-MCP效果展示与ALOHA双臂遥操作介绍-zh](2026-10-02-MCP效果展示与ALOHA双臂遥操作介绍-zh.md)

### P10 · 行为克隆 BC（ALOHA / 数据采集 / 训练）（Day 51–56，集号 188–207）

- **Day 51**（2026-10-03）：[2026-10-03-End-to-End-Behavior-Cloning-and-RL-vs-BC-Concepts-en](2026-10-03-End-to-End-Behavior-Cloning-and-RL-vs-BC-Concepts-en.md)
- **Day 51**（2026-10-03）：[2026-10-03-端到端行为克隆与RL-BC概念辨析-zh](2026-10-03-端到端行为克隆与RL-BC概念辨析-zh.md)
- **Day 52**（2026-10-04）：[2026-10-04-Git-Version-Control-and-genkiarm-Open-Source-Arm-Setup-en](2026-10-04-Git-Version-Control-and-genkiarm-Open-Source-Arm-Setup-en.md)
- **Day 52**（2026-10-04）：[2026-10-04-Git版本控制与开源机械臂项目genkiarm安装-zh](2026-10-04-Git版本控制与开源机械臂项目genkiarm安装-zh.md)
- **Day 53**（2026-10-05）：[2026-10-05-Proxy-Setup-and-Teacher-Arm-Calibration-with-Dual-Side-Alignment-en](2026-10-05-Proxy-Setup-and-Teacher-Arm-Calibration-with-Dual-Side-Alignment-en.md)
- **Day 53**（2026-10-05）：[2026-10-05-代理设置与teacher主臂标定及双端对齐-zh](2026-10-05-代理设置与teacher主臂标定及双端对齐-zh.md)
- **Day 54**（2026-10-06）：[2026-10-06-Teleop-Check-and-BC-Dataset-Recording-Replay-en](2026-10-06-Teleop-Check-and-BC-Dataset-Recording-Replay-en.md)
- **Day 54**（2026-10-06）：[2026-10-06-遥操作检查与行为克隆数据集录制回放-zh](2026-10-06-遥操作检查与行为克隆数据集录制回放-zh.md)
- **Day 55**（2026-10-07）：[2026-10-07-BC-Effect-Demo-and-Local-Training-Pipeline-en](2026-10-07-BC-Effect-Demo-and-Local-Training-Pipeline-en.md)
- **Day 55**（2026-10-07）：[2026-10-07-行为克隆效果展示与本地训练流程-zh](2026-10-07-行为克隆效果展示与本地训练流程-zh.md)
- **Day 56**（2026-10-08）：[2026-10-08-Cloud-Server-Training-nohup-Background-and-Firewall-Download-en](2026-10-08-Cloud-Server-Training-nohup-Background-and-Firewall-Download-en.md)
- **Day 56**（2026-10-08）：[2026-10-08-云服务器训练与nohup后台及防火墙下载-zh](2026-10-08-云服务器训练与nohup后台及防火墙下载-zh.md)

### P11 · 强化学习 / 遗传神经网络（Day 57–60，集号 208–223）

- **Day 57**（2026-10-09）：[2026-10-09-RL-Five-Key-Concepts-and-MDP-Markov-Decision-Process-en](2026-10-09-RL-Five-Key-Concepts-and-MDP-Markov-Decision-Process-en.md)
- **Day 57**（2026-10-09）：[2026-10-09-强化学习五大概念与MDP马尔可夫决策过程-zh](2026-10-09-强化学习五大概念与MDP马尔可夫决策过程-zh.md)
- **Day 58**（2026-10-10）：[2026-10-10-MDP-RL-Relation-and-Gym-Environment-Getting-Started-en](2026-10-10-MDP-RL-Relation-and-Gym-Environment-Getting-Started-en.md)
- **Day 58**（2026-10-10）：[2026-10-10-MDP与强化学习关系及Gym环境上手-zh](2026-10-10-MDP与强化学习关系及Gym环境上手-zh.md)
- **Day 59**（2026-10-11）：[2026-10-11-Q-learning-Tabular-Method-Principle-and-Code-en](2026-10-11-Q-learning-Tabular-Method-Principle-and-Code-en.md)
- **Day 59**（2026-10-11）：[2026-10-11-Q-learning表格法原理与代码实现-zh](2026-10-11-Q-learning表格法原理与代码实现-zh.md)
- **Day 60**（2026-10-12）：[2026-10-12-DQN-Deep-RL-HuggingFace-and-Genetic-NN-Graduation-en](2026-10-12-DQN-Deep-RL-HuggingFace-and-Genetic-NN-Graduation-en.md)
- **Day 60**（2026-10-12）：[2026-10-12-DQN深度强化学习与HuggingFace及遗传神经网络结营-zh](2026-10-12-DQN深度强化学习与HuggingFace及遗传神经网络结营-zh.md)


---

*共 **120 篇**（Day 1–60，每讲中英各一）。计划详见根目录 `study-plan-60d.md`。*

*本系列为通用具身智能学习笔记，不是军事专题。*
