# 高光谱研究雷达日报 · 2026-10-04（第 3 期）

## 来源与窗口

- **arXiv**（365 天窗口，`sortBy=relevance`，每查询 `max_results=300`）：**今日新扫 11 条查询全部被限流**——返回 14/126 字节的 `Rate exceeded.`（HTTP 429），另有多条 60 s 零字节挂起；冷却 150 s 后用 22 s 间隔重试 3 条，仍 **0/3 成功**。按既定预案**放弃今日新扫、改用昨日 365 天缓存池**，故今日新扫**新增 0 篇**。
- 候选池 = **2026-10-03 缓存的 365 天池（202 篇）** ∪ 今日新扫（0 篇），去重后仍 **202 篇**。池内最新 `published` 仍是 **2026-09-30**，与昨日一致——这是 arXiv 公告批次延迟（窗口上界 2026-10-04，实际公告只到 09-30），**不是漏筛**。真实有效窗口：**2025-10-03 → 2026-09-30**。
- **CVF**：CVPR2026 本地索引 **4,042** 条（缓存命中，未重下），本期只做离线匹配。
- 策略冻结与运行健康：`selftest 18/18 passed`；`radar_filter.py 66877f5979fe` / `radar_keywords.py d405ccb11486` / `search_keywords.txt 4382dbe26daf` —— **与上一期完全一致，运行期间未修改任何策略文件**（三个哈希与上一期报告相同，计数可与上一期直接比较）。

## 本期要点

1. **排序修复后的第二个完整期：本期 10 篇并列相关度 84，改动的是「平局怎么破」。** 相关度评分是粗粒度的，纯分类/纯超分、标题级命中的上限就是 84。本期过筛池未推送的 103 篇里，**32 篇并列 84**，两键排序 `(-relevance, -updated)` 取其中**更新时间最新 10 篇**；第 11 位仍是 84（更新 2026-04-28），说明截断发生在相关度平局内部，而非跨档降级——这是设计预期，不是漏筛。
2. **C 组（超分+分类交叉项）本期 0 篇** —— 365 天窗口下 123 篇过筛里再次无一命中交叉词形，是真实空缺。
3. **A/B 仍是主战场**：123 篇过筛中 A 组 42 篇、B 组 59 篇、D 组 18 篇（D 内部：基础模型/预训练 15、仅适配 2、两者兼有 1）；本期新推 10 篇里 **A 组 2 篇、B 组 8 篇、D 组 0 篇**。
4. **可复现性回暖**：本期 10 篇中 A 档（代码+数据）**0** 篇、B 档（仅代码）**4** 篇 —— 4 个仓库全部 HTTP 验活 200；B 档 4 篇里有 3 篇是分类侧、1 篇是超分侧（SDANet），后者是本轮最值得先跑的超分实现。
5. **效率导向的分类开始成组出现**：本期 8 篇分类里，BCG-Former（Pareto 效率）、MixerSENet（53k 参数）、DSCC（197 FPS）、SpectralTrain（2–7× 训练提速）都在打「精度–成本」权衡，而非单纯刷 OA —— 这是本方向近期一个可见的移动。

## 筛选结果

## 高光谱筛选结果（365 天窗口 + 去重）

- 拉取候选 **202** 篇 → 通过关键词策略 **123** 篇 → 已推过（去重剔除）**20** 篇 → **本期新推 10 篇**（另有 93 篇通过但未进前十，留待后续）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C/D 关键词之一；pansharpening、multispectral 单独出现不算；SAR/雷达类无条件剔除
- 排序：与「超分+分类」方向的相关度（主）+ 更新时间（仅用于打破相近分数的平局），**不按投稿时间**

- 可复现性：**A（代码+数据）0 篇** / B（仅代码）4 篇 / C（未声明）6 篇　— 由摘要 + arXiv comment 判定，C 表示「未声明」而非核实不存在

| # | 标题 | arXiv | 相关度 | 更新时间 | 可复现性 |
|---|---|---|---|---|---|
| 1 | Fermat Active Laplace Learning for Semi-Supervised Hyperspectral Image Classification | 2608.02483v1 | 84 | 2026-08-03 | C |
| 2 | USP-Mamba: Unmixing-Derived Spectral and Structural Prompting for Hyperspectral Image Super-Resolution | 2608.02401v1 | 84 | 2026-08-03 | C |
| 3 | HyperImageNet: A Large-Scale High-Spatial Resolution Hyperspectral Imagery Classification Benchmark | 2607.21050v2 | 84 | 2026-07-27 | C |
| 4 | BCG-Former: Toward Pareto-Efficient Hyperspectral Image Classification via Band-Contextual Gating | 2607.15639v1 | 84 | 2026-07-17 | C |
| 5 | DAPGNet: Dynamic Adaptive Physics-Guided Graph Diffusion Network for Hyperspectral Image Classification | 2607.15128v1 | 84 | 2026-07-16 | C |
| 6 | MixerSENet: A Lightweight Framework for Efficient Hyperspectral Image Classification | 2606.01700v1 | 84 | 2026-06-01 | B |
| 7 | SpectralTrain: A Universal Framework for Hyperspectral Image Classification | 2511.16084v3 | 84 | 2026-05-29 | B |
| 8 | SoDa2: Single-Stage Open-Set Domain Adaptation via Decoupled Alignment for Cross-Scene Hyperspectral Image Classification | 2605.03371v1 | 84 | 2026-05-05 | C |
| 9 | Hyperspectral Image Classification via Efficient Global Spectral Supertoken Clustering | 2604.27364v1 | 84 | 2026-04-30 | B |
| 10 | Spectral Dynamic Attention Network for Hyperspectral Image Super-Resolution | 2604.27326v1 | 84 | 2026-04-30 | B |

**可复现性判定依据**

- 1. `C` — 摘要与 comment 均未声明代码/数据
- 2. `C` — 摘要与 comment 均未声明代码/数据
- 3. `C` — 摘要与 comment 均未声明代码/数据
- 4. `C` — 摘要与 comment 均未声明代码/数据
- 5. `C` — 摘要与 comment 均未声明代码/数据
- 6. `B` — code: github.com/mqalkhatib/MixerSENet
- 7. `B` — code: github.com/mh-zhou/SpectralTrain
- 8. `C` — 摘要与 comment 均未声明代码/数据
- 9. `B` — code: github.com/laprf/DSCC
- 10. `B` — code: github.com/oucailab/SDANet

**被过滤（前 12 条，附原因）**

- `未命中 A/B/C/D 任一关键词` — A UAV-Based VNIR Hyperspectral Benchmark Dataset for Landmine and UXO Detection
- `纯传感器/仪器类（spectral imaging），未命中 A/B/C/D` — SpectralCA: Bi-Directional Cross-Attention for Next-Generation UAV Hyperspectral Vision
- `未命中 A/B/C/D 任一关键词` — Raman Microspectroscopy for Real-Time Structure Indicator in Ultrafast Laser Writing
- `未出现 hyperspectral/HSI` — AION-1: Omnimodal Foundation Model for Astronomical Sciences
- `未命中 A/B/C/D 任一关键词` — Decoupled Complementary Spectral-Spatial Learning for Background Representation Enhancement in 
- `未命中 A/B/C/D 任一关键词` — SWAN: Self-supervised Wavelet Neural Network for Hyperspectral Image Unmixing
- `未命中 A/B/C/D 任一关键词` — DeepSalt: Bridging Laboratory and Satellite Spectra through Domain Adaptation and Knowledge Dis
- `未命中 A/B/C/D 任一关键词` — A Provably-Correct and Robust Convex Model for Smooth Separable NMF
- `未出现 hyperspectral/HSI` — Burst Image Quality Assessment: A New Benchmark and Unified Framework for Multiple Downstream T
- `纯传感器/仪器类（spectral imaging），未命中 A/B/C/D` — HAMscope: a snapshot Hyperspectral Autofluorescence Miniscope for real-time molecular imaging
- `雷达/微波类：synthetic aperture radar` — UniDiff: Parameter-Efficient Adaptation of Diffusion Models for Land Cover Classification with 
- `纯传感器/仪器类（spectral imaging），未命中 A/B/C/D` — Visible to Longwave-infrared imaging via an inverse-designed monolithic lens
- …另有 67 条

## 分组（本期 10 篇）

- **① 超分+下游任务联合优化（C 组）：0 篇** —— **本期无交叉项**。
- **② 纯高光谱超分（A 组）：2 篇** —— USP-Mamba `2608.02401v1`、SDANet `2604.27326v1`。
- **③ 纯高光谱分类（B 组）：8 篇** —— Fermat Active Laplace `2608.02483v1`、HyperImageNet `2607.21050v2`、BCG-Former `2607.15639v1`、DAPGNet `2607.15128v1`、MixerSENet `2606.01700v1`、SpectralTrain `2511.16084v3`、SoDa2 `2605.03371v1`、DSCC Supertoken `2604.27364v1`。
- **④ 高光谱基础模型 / 高效微调（D 组，分两半）：0 篇**
  - **基础模型 / 预训练 / 表征学习：0 篇**
  - **高效微调 / 适配：0 篇**
- **⑤ benchmark / 数据集：** HyperImageNet 是 benchmark，但它同时命中 B 组，故按优先组归入 ③（不重复计）。
- **⑥ 其他高光谱：0 篇。**

## Top 3 精读（摘要级，未抓 PDF）

### 1. USP-Mamba: Unmixing-Derived Spectral and Structural Prompting for Hyperspectral Image Super-Resolution
`2608.02401v1` · rel **84** · 更新 2026-08-03 · 可复现性 **C**（未声明）

- **问题**：Mamba 类 HSI 超分模型受两点制约 ——（a）因果序列建模必须把二维高光谱特征沿固定扫描顺序展开，破坏空间邻接、限制上下文传播；（b）状态空间参数主要来自通用可学表示，**没有显式对齐高光谱自身的物理特性**。
- **方法**：USP-Mamba —— 用**解混派生的提示**驱动 Mamba 状态演化。① *解混信息谱提示*：捕捉输入图像的整体物质组成，在重建全程提供持续条件，并逐层自适应；② *特征级结构提示*：空间分量（增强局部细节的结构敏感状态编码）+ 频率分量（在同质区/高频细节间做区域自适应切换）；③ 互补的 **Hilbert 扫描**与**语义引导邻域扫描**，兼顾空间连续性与非局部语义依赖。
- **证据**：多个数据集上「一致优于代表性方法」（摘要未给出具体 PSNR 数值）。
- **局限**：**摘要无量化数字**（无法核验增益幅度）；无跨传感器/跨区域验证；未声明代码；无推理成本报告。
- **可延伸**：把「解混提示」当成 **SR 与分类共享的物理瓶颈**——解混（端元/丰度）本就是分类侧的经典先验，但目前几乎无人把它同时接到 SR 与下游分类上（见选题 1，正好补 C 组空缺）。

### 2. HyperImageNet: A Large-Scale High-Spatial Resolution Hyperspectral Imagery Classification Benchmark
`2607.21050v2` · rel **84** · 更新 2026-07-27 · 可复现性 **C**（未声明）

- **问题**：现有高光谱分类基准要么类别少、要么缺像素级/实例级标注，难以评测**细粒度**地物理解与**开放环境**（严格空间分离）泛化。
- **方法/数据**：**26,084** 个机载高光谱图块、**224 波段**、**138 个细粒度地物类别**；同时提供**原始影像 + 像素级语义标签 + 物体级实例掩码**（支持语义分割与实例分割）；建立**严格空间分离**的开放环境基准，评测代表性方法与 **HyperFree** 基础模型。
- **证据**：摘要称实验验证了 HyperImageNet 对细粒度高光谱理解与开放环境遥感研究的有效性（未列具体数值）。
- **局限**：仅机载（缺星载）；138 类必然**长尾**，但摘要未给类分布/长尾指标；代码与数据**未声明**（作为 benchmark，数据可得性是关键，需进一步确认）。
- **可延伸**：138 类 + 长尾 + 严格空间分离，正好是检验「光谱基础模型能否顶住细粒度长尾」的现成标尺（见选题 2）。

### 3. SpectralTrain: A Universal Framework for Hyperspectral Image Classification
`2511.16084v3` · rel **84** · 更新 2026-05-29 · 可复现性 **B**（仅代码）

- **问题**：HSI 分类训练数据大、算力昂贵，限制深度学习在真实遥感任务上的落地。
- **方法**：SpectralTrain —— **架构无关**的通用训练框架，把**课程学习**（逐步引入光谱复杂度）与**基于 PCA 的光谱降采样**结合；与具体架构/优化器/损失函数解耦，兼容经典与 SOTA 模型。
- **证据**：三个基准数据集（Indian Pines、Salinas-A、新提出的 **CloudPatch-7**）上跨空间尺度/光谱特性/应用域一致有效，**训练提速 2–7×**，精度仅小幅到中等下降（视主干而定）；并把它用到云分类，指向气候遥感。
- **局限**：是**训练策略**类贡献而非新架构，收益取决于主干；精度有代价（摘要未量化每主干的具体降幅）；CloudPatch-7 为新数据集，可比性有限。
- **可延伸**：把「PCA 光谱降采样 + 课程学习」这一**训练侧提速**直接搬到 **HSI 超分**的训练上（超分训练通常更贵），验证能否在 PSNR 基本持平下大幅缩短训练——这是本方向少见的、低门槛且立刻可跑的切入（见选题 3 的备选路线）。

## 3 个可做选题

### 选题 1：解混提示驱动的「超分↔分类」联合框架（直补 C 组空缺）
- **Problem**：C 组（超分与分类联合优化）在 365 天窗口内**连续两期 0 篇**；而本期 `2608.02401` 已证明**解混先验能有效引导超分**，`2604.27364`/`2608.02483` 又分别给出 token 级/半监督的分类侧工具，却无人把解混当作**SR 与分类共享的物理瓶颈**。
- **Hypothesis**：以端元/丰度为共享中间表示、联合优化 SR 与分类，在低标注预算下的分类增益**显著大于**「先 SR 再分类」的解耦流程。
- **Method sketch**：SR 主干用 `2608.02401` 的 USP-Mamba 解混谱提示（提供共享丰度场）→ 分类头接 `2604.27364` 的 token 级预测（丰度超像素）；对照「解耦两阶段」与「联合训练」，加消融「提示是否共享」。
- **数据与指标**：Pavia University、Chikusei、WHU-Hi-LongKou；SR 报 PSNR/SSIM/SAM，分类报 OA/AA/Kappa，重点报「SR 误差 → 分类增益」的传导曲线与 1%/5% 标注预算下的差异。
- **Baselines**：USP-Mamba（纯 SR）、SDANet、DSCC（纯分类）、解耦 SR→分类、无 SR 直接分类。
- **最小可证伪实验**：单数据集、1% 标注下比较「共享解混瓶颈的联合训练」vs「解耦」，若 OA 差在 3 个随机种子下均 <0.3%，假设不成立。
- **Risk**：C 组稀疏可能说明该方向本身收益有限（本期最需警惕的反证）；联合训练调参成本高；解混质量差时会同时拖累两侧。

### 选题 2：138 类细粒度长尾高光谱分类（HyperImageNet 起步）
- **Problem**：新基准 `2607.21050` 提供 138 类、严格空间分离的细粒度分类，但摘要未给长尾指标，现有分类器（本期多为 ~10 类标准集上的方法）在长尾细粒度上的退化程度未知。
- **Hypothesis**：现有 SOTA 分类器在 HyperImageNet 上的**宏平均（macro-F1/per-class recall）会显著低于总体精度**，且光谱基础模型（HyperFree）相对传统 CNN/Transformer 的领先在长尾类上更明显。
- **Method sketch**：在 HyperImageNet 上做「解耦表征 + 原型/长尾重加权」的基线改造（可用 `2604.27364` 的 soft-label 超像素方案处理混合类），对比 3D-CNN / Mamba / 基础模型微调。
- **数据与指标**：HyperImageNet（主）、Pavia/WHU-Hi（迁移）；OA/AA/Kappa + macro-F1 + 每类召回 + 类频分层报告。
- **Baselines**：HyperFree、BCG-Former `2607.15639`、MixerSENet `2606.01700`、DSCC `2604.27364`。
- **最小可证伪实验**：只测 3 个分类器在 HyperImageNet 上的 OA 与 macro-F1 差值；若差值 <2 个百分点，长尾假设弱化。
- **Risk**：基准数据/代码未声明，可能需向作者索要；138 类标注噪声未知；若数据不可得则该方向直接受阻（需先确认可得性）。

### 选题 3：把「效率-精度 Pareto」从分类搬到高光谱超分
- **Problem**：本期分类侧已形成 Pareto 视角（BCG-Former 亚毫秒、MixerSENet 53k 参数、DSCC 197 FPS），但**超分侧几乎无**「少参数 + 低延迟」的工作（本期 2 篇 SR 均未报告推理成本）。
- **Hypothesis**：把 band-contextual gating（`2607.15639` 的 BCG）与线性注意力搬到 SR 主干，能在 PSNR 基本持平的前提下把参数量/延迟压到当前 SR 方法的 1/5 以下。
- **Method sketch**：以 SDANet `2604.27326`（动态通道稀疏注意力）为起点，替换其通道注意力为 BCG 式的局部带间门控；加单遍 Band-RoPE + 线性注意力做高效联合表示；消融换掉各组件。
- **数据与指标**：Pavia University、Chikusei（HSI-MSI 融合设定）；PSNR/SSIM/SAM/ERGAS + 参数量 + 单图推理延迟。
- **Baselines**：SDANet、USP-Mamba、经典 CNN-SR。
- **最小可证伪实验**：单数据集替换注意力模块，看延迟是否下降 ≥3× 且 PSNR 下降 <0.2 dB；否则假设不成立。
- **Risk**：SR 的精度对注意力替换可能敏感，效率收益或被重构损失掩盖；Pareto 基准本身容易被质疑为工程调优，需严格控制变量并公开延迟测量协议。

## 会议论文（CVPR2026，本地索引离线匹配）

- 本期入选 10 篇中，**0 篇**同时有 CVPR2026 版本（本期多为 2026 年 4–8 月新投的分类/超分 preprint，尚无会议版）。
- 放回全池口径：**202 个候选命中 5 篇**同时有会议版本（与上一期相同，池未变）——分别是视频级压缩光谱重建、多光谱→NASA 高光谱的光谱超分、抗光谱漂移的双门控 MoE、无配准 HSI 超分（UAFL，上期已推）、以及一篇超表面相机（仪器类）。
- **会议新进榜（spotlight）：0 篇。** CVPR2026 的 seen-state 已于 2026-10-02 被消费，这是该模块的一次性设计，不是匹配失效。

## 排除说明

- 默认排除 SAR/雷达类：`UniDiff`（PEFT + 地物分类）因摘要含 synthetic aperture radar 被**无条件剔除**。
- 仪器/传感器类：`SpectralCA`、`HAMscope`（快照自体荧光显微）、`Visible to Longwave-infrared imaging via an inverse-designed monolithic lens` 等，唯一话题证据是 `spectral imaging`，判为仪器排除。
- 门禁/话题未命中：`A UAV-Based VNIR Hyperspectral Benchmark Dataset for Landmine and UXO Detection`（有高光谱但未命中 A/B/C/D）、`SWAN`（自监督小波解混）、`DeepSalt`、`A Provably-Correct and Robust Convex Model for Smooth Separable NMF` 等未命中 A/B/C/D 词形。
- 门禁未满足：`AION-1`（天文全模态基础模型）、`Burst Image Quality Assessment` 未出现 hyperspectral/HSI。
- 上述规则由 `search_keywords.txt` 单一真相源执行，本期未改动任何策略文件。

### 本期可复现（A/B 档，便于先跑）

- A（代码+数据）**0** 篇 ／ B（仅代码）**4** 篇 ／ C（未声明）6 篇

| 标题 | arXiv | 档 | 依据 |
|---|---|---|---|
| MixerSENet: A Lightweight Framework for Efficient Hyperspectral Image Classification | 2606.01700v1 | B | code: github.com/mqalkhatib/MixerSENet |
| SpectralTrain: A Universal Framework for Hyperspectral Image Classification | 2511.16084v3 | B | code: github.com/mh-zhou/SpectralTrain |
| Hyperspectral Image Classification via Efficient Global Spectral Supertoken Clustering | 2604.27364v1 | B | code: github.com/laprf/DSCC |
| Spectral Dynamic Attention Network for Hyperspectral Image Super-Resolution | 2604.27326v1 | B | code: github.com/oucailab/SDANet |

### 可跑的 baseline（本期论文提到的开源实现，已验活）

| 仓库 | 出处（arXiv ID） | HTTP |
|---|---|---|
| https://github.com/laprf/DSCC | 2604.27364v1 | ✅ 200 |
| https://github.com/mh-zhou/SpectralTrain | 2511.16084v3 | ✅ 200 |
| https://github.com/mqalkhatib/MixerSENet | 2606.01700v1 | ✅ 200 |
| https://github.com/oucailab/SDANet | 2604.27326v1 | ✅ 200 |

共 4 个仓库：**4 个可访问**
