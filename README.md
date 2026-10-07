# 高光谱研究雷达日报 · 2026-10-07（第 6 期）

- **数据来源**：本地缓存池 `candidates-2026-10-07.json`（**零 arXiv 请求**；本任务未发起任何 arXiv/学术站点抓取）
- **窗口**：365 天，365d 2025-10-07..2026-10-07；池内 203 篇（`sort=relevance`）
- **池的新鲜度**：池由独立的池刷新任务当天生成（文件 mtime 2026-10-07 08:00:43，本任务未参与该抓取；`fresh_sweep_status` = 31 windowed queries (p1 12 + p2 9 + p3 7 + diag 3): 31/31 HTTP 200），相对 10-04 基池净增 **1** 篇；池内最新 `published` = 2026-10-02（lag=5 天，arXiv 公告滞后正常区间 ≤5）
- **seen-state**：`E:/tool/Hermes/cache/radar/arxiv_seen.json`，推后 60 条（本期 +10）
- **计数**：候选 **203** → 通过关键词策略 **123** → 已推过（去重） **50** → **本期新推 10 篇**（另有 63 篇通过策略但未进前十，留待后续）
- 本期唯一的外部请求：3 个 GitHub 仓库验活 + 最终 README 推送。

## 一、本期要点

- **全部是平局截断出来的榜**：10 篇相关度只落两档（84 分 2 篇 / 82 分 8 篇），排序在 82 分档内部完全由 `updated` 日期决定（两键排序：相关度为主、更新时间破平局）。
- **入榜全部是存量论文（2025-10-07 ～ 2026-09-16），没有 10 月新投稿**：365 天窗口 + seen-state 去重推进 50→60 的自然结果；池里最新 `published` 2026-10-02 的 1 篇（`2610.04091` 纯盲解混）未命中 A/B/C/D，不入榜——不是召回失败。
- **稀疏主题继续为空**：C 组（超分+分类交叉项）连续第 6 期 **0 篇**；D 组（基础模型 / 高效微调）**两半均为 0 篇**。
- **可复现性**：A 0 篇 ／ B 3 篇 ／ C 7 篇；3 篇声明代码且仓库**全部验活 200**（上期只有 1 篇 B）。
- **主题撞车**：`2609.22333`（XAI 引导降维）与 `2609.10334`（降维 + 监督分类）同期入榜，都是「降维 → HSI 分类」这条老线；两篇都无代码。

## 二、筛选结果

### 高光谱筛选结果（365 天窗口 + 去重）

- 拉取候选 **203** 篇 → 通过关键词策略 **123** 篇 → 已推过（去重剔除）**50** 篇 → **本期新推 10 篇**（另有 63 篇通过但未进前十，留待后续）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C/D 关键词之一；pansharpening、multispectral 单独出现不算；SAR/雷达类无条件剔除
- 排序：与「超分+分类」方向的相关度（主）+ 更新时间（仅用于打破相近分数的平局），**不按投稿时间**

- 可复现性：**A（代码+数据）0 篇** / B（仅代码）3 篇 / C（未声明）7 篇　— 由摘要 + arXiv comment 判定，C 表示「未声明」而非核实不存在

| # | 标题 | arXiv | 相关度 | 更新时间 | 可复现性 |
|---|---|---|---|---|---|
| 1 | Label Semantics for Robust Hyperspectral Image Classification | 2510.07556v1 | 84 | 2025-10-08 | B |
| 2 | Compact Multi-level-prior Tensor Representation for Hyperspectral Image Super-resolution | 2510.06098v1 | 84 | 2025-10-07 | B |
| 3 | Dimensionality reduction for AI based hyperspectral image classification based on XAI | 2609.22333v1 | 82 | 2026-09-16 | C |
| 4 | Dimensionality Reduction for Hyperspectral Image Classification | 2609.10334v1 | 82 | 2026-09-09 | C |
| 5 | Lightweight Interpretable RGB-Guided Hyperspectral Super-Resolution under Real Cross-resolution Misalignment | 2609.01060v1 | 82 | 2026-09-01 | C |
| 6 | Interpretable Landsat-to-Hyperspectral Dual Super-Resolution Without Large Matrix Inversion | 2608.22790v1 | 82 | 2026-08-24 | B |
| 7 | Convolution-Free Holistic Multivariance Decomposition Layer for Efficient Hyperspectral Image Classification Tensor Networks | 2608.16241v1 | 82 | 2026-08-17 | C |
| 8 | Registration-Free Hyperspectral Reconstruction from RGB via a Permutation-Invariant Gram-Matrix Principle | 2608.14994v1 | 82 | 2026-08-15 | C |
| 9 | PNEC-Mamba: Prototype-Guided Positive-Negative Evidence Calibration for Hyperspectral Image Classification | 2608.01910v1 | 82 | 2026-08-03 | C |
| 10 | Adaptive Band Selection for Hyperspectral Classification with Spatially Disjoint Evaluation | 2606.06684v1 | 82 | 2026-06-04 | C |

**可复现性判定依据**

- 1. `B` — code: github.com/milab-nsu/S3FN
- 2. `B` — code: github.com/WongYinJ
- 3. `C` — 摘要与 comment 均未声明代码/数据
- 4. `C` — 摘要与 comment 均未声明代码/数据
- 5. `C` — 摘要与 comment 均未声明代码/数据
- 6. `B` — code: github.com/IHCLab/PAINT
- 7. `C` — 摘要与 comment 均未声明代码/数据
- 8. `C` — 摘要与 comment 均未声明代码/数据
- 9. `C` — 摘要与 comment 均未声明代码/数据
- 10. `C` — 摘要与 comment 均未声明代码/数据

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
- …另有 68 条

### ①–⑥ 分组清单（本期）

**① 超分+下游任务联合优化（C 组）：0 篇 —— 本期无交叉项**

**② 纯超分（A 组）：4 篇**

- Compact Multi-level-prior Tensor Representation for Hyperspectral Image Super-resolution · [2510.06098v1](https://arxiv.org/abs/2510.06098) · 相关度 84 · 可复现性 B
- Lightweight Interpretable RGB-Guided Hyperspectral Super-Resolution under Real Cross-resolution Misalignment · [2609.01060v1](https://arxiv.org/abs/2609.01060) · 相关度 82 · 可复现性 C
- Interpretable Landsat-to-Hyperspectral Dual Super-Resolution Without Large Matrix Inversion · [2608.22790v1](https://arxiv.org/abs/2608.22790) · 相关度 82 · 可复现性 B
- Registration-Free Hyperspectral Reconstruction from RGB via a Permutation-Invariant Gram-Matrix Principle · [2608.14994v1](https://arxiv.org/abs/2608.14994) · 相关度 82 · 可复现性 C

**③ 纯分类（B 组）：6 篇**

- Label Semantics for Robust Hyperspectral Image Classification · [2510.07556v1](https://arxiv.org/abs/2510.07556) · 相关度 84 · 可复现性 B
- Dimensionality reduction for AI based hyperspectral image classification based on XAI · [2609.22333v1](https://arxiv.org/abs/2609.22333) · 相关度 82 · 可复现性 C
- Dimensionality Reduction for Hyperspectral Image Classification · [2609.10334v1](https://arxiv.org/abs/2609.10334) · 相关度 82 · 可复现性 C
- Convolution-Free Holistic Multivariance Decomposition Layer for Efficient Hyperspectral Image Classification Tensor Networks · [2608.16241v1](https://arxiv.org/abs/2608.16241) · 相关度 82 · 可复现性 C
- PNEC-Mamba: Prototype-Guided Positive-Negative Evidence Calibration for Hyperspectral Image Classification · [2608.01910v1](https://arxiv.org/abs/2608.01910) · 相关度 82 · 可复现性 C
- Adaptive Band Selection for Hyperspectral Classification with Spatially Disjoint Evaluation · [2606.06684v1](https://arxiv.org/abs/2606.06684) · 相关度 82 · 可复现性 C

**④ 基础模型 / 高效微调（D 组，分两半）**

- 基础模型 / 预训练 / 表征学习：**0 篇**
- 高效微调 / 适配（D_ADAPT 子类）：**0 篇**

**⑤ benchmark：0 篇**
**⑥ 其他：0 篇**

- 分组标签由唯一真相源 `radar_keywords.KeywordPolicy().abc_hit(标题+摘要)` 判定（标题与摘要同权，仅在摘要命中也会被记入分组列，不会显示为 `-`）。

## 三、Top 3 精读（摘要级）

### 1. Label Semantics for Robust Hyperspectral Image Classification（S3FN）

- [2510.07556v1](https://arxiv.org/abs/2510.07556) · 相关度 **84**（本期最高）· 可复现性 **B**（`code: github.com/milab-nsu/S3FN`，验活 ✅ 200）· comment: IJCNN 2025 已接收 · 2025-10-08
- **方法**：用 LLM 为每个类别生成文本描述，经 BERT/RoBERTa 编码成标签语义向量，再与光谱-空间特征做**特征-标签对齐**；不改主干网络，属于「语义补强」而非新架构。
- **实验**：Hyperspectral Wood、HyperspectralBlueberries、DeepHS-Fruit 三个数据集，报告显著提升。
- **局限（推断＋来源）**：① 三个数据集都是近景/物质类高光谱，**未在经典遥感基准（Indian Pines / Pavia / WHU-Hi）验证**；② 摘要未给任何数值与消融，「文本语义在样本充足时是否仍有效」无法判断；③ 依赖 LLM 生成的类别描述质量，未做敏感性分析。
- **延伸**：把「LLM 标签文本」换成跨传感器共享锚点，用于跨场景/标签空间不重叠的迁移（与 2512.08989 的跨场景知识整合同线）。

### 2. Compact Multi-level-prior Tensor Representation for Hyperspectral Image Super-resolution

- [2510.06098v1](https://arxiv.org/abs/2510.06098) · 相关度 **84** · 可复现性 **B**（`code: github.com/WongYinJ`，验活 ✅ 200）· 2025-10-07
- **方法**：模型驱动。块张量分解把 HR-HSI 解耦为**光谱子空间 + 空间图**，空间图堆叠成空间张量，用非凸的 *mode-shuffled tensor correlated total variation* 同时建模高阶低秩与平滑先验；用线性化 ADMM（L-ADMM）求解，并**理论证明 KKT 收敛性**。
- **实验**：多个 HSI-MSI 融合数据集（摘要未具名——标注为**未具名**，不推断）。
- **局限**：多块结构 + 多先验带来权重平衡与优化复杂度（摘要自承）；**未报告运行时间/参数量**；是否与近期 Transformer/扩散 SR 基线对比，摘要无法判断。
- **延伸**：把该非凸张量先验做成即插即用正则项接进深度 SR（PnP-ADMM），兼顾可解释与速度；或用它监督 2609.01060 那类轻量 RGB 引导 SR 的**真实跨分辨率错配**场景。

### 3. Interpretable Landsat-to-Hyperspectral Dual Super-Resolution Without Large Matrix Inversion（PAINT）

- [2608.22790v1](https://arxiv.org/abs/2608.22790) · 相关度 **82** · 可复现性 **B**（`code: github.com/IHCLab/PAINT`，验活 ✅ 200） · comment: JSTARS 已接收 · 2026-08-24
- **方法**：把 Landsat-8/9 多光谱**可解释地**转成 AVIRIS 级 HSI，同时做空间 SR（30→15 m）与光谱 SR（7→172 波段），称 DualSR；空间细节用 panchromatic sharpening（物理有依据，**非生成式**）；用 Woodbury W-Lemma + 光谱连续性先验构造 ADMM-Net，并设计**免大矩阵求逆**的近端梯度下降网络 PGD-Net 解决像素级 LMI。
- **实验**：Landsat→AVIRIS 级重建；下游 Landsat 分类 **78.98% OA / 76.06% kappa → 92.16% OA / 90.98% kappa**。
- **局限**：强绑定 AVIRIS 级 172 波段目标与 panchromatic 通道，换传感器需重训；分类提升是**间接指标**，摘要未报告重建保真度（PSNR/SAM/ERGAS）数字。
- **延伸**：这正是本期缺失的 **C 组（SR+下游联合）** 的天然起点——把分类损失反传进重建网络。

## 四、3 个可做选题

**① 面向分类指标的 SR 联合优化（补上 C 组）**

- 假设：以分类损失微调的重建网络，可用少量 PSNR 代价换显著 OA/kappa 提升。
- 方法：以 PAINT 的 PGD-ADMM 为主干，接下游分类头，分类损失（+ 光谱连续性正则）联合反传；对照纯重建损失训练。
- 数据：Landsat-8/9 → AVIRIS 级 DualSR 设定；下游接 WHU-Hi / Indian Pines / Pavia。
- 指标：OA/AA/kappa 为主，PSNR/SAM/ERGAS 为辅；基线：PAINT、双三次 + 独立分类器、S3FN。
- 风险：重建—分类梯度尺度失衡（需分层学习率/梯度归一）；LMI-free 结构下的显存约束。

**② LLM 标签语义作为跨场景锚点**

- 假设：类别文本语义构成跨传感器/跨场景的共享空间，可缓解目标域标注极少的问题。
- 方法：S3FN 的文本嵌入 + 跨场景知识整合（2512.08989 的思路），做光谱-文本对比对齐后再微调分类头。
- 数据：WHU-Hi 系列（不同相机/场景）、Pavia↔Indian Pines 跨域。
- 指标：few-shot（1/5/10 样本/类）OA、跨场景 OA 下降幅度；基线：S3FN、微调 ViT/Mamba 分类器。
- 风险：LLM 描述与光谱行为可能弱相关，需先验证文本-光谱互信息；描述生成的类别名依赖公开数据集的语义标签。

**③ 非凸张量先验 × 轻量深度 SR（可解释 + 低算力）**

- 假设：模型驱动的高阶低秩/平滑先验在**真实错配**与少样本下优于纯数据驱动轻量网络。
- 方法：把 2510.06098 的 mode-shuffled 张量相关全变差做成可微正则项，嵌入 2609.01060 式轻量 RGB 引导 SR。
- 数据：CAVE/Harvard 合成 + 真实跨分辨率错配（无人机 RGB + 快照 HSI）。
- 指标：PSNR/SAM/ERGAS + 参数量/FLOPs/推理时延；基线：2510.06098、2609.01060、SwinIR 类。
- 风险：真实错配数据获取难，需合成退化管线；非凸正则的可微化可能破坏收敛性理论。

## 五、会议论文

### 会议论文（Conference）

**arXiv × 会议索引匹配**：10 个候选，命中 0 篇同时有会议版本。

（本期无候选命中会议版本。）

**会议新进榜（Conference spotlight）**：本次首次纳入 0 篇。

_已更新 seen-state（0 个 venue）_

## 六、排除说明

- **SAR/微波无条件剔除**：`UniDiff`（摘要含 `synthetic aperture radar`，虽然主题是扩散模型参数高效适配）。
- **纯仪器/传感器类**：`HAMscope`（快照自体荧光显微内窥）、`SpectralCA`（UAV 高光谱相机跨注意力）、`Visible to Longwave-infrared via an inverse-designed monolithic lens`（单片透镜）。
- **池内最新一篇也没入选**：`2610.04091`（Robust blind unmixing: A geometric approach to overcoming basis variation，2026-10-02 发布，脚本给出原因 `纯传感器/仪器类（spectral imaging），未命中 A/B/C/D`）——该「仪器类」标签对一篇纯解混论文并不贴切，如实照录；结论一致：纯解混不是 A/B/D 任务，不入榜（范围冻结下的设计行为）。
- **大量纯解混/NMF 被过滤**（SWAN、DeepSalt、Diffusion Posterior Sampler for Unmixing、Convex Smooth Separable NMF 等）：解混不是 A/B/D 任务词，不入榜；这是**故意**的，不是缺口。
- 另有 80 篇被策略过滤（原因见上表下的完整清单）；通过 carve-out 入池但相关度为 0 的论文不会进榜。

## 七、本期可复现（A/B 档）与可跑的 baseline

### 本期可复现（A/B 档，便于先跑）

- A（代码+数据）**0** 篇 ／ B（仅代码）**3** 篇 ／ C（未声明）7 篇

| 标题 | arXiv | 档 | 依据 |
|---|---|---|---|
| Label Semantics for Robust Hyperspectral Image Classification | 2510.07556v1 | B | code: github.com/milab-nsu/S3FN |
| Compact Multi-level-prior Tensor Representation for Hyperspectral Image Super-resolution | 2510.06098v1 | B | code: github.com/WongYinJ |
| Interpretable Landsat-to-Hyperspectral Dual Super-Resolution Without Large Matrix Inversion | 2608.22790v1 | B | code: github.com/IHCLab/PAINT |

### 可跑的 baseline（本期论文提到的开源实现，已验活）

| 仓库 | 出处（arXiv ID） | HTTP |
|---|---|---|
| https://github.com/IHCLab/PAINT | 2608.22790v1 | ✅ 200 |
| https://github.com/WongYinJ | 2510.06098v1 | ✅ 200 |
| https://github.com/milab-nsu/S3FN | 2510.07556v1 | ✅ 200 |

共 3 个仓库：**3 个可访问**

---

*第 6 期 · 生成于 2026-10-07 · 数据来自本地缓存池（未做新扫）· 排序由 `radar_filter.py` 两键排序完成，本期未修改任何关键词/过滤脚本*