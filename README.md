# 高光谱研究雷达日报 · 2026-10-05（第 4 期）

## 来源与窗口

- **arXiv：本期按硬性限制未做任何新扫**（连续多日限流；上一期死于一个 7,431 s 的 fetch 被 watchdog 杀掉）。本期使用**本地 365 天缓存池** `candidates-2026-10-04.json`（**202 篇**；文件内 `generated_at = 2026-10-04`，`fresh_sweep_status` 自记为「11 条查询全部 HTTP 429（Rate exceeded.），新增 0 行」）。
- 池口径（实测）：`published` 跨度 **2025-10-03 → 2026-09-30**（= 本报告的真实有效窗口），`updated` 跨度 2025-10-07 → 2026-09-30；其中 `published ≥ 2026-09-01` 的近期投稿 **26 篇**。池与上一期是**同一份、未变化**，故「候选 202」与上一期可直接比较。
- **CVF**：CVPR2026 本地索引 **4,042** 条（2026-10-02 缓存，未重下），本期只做离线匹配。
- 策略冻结与运行健康：`selftest 18/18 passed`；`radar_filter.py 66877f5979fe` / `radar_keywords.py d405ccb11486` / `search_keywords.txt 4382dbe26daf` —— **与上一期三个哈希完全一致，运行期间未修改任何策略文件**，计数可与上一期直接比较。
- 去重状态：seen-state 由 **30 → 40**（本期写入 10 篇）。

## 本期要点

1. **本期是「平局截断」的一期**：入选 10 篇**全部相关度 84**；未推送的 83 篇里 **12 篇并列 84**，两键排序 `(-relevance, -updated)` 取其中**更新最新的 10 篇**（2026-04-28 → 2026-03-05）。排名第 11 位仍是 84，但其更新时间是 **2025-10-08**，直接跳到上一年批次——说明截断发生在**相关度平局内部**，不是跨档降级，也不是漏筛（设计预期）。
2. **C 组（超分+分类交叉项）本期 0 篇** —— 365 天窗口、123 篇过筛里再次无一命中交叉词形，**本期无交叉项**（连续第 4 期）。
3. **A/B 仍是主战场**：123 篇过筛中 A 组 **42**、B 组 **59**、D 组 **18**（D 内部：基础模型/预训练 15、仅适配 2、两者兼有 1）；本期新推 10 篇 = **A 组 2 篇、B 组 8 篇、C/D 组 0 篇**。
4. **可复现性**：10 篇中 A 档（代码+数据）**0**、B 档（仅代码）**6**、C 档（未声明）**4**；6 个仓库**全部 HTTP 验活 200**（见文末）。
5. **「解混」在新推论文里同时出现在超分与分类两侧**：`2601.22755` 把丰度当作**超分的工作域**（合成丰度、无监督），`2604.09948` 把丰度当作**分类的 token 组织依据**（聚类 Top-K + 多任务）——两侧各有一块，却没人把它们接成一条链。这是补 C 组空缺最直接的现成材料（见选题 1、2）。

## 筛选结果

## 高光谱筛选结果（365 天窗口 + 去重）

- 拉取候选 **202** 篇 → 通过关键词策略 **123** 篇 → 已推过（去重剔除）**30** 篇 → **本期新推 10 篇**（另有 83 篇通过但未进前十，留待后续）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C/D 关键词之一；pansharpening、multispectral 单独出现不算；SAR/雷达类无条件剔除
- 排序：与「超分+分类」方向的相关度（主）+ 更新时间（仅用于打破相近分数的平局），**不按投稿时间**

- 可复现性：**A（代码+数据）0 篇** / B（仅代码）6 篇 / C（未声明）4 篇　— 由摘要 + arXiv comment 判定，C 表示「未声明」而非核实不存在

| # | 标题 | arXiv | 相关度 | 更新时间 | 可复现性 |
|---|---|---|---|---|---|
| 1 | MixerCA: An Efficient and Accurate Model for High-Performance Hyperspectral Image Classification | 2604.26138v1 | 84 | 2026-04-28 | B |
| 2 | A Synergistic CNN-Transformer Network with Pooling Attention Fusion for Hyperspectral Image Classification | 2604.23622v1 | 84 | 2026-04-26 | B |
| 3 | Synthetic Abundance Maps for Unsupervised Super-Resolution of Hyperspectral Remote Sensing Images | 2601.22755v2 | 84 | 2026-04-21 | B |
| 4 | ConvVitMamba: Efficient Multiscale Convolution, Transformer, and Mamba-Based Sequence modelling for Hyperspectral Image Classification | 2604.18856v1 | 84 | 2026-04-20 | B |
| 5 | Unmixing-Guided Spatial-Spectral Mamba with Clustering Tokens for Hyperspectral Image Classification | 2604.09948v1 | 84 | 2026-04-10 | B |
| 6 | Cross-Domain Few-Shot Learning for Hyperspectral Image Classification Based on Mixup Foundation Model | 2601.22581v2 | 84 | 2026-04-07 | B |
| 7 | Physics-Informed Untrained Learning for RGB-Guided Superresolution Single-Pixel Hyperspectral Imaging | 2604.03572v1 | 84 | 2026-04-04 | C |
| 8 | LGEST: Dynamic Spatial-Spectral Expert Routing for Hyperspectral Image Classification | 2603.24045v1 | 84 | 2026-03-25 | C |
| 9 | 3D Fourier-based Global Feature Extraction for Hyperspectral Image Classification | 2603.16426v1 | 84 | 2026-03-17 | C |
| 10 | A Benchmark Study of Neural Network Compression Methods for Hyperspectral Image Classification | 2603.04720v1 | 84 | 2026-03-05 | C |

**可复现性判定依据**

- 1. `B` — code: github.com/mqalkhatib/MixerCA
- 2. `B` — code: github.com/chenpeng052/SCT-Net.git
- 3. `B` — code: github.com/xinxinxu99/SISR-DL.git
- 4. `B` — code: github.com/mqalkhatib/ConvVitMamba
- 5. `B` — code: github.com/GSIL-UCalgary/Unmixing_guided_Mamba.git
- 6. `B` — code: github.com/Naeem-Paeedeh/MIFOMO
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
- …另有 67 条

## 分组（本期 10 篇）

- **① 超分+下游任务联合优化（C 组）：0 篇** —— **本期无交叉项**。
- **② 纯高光谱超分（A 组）：2 篇** —— Synthetic Abundance Maps `2601.22755v2`、Physics-Informed Untrained Learning `2604.03572v1`。
- **③ 纯高光谱分类（B 组）：8 篇** —— MixerCA `2604.26138v1`、SCT-Net `2604.23622v1`、ConvVitMamba `2604.18856v1`、Unmixing-Guided Mamba `2604.09948v1`、MIFOMO `2601.22581v2`、LGEST `2603.24045v1`、HGFNet `2603.16426v1`、NN Compression Benchmark `2603.04720v1`。
- **④ 高光谱基础模型 / 高效微调（D 组，分两半）：0 篇**
  - **基础模型 / 预训练 / 表征学习：0 篇**
  - **高效微调 / 适配：0 篇**
- **⑤ benchmark / 数据集：** `2603.04720`（压缩方法基准研究）与 `2604.18856`（含 3 个 UAV QUH 数据集）**同时命中 B 组**，按优先组归入 ③（不重复计）。
- **⑥ 其他高光谱：0 篇。**
- 一条来源事实（非推断）：入选的 MIFOMO `2601.22581` 摘要是 "remote sensing (RS) foundation model"，**未命中 D 组词形**（D 组要求 `hyperspectral foundation model` 等），故归 ③。这是既定词表的确定行为，不是漏筛。

## Top 3 精读（摘要级，未抓 PDF）

挑选说明：本期 10 篇中 8 篇为纯分类，故 Top 3 取「**相关度第一的分类基线** + **唯一带代码的纯超分** + **唯一把解混与分类耦合的多任务工作**」，并跳过与 MixerCA 同族的 SCT-Net（rank 2，纯分类）。

### 1. MixerCA: An Efficient and Accurate Model for High-Performance Hyperspectral Image Classification
`2604.26138v1` · rel **84** · 更新 2026-04-28 · 可复现性 **B**（code: github.com/mqalkhatib/MixerCA）

- **问题**：HSI 分类要在多波段、少标注下同时拿精度与低算力。
- **方法**：MixerCA —— 用**深度可分离卷积 + 自注意力**统一成一个轻量结构：token mixing 与 channel mixing 解耦空间/通道交互，coordinate attention 补位置信息，**全网络保持一致分辨率**并直接处理 HSI patch（不走主流的下采样—上采样）。
- **证据**：四个高光谱基准上对 2D-CNN / 3D-CNN / Tri-CNN / HybridSN / ViT / Swin Transformer 称有明确优势（**摘要未给数值**）。
- **局限**：纯分类、无超分；摘要**无量化数字**；未报告参数量/延迟（「efficient」未量化）；无跨传感器验证；is 期刊 preprint（RSASE），非会议。
- **可延伸**：其「一致分辨率 + 通道/token 解耦」正是超分主干常用的形态——把 MixerCA 直接当 SR 输出上的分类头，是构造 C 组实验的最低成本途径（选题 3 的对照）。

### 2. Synthetic Abundance Maps for Unsupervised Super-Resolution of Hyperspectral Remote Sensing Images
`2601.22755v2` · rel **84** · 更新 2026-04-21 · 可复现性 **B**（code: github.com/xinxinxu99/SISR-DL）

- **问题**：HS-SISR 主流方法是**监督**的，需要高分辨 GT；真实场景往往拿不到。
- **方法**：**无监督**框架 —— ①先把 LR HSI 解混为端元 + 丰度；②用**死叶模型**合成丰度图（统计特性继承自待超分的 LR 图像，并利用已知的**传感器 PSF**）；③只用合成丰度训练网络做**丰度超分**；④推理时把超分丰度与端元重组回高分 HSI。**训练全程不需要 HR 参考**。
- **证据**：3 个数据集 × 3 个缩放因子 × 多指标，验证合成数据的训练价值与方法的有效性（摘要未列具体 PSNR/SSIM）。
- **局限**：**强依赖解混质量与 PSF 已知**（PSF 估计不准即分布偏移）；无监督设定下 PSNR 类有参考指标的可信度显著下降；未报告跨传感器泛化；大缩放因子下无监督方法普遍退化。
- **可延伸**：这条「解混 → 丰度超分 → 重组」链天然能为分类提供**无需 GT 的高分输入**，而 `2604.09948` 已证明「丰度 → 聚类 token → 分类」可行——两者拼接即 C 组的现成骨架（选题 1、2）。

### 3. Unmixing-Guided Spatial-Spectral Mamba with Clustering Tokens for Hyperspectral Image Classification
`2604.09948v1` · rel **84** · 更新 2026-04-10 · 可复现性 **B**（code: github.com/GSIL-UCalgary/Unmixing_guided_Mamba）

- **问题**：光谱混合效应、空间—光谱异质、类边界与细节难以保持。
- **方法**：①光谱解混网络，自学习端元与丰度并显式建模**端元可变性**；②按丰度图的聚类定义 **Top-K token 选择**，自适应排序 Mamba 序列；③**解混引导的空间—光谱 Mamba 模块**；④**多任务监督**（端元—丰度 + 分类标签），同时输出分类图、光谱库与丰度图。
- **证据**：四个 HSI 数据集上称显著优于 SOTA（摘要未给数值）。
- **局限**：任务仍是**分类**（不是 SR）；多任务权重需调；Mamba 序列排序对 token 选择敏感；未报告推理成本；仅声明代码、未声明数据。
- **可延伸**：它把「解混 + 聚类 + 多任务」做成了分类侧工具；若让其丰度场与 `2601.22755` 的超分丰度**共享**，就是「SR 与分类共享物理瓶颈」的联合框架（选题 2）。

## 3 个可做选题

### 选题 1：无监督合成丰度超分 → 低标注/跨域分类（补 C 组空缺的轻量路线）
- **Problem**：C 组连续 4 期 0 篇；本期同时出现「无监督丰度超分」`2601.22755`（训练无需 HR GT）与「跨域少样本分类」`2601.22581`（跨域标注昂贵）。二者互不解决对方的问题：超分不评测分类增益，分类固定输入分辨率。
- **Hypothesis**：用 `2601.22755` 的无监督 SR 提升分辨率后接分类，在低标注（1%/5%）与跨域设定下，其分类增益**显著大于**「监督 SR 预处理」或「不超分直接分类」，且**不需要目标域 HR GT**。
- **Method sketch**：LR HSI → 解混 → 合成丰度训练丰度超分网络（`2601.22755`）→ 重组 HR HSI → 分类头（MixerCA `2604.26138`；跨域时用 MIFOMO `2601.22581` 的冻结骨干 + coalescent projection）。对照：无 SR / 监督 SR / 无监督 SR。消融：PSF 是否准确（注入 PSF 误差）。
- **数据与指标**：Pavia University、Chikusei、WHU-Hi-LongKou；SR：PSNR/SSIM/SAM/ERGAS，分类：OA/AA/Kappa + 每类召回；重点是「SR 质量 → 分类增益」传导曲线 + 跨传感器（Pavia→Chikusei）。
- **Baselines**：SISR-DL `2601.22755`、动态稀疏注意力 CNN-SR、无 SR 分类、监督 SR + 分类。
- **最小可证伪实验**：单数据集、5% 标注，比较「无监督 SR + 分类」vs「不超分 + 分类」；若 OA 差在 3 个随机种子下均 <0.5%，假设不成立。
- **Risk**：无监督 SR 的伪影可能被分类器放大；跨传感器 PSF 假设失效即退化；C 组长期为空本身可能说明该联结收益有限（**本期最需警惕的反证**）。

### 选题 2：共享解混瓶颈的「超分 × 分类」联合框架
- **Problem**：`2604.09948` 证明解混 + 多任务能提升分类，`2601.22755` 证明丰度可作超分的工作域；但无人把**同一套端元/丰度**同时接到 SR 与分类上——这正是 C 组本身。
- **Hypothesis**：以端元/丰度为共享中间表示联合优化 SR 与分类，在低标注下分类增益显著大于「先 SR 再分类」的解耦流程，且联合训练使丰度估计更准（互相正则）。
- **Method sketch**：主干用 `2601.22755` 的丰度超分（产出超分丰度场）；分类侧接 `2604.09948` 的 Top-K 聚类 token + 多任务损失；共享解混模块。对照：解耦两阶段 / 共享 vs 不共享丰度 / 只 SR / 只分类。
- **数据与指标**：Pavia University、Chikusei、WHU-Hi-LongKou；SR：PSNR/SSIM/SAM；分类：OA/AA/Kappa；额外报丰度解混误差（SAD/RMSE）以验证「互相正则」。
- **Baselines**：`2601.22755`（纯 SR）、`2604.09948`（纯分类）、解耦 SR→分类、无 SR 直接分类。
- **最小可证伪实验**：单数据集、1% 标注，「共享丰度瓶颈的联合训练」vs「解耦」；若 OA 差在 3 个种子下均 <0.3% 且丰度 SAD 无改善，假设不成立。
- **Risk**：联合训练调参成本高；解混差会同时拖累两侧；C 组稀疏是反证信号。

### 选题 3：把「效率—精度」评估搬到高光谱超分（可部署 SR 基准）
- **Problem**：分类侧已出现成组的效率工作（MixerCA 轻量、ConvVitMamba 轻量 Mamba、LGEST 稀疏专家路由），并有 `2603.04720` 专门评测剪枝/量化/蒸馏；而**超分侧**本期两篇（含 `2604.03572` 的免训练框架）均未报告参数量/延迟/显存——超分侧缺一份可部署性对照。
- **Hypothesis**：把 `2603.04720` 的压缩流程（pruning / quantization / distillation）直接施于现有 HSI-SR 主干，可在 PSNR 下降 <0.2 dB 内把参数量压到 1/4、延迟压到 1/3。
- **Method sketch**：以 `2601.22755` 的丰度超分网络与一个 CNN/Mamba SR 主干为对象，逐一施加剪枝/量化/蒸馏，测精度—成本 Pareto；给出统一延迟协议（batch=1、固定分辨率、同 GPU）。
- **数据与指标**：Pavia University、Chikusei；PSNR/SSIM/SAM/ERGAS + 参数量 + FLOPs + 单图延迟 + 显存。
- **Baselines**：未压缩 SR 主干、`2601.22755`、经典 CNN-SR。
- **最小可证伪实验**：单数据集、单主干做 INT8 量化；若延迟下降 <2× 或 PSNR 下降 >0.5 dB，假设不成立。
- **Risk**：易被质疑为纯工程调优；量化的精度损失对光谱维度敏感；须严格控制变量并公开测量协议。

## 会议论文（CVPR2026，本地索引离线匹配）

- 本期入选 10 篇中，**0 篇**同时有 CVPR2026 版本（多为 2026 年 3–4 月新投的分类/超分 preprint，尚无会议版）。
- 放回全池口径：**202 个候选命中 5 篇**同时有会议版本（与上一期相同，池未变）——视频级压缩光谱重建、多光谱→NASA 高光谱的光谱超分、抗光谱漂移的双门控 MoE、无配准 HSI 超分（UAFL，上期已推）、超表面快照相机（仪器类）。
- **会议新进榜（spotlight）：0 篇。** CVPR2026 seen-state 已于 2026-10-02 被消费（3 条），这是该模块的一次性设计，不是匹配失效。

## 排除说明

- 默认排除 SAR/雷达类：`UniDiff`（PEFT + 地物分类）与 `SpectralEarth-FM`（高光谱多模态预训练）因摘要含 **synthetic aperture radar** 被**无条件剔除**。
- 仪器/传感器类：`SpectralCA`、`HAMscope`（快照自体荧光显微）、`MetaSpectra+`（超表面相机）、`Visible to Longwave-infrared imaging via an inverse-designed monolithic lens` 等，唯一话题证据是 `spectral imaging`，判为仪器排除。
- 门禁/话题未命中：`A UAV-Based VNIR Hyperspectral Benchmark Dataset for Landmine and UXO Detection`（有高光谱但未命中 A/B/C/D）、`SWAN`（自监督小波解混）、`Self-Supervised Super-Resolution for Sentinel-5P Hyperspectral Images`、`HSI-VAR`、`HyperCOD` 等。
- 门禁未满足：`AION-1`（天文全模态基础模型）、`Burst Image Quality Assessment`、`S3-CLIP` 未出现 hyperspectral/HSI。
- 上述规则由 `search_keywords.txt` 单一真相源执行，本期未改动任何策略文件。

### 本期可复现（A/B 档，便于先跑）

- A（代码+数据）**0** 篇 ／ B（仅代码）**6** 篇 ／ C（未声明）4 篇

| 标题 | arXiv | 档 | 依据 |
|---|---|---|---|
| MixerCA: An Efficient and Accurate Model for High-Performance Hyperspectral Image Classification | 2604.26138v1 | B | code: github.com/mqalkhatib/MixerCA |
| A Synergistic CNN-Transformer Network with Pooling Attention Fusion for Hyperspectral Image Classification | 2604.23622v1 | B | code: github.com/chenpeng052/SCT-Net.git |
| Synthetic Abundance Maps for Unsupervised Super-Resolution of Hyperspectral Remote Sensing Images | 2601.22755v2 | B | code: github.com/xinxinxu99/SISR-DL.git |
| ConvVitMamba: Efficient Multiscale Convolution, Transformer, and Mamba-Based Sequence modelling for Hyperspectral Image Classification | 2604.18856v1 | B | code: github.com/mqalkhatib/ConvVitMamba |
| Unmixing-Guided Spatial-Spectral Mamba with Clustering Tokens for Hyperspectral Image Classification | 2604.09948v1 | B | code: github.com/GSIL-UCalgary/Unmixing_guided_Mamba.git |
| Cross-Domain Few-Shot Learning for Hyperspectral Image Classification Based on Mixup Foundation Model | 2601.22581v2 | B | code: github.com/Naeem-Paeedeh/MIFOMO |

### 可跑的 baseline（本期论文提到的开源实现，已验活）

| 仓库 | 出处（arXiv ID） | HTTP |
|---|---|---|
| https://github.com/GSIL-UCalgary/Unmixing_guided_Mamba.git | 2604.09948v1 | ✅ 200 |
| https://github.com/Naeem-Paeedeh/MIFOMO | 2601.22581v2 | ✅ 200 |
| https://github.com/chenpeng052/SCT-Net.git | 2604.23622v1 | ✅ 200 |
| https://github.com/mqalkhatib/ConvVitMamba | 2604.18856v1 | ✅ 200 |
| https://github.com/mqalkhatib/MixerCA | 2604.26138v1 | ✅ 200 |
| https://github.com/xinxinxu99/SISR-DL.git | 2601.22755v2 | ✅ 200 |

共 6 个仓库：**6 个可访问**
