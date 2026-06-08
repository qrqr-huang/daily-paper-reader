---
title: Optimal Sensor Scheduling and Selection for Continuous-Discrete Kalman Filtering with Auxiliary Dynamics
title_zh: 带辅助动力学的连续-离散卡尔曼滤波的最优传感器调度与选择
authors: "Mohamad Al Ahdab, John Leth, Zheng-Hua Tan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=CAPNgWkEEk"
tags: ["query:lfp-soc"]
score: 7.0
evidence: 开发了用于连续-离散卡尔曼滤波的最优传感器调度方法，可用于电池荷电状态估计。
tldr: 现有卡尔曼滤波中传感器测量往往固定且无约束，本文提出一种最优传感器调度与选择方法，在连续-离散状态空间模型中引入辅助动力学，模拟测量过程与辅助状态耦合。通过泊松过程建模测量发生，设计算法最小化估计误差同时满足成本约束。实验验证该方法在多种场景下均能有效提升滤波精度，为电池荷电状态估计等实际应用中的传感器管理提供理论支撑。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1048, \"height\": 2153, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1022, \"height\": 1385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1729, \"height\": 1787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1730, \"height\": 1417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1740, \"height\": 1491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1737, \"height\": 1718, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1725, \"height\": 1643, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1723, \"height\": 1639, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1723, \"height\": 1638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-capngwkeek/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1732, \"height\": 1763, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-capngwkeek/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 968, \"label\": \"Table\"}]"
motivation: 现有卡尔曼滤波器在多传感器场景下缺乏对测量调度和传感器选择的优化，尤其当测量过程涉及辅助动力学和成本约束时。
method: 提出将测量发生建模为独立泊松过程，结合辅助状态空间模型，设计最优调度策略以最小化估计误差。
result: 实验表明，该方法在多种模拟场景下能够显著提高滤波精度，并有效管理传感器资源。
conclusion: 为带约束的传感器管理提供了理论框架，可直接应用于电池管理系统的状态估计。
---

## Abstract
We study the Continuous-Discrete Kalman Filter (CD-KF) for State-Space Models (SSMs) where continuous-time dynamics are observed via multiple sensors with discrete, irregularly timed measurements. Our focus extends to scenarios in which the measurement process is coupled with the states of an auxiliary SSM. For instance, higher measurement rates may increase energy consumption or heat generation, while a sensor’s accuracy can depend on its own spatial trajectory or that of the measured target. Each sensor thus carries distinct costs and constraints associated with its measurement rate and additional constraints and costs on the auxiliary state. We model measurement occurrences as independent Poisson processes with sensor-specific rates and derive an upper bound on the mean posterior covariance matrix of the CD-KF along the mean auxiliary state. The bound is continuously differentiable with respect to the measurement rates, which enables efficient gradient-based optimization. Exploiting this bound, we propose a finite-horizon optimal control framework to optimize measurement rates and auxiliary-state dynamics jointly. We further introduce a deterministic method for scheduling measurement times from the optimized rates. Empirical results in state-space filtering and dynamic temporal Gaussian process regression demonstrate that our approach achieves improved trade-offs between resource usage and estimation accuracy.

---

## 论文详细总结（自动生成）

## 论文总结：《带辅助动力学的连续-离散卡尔曼滤波的最优传感器调度与选择》

### 1. 核心问题与研究动机
- **背景**：许多实际动态系统（如环境污染监测、卫星观测、血糖检测）中，待估计的连续时间状态只能通过多个传感器以离散、不规则的时间进行观测。
- **核心挑战**：传感器的测量过程往往与**辅助动力学变量**耦合（如测量能耗、传感器温度、位置轨迹导致的精度变化、辐射损伤等），且不同传感器具有不同的测量代价与约束。
- **研究目标**：在连续-离散状态空间模型中，联合优化**多个传感器的测量调度**以及**辅助动力学系统的控制输入**，以在给定资源限制下最大程度降低状态估计的不确定性。

### 2. 方法论核心思想与技术细节
- **随机化测量建模**：将每个传感器 `s` 的测量到达建模为**时变强度的独立泊松过程** `N_s(t)`，强度为 `λ_s(t)`。这使得协方差矩阵和辅助状态成为随机微分方程的解。
- **两个关键上界**：
    - **命题 6.1 (协方差上界)**：利用卡尔曼更新映射的凸性（引理 A.1），通过詹森不等式和比较定理，推导出后验协方差矩阵 `Σ(t)` 在给定辅助状态均值下的**上界 `ˆΣ(t)`**，该上界满足关于 `λ_s` 的确定性微分方程。
    - **命题 6.2 (辅助状态上界)**：假设辅助状态 `ξ_p` 的动态函数具有凹性/凸性（如仿射系统自然满足），导出辅助状态均值的上界或下界 `ˆξ_p(t)`。
    - 这两个上界关于测量速率 `λ_s` 是**连续可微的**，从而支持基于梯度的数值优化。
- **最优控制问题 (OCP) 构建**：将原问题转化为有限时域的确定性最优控制问题 (12)。目标函数和约束均为 `ˆΣ` 和 `ˆξ` 的单调函数，确保上界提供有意义的保守设计。决策变量包括测量速率 `λ(t)` 和控制输入 `u(t)`。
- **确定性的测量时刻生成**：求解 OCP 得到优化速率 `λ_s(t)` 后，通过**最小化瓦瑟斯坦‑2 距离**，将连续的速率分布量化为确定性的测量时间点。命题 8.1 给出闭合形式的条件质心公式，能精确匹配平均测量次数，且计算高效。
- **滚动时域扩展**：对于非线性或未知的真实动态，可采用滚动时域（模型预测控制）框架，每次更新估计后重新求解 OCP，并结合扩展卡尔曼滤波器 (EKF) 处理非线性。

### 3. 实验设计与对比方法
实验在 **4 个主要场景** 下开展，并对比了多种基准策略：
- **场景 1：机器人环境监测** 机器人携带两个传感器（精度与能耗不同），需在有限能量下移动到目标点测量、返回基站充电，并最小化过程 GP 回归的估计误差。
- **场景 2：放射性环境扩展** 在场景 1 基础上增加辐射损伤动态，传感器精度随损伤指数衰减。
- **场景 3：水质量监测与主动除垢** 双传感器，测量会加重结垢（精度下降），可启用除垢输入恢复精度，需平衡测量、除垢成本与估计精度。
- **场景 4：航天器对地监测** 两架航天器，每架携带两个传感器（昼间精度高但易损耗的传感器 vs. 全天可用但耗能大的传感器），需利用太阳能充电并管理能量与传感器损伤。
- **对比方法**：
    - **随机 (Random)**：均匀时间格点，以恒定速率泊松采样。
    - **贪婪 (Greedy)**：每一步选择使预测协方差迹下降最大且代价可接受的传感器。
    - **M‑Optimized**：从优化速率多次随机采样，选代价最小的实现（用于验证确定性调度）。
- **评估指标**：协方差迹、能量水平、辐射/结垢损伤的均值、标准差与最差情况。

### 4. 资源与算力
- 论文 **未明确提及使用 GPU** 或大规模并行训练。
- 最优控制问题的求解通过 IPOPT 在 CPU（Intel Core Ultra 7 155H @ 1.40 GHz, 64 GB RAM）上完成，文中仅对不同离散化点数下的优化时间给出了示例（图2），例如 400 点约需 3 秒。
- 因此，该方法属于轻量级优化，不依赖大规模算力。

### 5. 实验数量与充分性
- 共包含 **4 个主实验场景**，每个场景均与 3 种基准方法对比，提供定量统计表格。
- 附录中额外包含：
    - **越界假设验证**：4 组违背凹性/凸性假设的案例（机器人辐射损伤、能量动态、水结垢动态的非凸修改），展示了方法的鲁棒性。
    - **滚动时域目标跟踪**：用错误模型（恒定速度）跟踪真实转弯率目标，验证在线重规划的可行性。
    - **离散化点数影响分析**：证明随着点数增加，结果收敛。
- 实验设计覆盖了多种约束类型（能量、损伤、精度衰减）和不同的控制目标，对比公平；但**所有场景均为仿真**，未使用真实传感器数据。

### 6. 主要结论与发现
- 提出的 OCP 框架能**有效联合优化测量速率与辅助输入**，生成的调度方案在权衡资源与估计精度方面显著优于随机和贪婪策略。
- 基于瓦瑟斯坦距离的**确定性时间量化**能够逼近优化速率的平均行为，且避免了多次随机采样，计算代价低。
- 即使在辅助动力学不严格满足凹性/凸性假设时，方法仍能以**近似或启发式的方式**提供良好性能。
- 滚动时域扩展使非线性或模型不准确的场景得以应用，且保持较小协方差。

### 7. 方法优势与亮点
- **可微上界**：将随机调度问题转化为确定性梯度优化问题，使得可融入标准数值最优控制求解器。
- **通用框架**：可处理多种辅助动态（能量、位置、损伤、结垢），并统一纳入 OCP。
- **闭环可行**：确定性调度方法保证测量次数与平均一致，避免随机波动带来的约束违反风险。
- **模块灵活**：可结合滚动时域、EKF 等扩展至非线性/不确定系统。

### 8. 不足与局限
- **对辅助状态凹/凸性的依赖**：若辅助动态不满足该假设（或非线性程度强），理论保证失效，只能作为启发式近似。
- **仿真验证为主**：缺乏真实硬件或物理传感器的实验验证，实际传感器噪声模型、延迟等未考虑。
- **模型复杂度**：OCP 状态维度随传感器数和辅助维度增加，求解时间可能增长，文中未讨论扩展性极限。
- **目标函数设定**：需要人工设计代价权重（如 `w_Σ`、`w_λ`），对问题敏感，缺乏自动化调优建议。
- **泊松假设**：实际测量可能无法严格用无记忆泊松过程描述（如周期性规避窗口），框架适用性受限。

（完）
