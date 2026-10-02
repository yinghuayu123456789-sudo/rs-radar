# 高光谱研究雷达 · 日报（2026-10-02 · 关键词策略验收运行 C）

**来源与时间窗口**：arXiv API（20 条查询全部 HTTP 200，无 429/503）＋ CVF openaccess（CVPR2026 本地索引，4,042 条）
**请求窗口**：2026-09-25 → 2026-10-02（近 7 天）｜**实测有效窗口**：2026-09-25 → 2026-09-30（arXiv 公告滞后约 2 天，见 §7）
**生成日期**：2026-10-02
**策略版本（本次评测固定在此版本）**：

| 文件 | sha256 |
|---|---|
| `scripts/radar_filter.py` | `f2e50032bc1dceb462e5428039fbc61f699ffad39a151f087bfe7a95a80944f6` |
| `scripts/radar_keywords.py` | `613c72954980e54835acee801d09dccd7e0cc6cc6bb46b8ef58aa0703dbf86ba` |
| `scripts/search_keywords.txt` | `4382dbe26daf16d6512c1b27d52cbda23c9bc3aad96a796ee236bc25f7d9c81f` |

`radar_filter.py --selftest` → **13/13 passed**。筛选前后两次哈希一致，说明本轮结果出自同一版本（运行中有另一会话在改同一批判策略文件，见 §8）。

---

## 1. 本期要点

1. **筛选结果：候选 16 篇 → 入选 7 篇**（上一轮同日运行 B：16 → 2）。增量来自四处策略改动，且每一处都能对上具体论文（§8 给出逐条归因）。
2. **② 高光谱超分是本期最厚的一档（3 篇）**，且都指向同一个技术母题：**把超分从"预测光谱值/像素"改成"预测算子/整流"**——OmniHSR 预测空间算子、SSRON 学函数到函数的算子映射、SR²-Net 做骨干无关的光谱整流。这是一个可写进 related work 的收敛趋势。
3. **① C 组（超分＋下游任务联合优化）本期 0 篇**——不是筛选漏掉，而是 7 天窗口内确实没有这类投稿（C 组已扩到 7 个关键词仍无命中）。对用户方向而言这是**空白区**，见 §5 选题三。
4. **④ D 组首次真正吃到论文（3 篇）**：HyperSAM（提示式高光谱基础模型）、Hyperspectral Image Models（55 模型 / 24 场景统一评测）、NE-LoRA（星上参数高效适配）。其中 NE-LoRA 正是上一轮标记为"显然属 ③ 档但永远进不来"的那篇，本次新增 `[D_ADAPT]` 子组后正常入选。
5. **会议面没有新增**：CVPR2026 索引里高光谱只有 3 篇（全部 p2 超分），且已在同日更早的运行中被 spotlight 消费；arXiv × 会议匹配 0 篇的原因已逐篇查实（§6），**不是匹配器漏配**。

---

## 2. 高光谱筛选结果

（`radar_filter.py` 原始输出，未手工改动）

## 高光谱筛选结果

- 候选：16 篇 → **入选 7 篇**（过滤掉 9 篇）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C/D 关键词之一；pansharpening、multispectral 单独出现不算；SAR/雷达类无条件剔除

| 优先 | 标题 | 来源 | 命中组 | 为什么值得看 |
|---|---|---|---|---|
| ② 高光谱超分 (A) | Correcting Spectra Outside the Backbone: A Model-Agnostic Rectifier for Hyperspectral Image Super-Resolution | 2601.21338v2 | A | |
| ② 高光谱超分 (A) | Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks | 2609.35410v1 | A | |
| ② 高光谱超分 (A) | Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators | 2609.39926v1 | A | |
| ③ 高光谱分类 (B) | Adaptive Subspace Modeling With Functional Tucker Decomposition | 2603.25530v2 | B | |
| ④ 高光谱基础模型/少样本 (D) | HyperSAM: A Promptable Foundation Model for Hyperspectral Remote Sensing | 2609.37340v1 | D | |
| ④ 高光谱基础模型/少样本 (D) | Hyperspectral Image Models: Technical Report | 2609.39871v1 | D | |
| ④ 高光谱基础模型/少样本 (D) | Resource-Aware Parameter-Efficient Model Adaptation for Onboard High-Dimensional Data | 2609.33687v1 | D | |

### ④ 高光谱基础模型 / 高效微调（D 组，分两半列）

**基础模型 / 预训练 / 表征学习**（2 篇）

- HyperSAM: A Promptable Foundation Model for Hyperspectral Remote Sensing
- Hyperspectral Image Models: Technical Report

**高效微调 / 适配**（D 子类，1 篇）

- Resource-Aware Parameter-Efficient Model Adaptation for Onboard High-Dimensional Data

**被过滤（前 9 条，附原因）**

- `未命中 A/B/C/D 任一关键词` — High-power photoconductive THz emitters for fast parallel electro-optic detection
- `未命中 A/B/C/D 任一关键词` — Prototype-Rule Neurosymbolic Regularization for Rank-Constrained Tensor Neural Networks under L
- `未出现 hyperspectral/HSI` — Strong Dimerization and Field-Induced Reconstruction of the Low-Energy Spectrum in $\mathrm{Cu}
- `未命中 A/B/C/D 任一关键词` — Phase-resolved wide-field CARS microscopy with speckle illumination
- `纯传感器/仪器类（spectral imaging），未命中 A/B/C/D` — Scanless quantum Fourier-transform mid-infrared spectroscopy for solids and surface analysis
- `未命中 A/B/C/D 任一关键词` — HyperDAM: Hyperspectral Distractor-Aware Memory with Amodal Expansion for SAM 3 Tracking
- `未命中 A/B/C/D 任一关键词` — Implicit Neural Representation for Hyperspectral Video Compression
- `纯传感器/仪器类（spectral imaging），未命中 A/B/C/D` — Band-Selection Stability and Semantic Segmentation Performance: A Study on Hyperspectral City
- `未命中 A/B/C/D 任一关键词` — Hyperspectral Trajectory Image for Multi-Month Trajectory Anomaly Detection

### 2.1 入选项逐条补充（命中证据来自标题还是摘要，已机器核对）

| arXiv | 标题 | 档 | 命中关键词（证据位置） |
|---|---|---|---|
| [2609.39926v1](https://arxiv.org/abs/2609.39926v1) | Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators | ②A | `hyperspectral super-resolution`、`spectral super-resolution`（**仅摘要**） |
| [2609.35410v1](https://arxiv.org/abs/2609.35410v1) | Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks | ②A | `spectral super-resolution`（标题） |
| [2601.21338v2](https://arxiv.org/abs/2601.21338v2) | Correcting Spectra Outside the Backbone: A Model-Agnostic Rectifier for Hyperspectral Image Super-Resolution | ②A | `hyperspectral image super-resolution` 等（标题） |
| [2603.25530v2](https://arxiv.org/abs/2603.25530v2) | Adaptive Subspace Modeling With Functional Tucker Decomposition | ③B | `cross-domain hyperspectral classification`、`hyperspectral classification`（**仅摘要**） |
| [2609.37340v1](https://arxiv.org/abs/2609.37340v1) | HyperSAM: A Promptable Foundation Model for Hyperspectral Remote Sensing | ④D | `hyperspectral foundation model`（标题）＋`promptable hyperspectral`（摘要） |
| [2609.39871v1](https://arxiv.org/abs/2609.39871v1) | Hyperspectral Image Models: Technical Report | ④D | `hyperspectral image models`（标题） |
| [2609.33687v1](https://arxiv.org/abs/2609.33687v1) | Resource-Aware Parameter-Efficient Model Adaptation for Onboard High-Dimensional Data | ④D(适配) | `hyperspectral adaptation`（**仅摘要**） |

**arXiv ID 复核：7/7** 在 `arxiv.org/abs/<id>` 解析成功且 `citation_title` 与候选标题归一化后完全一致（`verify-kept-2026-10-02c.json`）。

---

## 3. Top 3 精读

### 3.1 Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators（OmniHSR，2609.39926v1）

- **核心问题**（来源事实）：单一模型在**未见过的传感器/尺度**上做高光谱超分（HSR），现有任意尺度方法换传感器通常要额外数据与算力。
- **方法**：不预测光谱值，改为**预测波段共享的空间算子**。Cross-Spectral Mapping（CSM）把任意波段数的输入重采样到固定参考位置；Continuous Operator-Field Reconstruction（COFR）把局部高斯支撑算子合成连续算子场，作用于全部原始波段，得到任意尺度重建。
- **证据**：在 7 个数据集上算子预测都优于直接光谱值预测；**只用 ARAD 训练、0.538M 参数**，在 6 个未见数据集上超过所有直接迁移基线（无需目标域数据/微调）；×2 到 ×48 十二个尺度因子下，Pavia U 与 Chikusei 平均 PSNR 比最强基线高 **0.55 dB**；推理快至 **36×**。代码"will be publicly released soon"（**当前不可复现**）。
- **局限**：代码未放出；PSNR 增益 0.55 dB 属中等；"超越在目标传感器上从零训练/微调的基线"这一强主张没有给出各数据集方差。
- **可延伸**：把算子的"连续场"形式接到分类前端（见 §5 选题三）；或检验算子假设在跨传感器光谱响应差异极大（EMIT vs 航空）时是否退化。

### 3.2 Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks（SSRON，2609.35410v1）

- **核心问题**（来源事实）：用多光谱卫星影像做**光谱超分**，以低成本逼近高时空分辨率高光谱影像；该问题本身病态。
- **方法**：把光谱超分建成**算子学习**问题（函数→函数），SSRON 是 Deep Operator Network，学"降采样光谱 → 连续光谱"的映射；训练目标是从 Sentinel-2A 类多光谱影像超分到 **EMIT** 影像。
- **证据**：所有指标优于基线；具备**零样本光谱超分**能力（可预测训练中未见波段）；连续输出形式暗示可在比传感器原生更细的波段间隔上估计光谱。
- **局限**：摘要级证据，**未见代码/数据链接**；"更细波段间隔"只是"potential/suggests"，非实验结论；“连续光谱”的真值监督如何构造未说明。
- **可延伸**：与 OmniHSR 的算子场做同一评测台（都属算子/连续形式），比较"空间算子"与"光谱算子"哪一路在跨传感器上更稳；EMIT 作为真值可复用。

### 3.3 Hyperspectral Image Models: Technical Report（2609.39871v1）

- **核心问题**（来源事实）：高光谱深度学习进展被**碎片化仓库、不兼容的张量约定、非标准化评测**拖住。
- **方法**：模块化框架统一 **6 个范式、55 个代表模型**（谱-空 CNN、ViT、Mamba、GNN、KAN、自监督掩码自编码），公共 registry＋自动 4D/5D 张量适配＋标准构造器；集成 **Airborne / Spaceborne / UAV / Mars CRISM 共 24 个基准场景**，含缓存、标签重映射、PCA、显式波段选择或原始光谱、可选空间池化、任意 P×P 取块。
- **证据**：为防重叠窗口虚高，提供类均衡随机划分与**空间不重叠区域划分 + Chebyshev 保护带**，消除训练/测试像素重叠；1,320 次 model×scene 评测、6,600 次带种子的运行。结论：**场景难度主导架构**（Botswana 平均 96.40% ↔ Houston 2018 56.70%，差距 39.7 个点），而**范式均值之间只差约 15 个点**；**无普遍最强范式**，≤1M 参数的小模型可媲美大两个数量级的架构。**代码公开**：https://github.com/Tanishq251/Hyperspectral-Image-Models
- **局限**：技术报告（非经同行评审）；只覆盖**分类**任务，不含超分/检测；结论基于其自带划分，未与各原论文的官方划分交叉验证。
- **可延伸**：把**"Chebyshev 保护带 + 空间不重叠划分"协议搬到 HSI 超分评测**——超分论文的增益有多少来自重叠窗口/同源退化，目前无人系统检验（见 §5 选题二）。

---

## 4. CV 到 RS 的迁移注记

本期入选均为遥感原生工作，无纯 CV 论文入选。但两条方法学迁移成立：

- **算子学习（DeepONet / 神经算子）→ 高光谱**：来源是科学计算与 PDE 求解的算子学习范式。可迁移组件是"学函数到函数的映射 + 连续输出"。所需改动：把物理域（时空）换成光谱/空间轴，处理 4D/5D 高光谱张量而非 2D 场。遥感数据集：EMIT、EnMAP、ARAD、Pavia U、Chikusei。风险：连续输出的真值需从多源传感器配准后产生，配准误差会直接变成标签噪声。
- **提示式分割基础模型（SAM 系列）→ 高光谱**：可迁移组件是"冻结 RGB 分支＋可训练光谱侧编码器＋零初始化特征注入（ControlNet 式）"。所需改动：把 RGB 先验经丰度迁移生成器合成高光谱立方体来对齐通道；风险是合成分数据的域隙——HyperSAM 自己给出的答案是"高质量合成数据可能比单纯堆噪声监督更有效"，但这仍是该路线最大的未解风险。

---

## 5. 三个可做的选题

### 选题一：算子场超分的跨传感器鲁棒性边界

- **Problem**：算子/连续形式（OmniHSR、SSRON）宣称跨传感器零样本，但都没报告**传感器光谱响应间隔变大时的失效点**（如 ARAD→EMIT 的波长覆盖差异）。
- **Hypothesis**：算子预测的跨传感器优势随"波段数差 + 光谱响应重叠率"下降而退化，存在可测量的临界重叠率。
- **Method sketch**：固定 OmniHSR 与 SSRON 两类算子模型，构造按光谱响应重叠率分层的数据切分（高/中/低重叠），比较"算子预测"vs"直接光谱值预测"两条路径的 PSNR/SSIM/SAM。
- **数据与指标**：训练 ARAD；测试 Pavia U、Chikusei、Houston、EMIT 配准子集；指标 PSNR / SSIM / SAM（光谱角）+ 跨传感器 ΔPSNR。
- **Baselines**：OmniHSR、SSRON（若代码放出）；直接光谱值预测的同架构版本；在目标传感器微调的 LoRA 版本。
- **最小可证伪实验**：只用 ARAD 训练、在**一个**未见传感器上按三个重叠率档位评测，若 ΔPSNR 不随重叠率单调变化，假设即被推翻。
- **Risk**：OmniHSR 代码"soon"未放出 → 可能需自行复现；EMIT 与 ARAD 的空间配准质量决定标签可信度。

### 选题二：HSI 超分评测的泄漏审计

- **Problem**：高光谱分类已被证明存在重叠窗口导致虚高（Hyperspectral Image Models 用 Chebyshev 保护带专门解决），但**超分评测从未做同样审计**：训练块与测试块在空间上重叠、或退化算子同源，都会虚高 PSNR。
- **Hypothesis**：近三年主流 HSI 超分论文的增益中有可观比例来自空间重叠与同源退化，改用保护带划分后排序会变化。
- **Method sketch**：复现 3–5 篇代表性 HSI-SR 方法，在"原划分"与"空间不重叠划分 + Chebyshev 保护带"两套协议下各评一次，报告排名变化与 ΔPSNR。
- **数据与指标**：Pavia U、Chikusei、Houston、Botswana（与 3.3 的场景集对齐）；指标 ΔPSNR / ΔSSIM、Kendall τ（两次排名一致性）。
- **Baselines**：被复现论文的原始报告数字；同一模型在两套划分下的自身对照。
- **最小可证伪实验**：只挑**一篇**有公开代码的 HSI-SR 论文，在两套划分下重跑，若 ΔPSNR ≈ 0 且排名不变，假设被推翻。
- **Risk**：复现成本高、部分论文无代码；"泄漏"与"真实泛化"难以完全解耦。

### 选题三：任务驱动超分——把算子场作为分类的可微前端（C 组空白区）

- **Problem**：本期 ① C 组 **0 篇**：高光谱超分与分类几乎各自为政，超分论文用 PSNR/SAM 证明"更像真值"，却没人证明**超分是否真的提升分类**。
- **Hypothesis**：以分类损失端到端驱动超分前端，能在低分辨率输入下比"先超分再分类"的两阶段流水线获得更高的分类精度，且在高倍率下优势更大。
- **Method sketch**：以 OmniHSR 式算子场（或 SR²-Net 式骨干无关整流器）作可微前端，后端接标准谱-空分类器，联合优化 L = L_cls + λ·L_rec；对比 λ=0 与两阶段基线。
- **数据与指标**：分类数据集（Indian Pines、Pavia U、Salinas、Houston 2013）；指标 OA / AA / Kappa，附加 SAM 与推理成本。
- **Baselines**： bicubic 降采样直接分类；两阶段（先超分后分类）；只做分类不做超分；λ 扫描下的联合训练。
- **最小可证伪实验**：在 **1 个**数据集、**1 个**分类器上跑两阶段 vs 联合训练，若 OA 提升 <1 个点或不显著，假设被推翻。
- **Risk**：超分前端可能只是充当隐式正则化器，"提升"来自参数量而非超分本身——需参数量对齐的对照臂；分类标签本身就是低分辨率采集，超分真值不可得。

---

## 6. 会议论文（Conference）

（`conf_match.py` 原始输出）

## 会议论文（Conference）

**arXiv × 会议索引匹配**：16 个候选，命中 0 篇同时有会议版本。

（本期无候选命中会议版本。）

**会议新进榜（Conference spotlight）**：本次首次纳入 0 篇。

_dry-run：未更新 seen-state_

### 6.1 为什么这里是 0 篇（已逐篇查实，不是匹配器漏配）

CVPR2026 索引共 **4,042 条**，按现行策略命中高光谱的**只有 3 篇，全部 p2 高光谱超分**：

| 标题 | 会议页 | arXiv 预印本 |
|---|---|---|
| EMR-Diff: Edge-aware Multimodal Residual Diffusion Model for Hyperspectral Image Super-resolution | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_EMR-Diff_Edge-aware_Multimodal_Residual_Diffusion_Model_for_Hyperspectral_Image_Super-resolution_CVPR_2026_paper.html) | **未找到**（4 种写法查询均 0 条） |
| Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_Enhancing_Unregistered_Hyperspectral_Image_Super-Resolution_via_Unmixing-based_Abundance_Fusion_Learning_CVPR_2026_paper.html) | [2603.07918v1](https://arxiv.org/abs/2603.07918v1)（2026-03-09） |
| Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Young_Spectral_Super-Resolution_via_Adversarial_Unfolding_and_Data-Driven_Spectrum_Regularization_From_CVPR_2026_paper.html) | [2603.00920v1](https://arxiv.org/abs/2603.00920v1)（2026-03-01） |

- 两篇有预印本的 CVPR 论文，预印本日期为 **2026-03**，落在 7 天窗口之外 → 与本轮 16 篇候选自然无交集（**不是漏匹配**）。
- EMR-Diff 用 `all:"EMR-Diff"`、`ti:"Residual Diffusion Model for Hyperspectral"`、`all:"Edge-aware Multimodal Residual Diffusion"`、`all:"EMR Diff" AND all:"hyperspectral"` **四种写法各查一次，均 0 条** → arXiv 上确无预印本。
- spotlight 显示 0 篇新进，是因为**同日更早的运行已把 3 篇写入 `CVPR2026_seen.json`**（`updated_at: 2026-10-02T10:49:06`）。这是该机制"同一批会议论文只报一次"的正常行为，不是本次漏报；本次以 `--dry-run` 执行，未改动 seen-state。

---

## 7. 检索覆盖与窗口证据（arXiv）

| 项 | 值 |
|---|---|
| 查询数 | 20（A 组 7 / B 组 4 / C 组 2 / D 组 3 / 无界 4） |
| HTTP 200 | **20/20**，无 429 / 503 / 解析错误 |
| 全查询去重 | 564 篇 |
| 落窗候选 | **16 篇**（新投稿 13 / 仅更新 3） |
| 窗口内最新 published | **2026-09-30** |
| 无界查询召回跨度 | `all:"hyperspectral"`（300 条）覆盖 **2026-01-18 → 2026-09-30** |

- **有效窗口声明**：请求窗口为 09-25→10-02，实际能落窗的最新发表日期是 **09-30**，差 2 天属 arXiv 公告滞后，**不是漏检**；无界查询回看到 2026-01 说明最新切片 `sortBy=submittedDate` 未被截断，召回完整。
- **跨列表更新单列**：`2601.21338v2`（01-29 投、09-28 更新）、`2603.25530v2`（03-26 投、09-25 更新）为 **updated-only**，按 skill 要求单独标注，未与本期新投稿混算。
- **SAR / 雷达排除**：本期窗口内命中 SAR/雷达词表的论文 **0 篇**。
- 本期**只用了 arXiv + CVF**，未使用 Semantic Scholar / Papers with Code / Hugging Face，故对其榜单不作任何断言。

---

## 8. 验收结论（策略准不准 · 逐条归因）

### 8.1 数字对比

| 运行 | 候选 | 入选 | ① C | ② A | ③ B | ④ D |
|---|---|---|---|---|---|---|
| 同日运行 B（10:48） | 16 | 2 | 0 | 2 | 0 | 0 |
| **本次运行 C** | **16** | **7** | **0** | **3** | **1** | **3** |

增量 5 篇**全部可归因到具体策略改动**，无一篇来源不明：

| 新增入选 | 触发改动 |
|---|---|
| `2609.39926` Super-Resolving Unseen Hyperspectral Sensors… | A/B/C/D 匹配范围由"标题"放宽为**标题＋摘要**（其 A 组命中仅出现在摘要 `hyperspectral super-resolution`）——上一轮已列为"唯一可证漏检 1 篇"，本轮修复后正常入选 |
| `2609.37340` HyperSAM | D 组关键词生效（`hyperspectral foundation model` / `promptable hyperspectral`）——上一轮标注"显然属 ③ 档但 B 组只列 classification，永远进不来" |
| `2609.39871` Hyperspectral Image Models | D 组 `hyperspectral image models` |
| `2603.25530` Adaptive Subspace Modeling… | B 组短语级匹配（`cross-domain hyperspectral classification`，标题无命中、摘要命中） |
| `2609.33687` Resource-Aware PEFT…（NE-LoRA） | 新增 `[D_ADAPT]` 子组（`hyperspectral adaptation`）——上一轮明确点名"是否加需你决定"，已加 |

**尚未解决、需要你定夺的**（本轮如实列出，未擅自扩词）：

- `2609.34396` HyperDAM（SAM 3 跟踪）、`2609.31435` INR 高光谱视频压缩、`2609.31074` 波段选择与语义分割——都是高光谱且方法上属于"基础模型 / 表征"一脉，但现行 D 组 7 个词形与 A/B/C 均不覆盖，仍被 `未命中 A/B/C/D 任一关键词` 拦下。若要收，需要新增**任务词形**（tracking / compression / semantic segmentation / band selection），而不是继续放宽现有短语。
- `2609.34396` 与 `2609.31435` 若加入榜单会稀释"超分/分类"主轴；建议只在你决定扩展雷达口径时再加。

### 8.2 本轮发现并已修复的两个脚本缺陷（改动均在 `radar_filter.py`，未动关键词策略）

1. **`命中组` 列口径与准入口径不一致**：准入用"标题＋摘要"，而该列只拿**标题**去 `abc_hit()`，导致靠摘要入选的论文（`2609.39926`、`2603.25530`）显示为 `-`，等于在报告里凭空抹掉了入选理由。已改为传 `标题＋摘要`。**修复前**：2 篇显示 `-`；**修复后**：7 篇全部正确显示 A/B/D。
2. **规则说明文字过时**：输出里的"过滤规则"仍写"命中 `hyperspectral / HSI` 与 **A/B/C** 关键词之一"，而策略已是 A/B/C/D，且未提 SAR 无条件剔除。已更正。

两处修复后 `--selftest` 仍 **13/13 passed**，筛选计数 **16 → 7 不变**（即修复只影响展示，不改变任何准入/排序判定）。

### 8.3 运行完整性告警（需要你知道）

本轮运行期间，**另一个会话（`20261001_195920_6ed716ea`）正在同时修改同一批判策略文件**：11:03 时段 `search_keywords.txt` 被加入 4 个 C 组新词、新增 `[D_ADAPT]` 子组，`radar_keywords.py` 相应增加 `SUBGROUP_OF` / `d_kind`。我通过**筛选前后两次 sha256 比对**把本轮固定在同一版本上（§0 表格），结果一致；但**下一次运行会拿到又一份不同的策略**。建议：策略变更与验收运行不要并行，否则"候选 N → 入选 M"不可比。

---

## 9. 排除说明（被过滤候选及原因）

**16 篇候选的完整分解**：入选 7 ｜ 未命中 A/B/C/D 5 ｜ 疑似光谱仪器/传感器 2 ｜ 未出现 hyperspectral/HSI 1 ｜ SAR/雷达 0。

**典型过滤例子（3 条）**：

1. `2610.00744` **High-power photoconductive THz emitters for fast parallel electro-optic detection** — 判为 `未命中 A/B/C/D 任一关键词`。宽泛的 `all:"hyperspectral"` 在物理/材料分类上的典型污染：太赫兹器件，与遥感无关。
2. `2609.39730` **Phase-resolved wide-field CARS microscopy with speckle illumination** — 相干拉曼显微，"spectrum/spectral"系词在光学测量领域的高频同形词，非遥感。
3. `2609.37281` **Scanless quantum Fourier-transform mid-infrared spectroscopy for solids and surface analysis** — 判为 `纯传感器/仪器类（spectral imaging），未命中 A/B/C/D`，即"仪器/传感器设计"略过档，符合策略。

**略过档（不占榜单名额）**：纯 pansharpening 0 篇 ｜ 纯 multispectral 0 篇 ｜ 纯光谱仪器/传感器设计 2 篇 ｜ 纯 SAR 0 篇。

**待你定夺的口径问题**：`2609.34396` HyperDAM、`2609.31435` INR 高光谱视频压缩、`2609.31074` 波段选择×语义分割、`2609.33687` 之外仍有若干"高光谱＋基础模型"工作落在 D 组词形之外——是否扩 D 组任务词形，是口径决策而非 bug（见 §8.1）。

---

*本期数据来源：arXiv API（20/20 查询成功）、CVF openaccess CVPR2026 本地索引（4,042 条 / 命中高光谱 3 条）。所有 arXiv ID 均经 `arxiv.org/abs/<id>` 复核标题与日期。区分「来源事实」与「推断」：正文中带"（来源事实）"标记的为摘要/页面原文所述，其余为基于该证据的推断；未获得的信息一律写"未说明/未找到"，不作补全。*
