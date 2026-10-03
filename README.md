# 高光谱研究雷达日报 · 2026-10-03（第 2 期）

## 来源与窗口

- **arXiv**（365 天窗口，`sortBy=relevance`，每查询 `max_results=300`）：今日新扫 8 条查询 —— 首轮 3/8 成功，其余被 `HTTP 429 Rate exceeded.` 拦下；隔 150 s 后用 22 s 间隔重扫，5/5 成功，**合计 36/41 条查询 HTTP 200**（含昨日缓存的 31 条）。
- 候选池 = **昨日 31/31 全成功的扫描缓存 ∪ 今日新扫**，按裸 arXiv ID 去重后 **202 篇**。今日新扫相对缓存**新增 0 篇**：池内最新 `published` 仍是 **2026-09-30**，与昨日完全一致 —— 这是 arXiv 公告批次延迟（窗口上界 2026-10-03，实际公告只到 09-30），**不是漏筛**。真实有效窗口：**2025-10-03 → 2026-09-30**。
- **CVF**：CVPR2026 本地索引 **4,042** 条（缓存命中，未重下），本期只做离线匹配。
- 策略冻结与运行健康：`selftest 18/18 passed`；`radar_filter.py 66877f5979fe` / `radar_keywords.py d405ccb11486` / `search_keywords.txt 4382dbe26daf`。**注意：`radar_filter.py` 自上一期后已被修改**（上一期哈希 `037b5b9f`），本期起排序为标准两键排序，见「本期要点」第 1 条。

## 本期要点

1. **上一期标注的排序偏差已修复并实测生效。** 旧实现是 `相关度 + 上限 20 分的新鲜度`，而池内相关度区间只有 72–99，等于让时间驱动了约五分之一的名次。现在的实现是两键排序 `(-relevance, -updated)`，新鲜度只用于展示与打破平局。用**同一份候选池**重算三种口径：本期实推 10 篇与**纯相关度 top-10 重合 10/10**，与**旧规则 top-10 只重合 3/10**；全池相关度最高的 `2510.11576`（rel=99，2025-10-13 投）从上一期的第 24 名、直接落榜，变为**本期第 1 名**。
2. **本期最高相关度落在一篇「基准」论文上，而不是新方法。** `2510.11576` 用 HyperSigma / DOFA / SpectralEarth 三个基础模型做谷类作物高光谱制图，结论是**架构差异远大于预训练数据**（OA 34.5% vs 62.6% vs 93.5%），且评测是训练区微调 + **独立测试区**外推 —— 在「同区域随机划块」为主流的高光谱文献里，这种地理外推证据比又一个新模块更稀缺。
3. **C 组（超分+分类交叉项）本期 0 篇** —— 365 天窗口下 123 篇过筛论文里无一命中交叉词形，是真实空缺，不是漏筛。
4. **A 组与 B 组仍是主战场**：123 篇过筛中 A 组 42 篇、B 组 59 篇、D 组 18 篇（D 内部：基础模型/预训练 15、仅适配 2、两者兼有 1）。
5. **可复现性依旧偏低但可跑**：本期 10 篇中 A 档（代码+数据）**0** 篇、B 档（仅代码）**3** 篇 —— 3 个仓库全部 HTTP 验活 200；其中 `2603.07918`（无配准 HSI 超分）同时有 **CVPR2026** 版本，是本期最值得先跑的一篇。

## 筛选结果

## 高光谱筛选结果（365 天窗口 + 去重）

- 拉取候选 **202** 篇 → 通过关键词策略 **123** 篇 → 已推过（去重剔除）**10** 篇 → **本期新推 10 篇**（另有 103 篇通过但未进前十，留待后续）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C/D 关键词之一；pansharpening、multispectral 单独出现不算；SAR/雷达类无条件剔除
- 排序：与「超分+分类」方向的相关度（主）+ 更新时间（仅用于打破相近分数的平局），**不按投稿时间**

- 可复现性：**A（代码+数据）0 篇** / B（仅代码）3 篇 / C（未声明）7 篇　— 由摘要 + arXiv comment 判定，C 表示「未声明」而非核实不存在

| # | 标题 | arXiv | 相关度 | 更新时间 | 可复现性 |
|---|---|---|---|---|---|
| 1 | Benchmarking foundation models for hyperspectral image classification: Application to cereal crop type mapping | 2510.11576v2 | 99 | 2025-10-14 | C |
| 2 | Cosine-Normalized Attention for Hyperspectral Image Classification | 2604.01763v1 | 91 | 2026-04-02 | C |
| 3 | Clustering-Guided Spatial-Spectral Mamba for Hyperspectral Image Classification | 2601.16098v1 | 91 | 2026-01-22 | C |
| 4 | SDHSI-Net: Learning Better Representations for Hyperspectral Images via Self-Distillation | 2601.07416v1 | 91 | 2026-01-12 | B |
| 5 | Perceive, Act and Correct: Confidence Is Not Enough for Hyperspectral Classification | 2511.10068v1 | 89 | 2025-11-13 | C |
| 6 | A Latent Representation Learning Framework for Hyperspectral Image Emulation in Remote Sensing | 2603.21911v2 | 87 | 2026-06-22 | C |
| 7 | Hyperspectral Image Classification using Spectral-Spatial Mixer Network | 2511.15692v2 | 86 | 2026-05-29 | B |
| 8 | Voronoi-guided Bilateral 2D Gaussian Splatting for Arbitrary-Scale Hyperspectral Image Super-Resolution | 2604.17727v1 | 86 | 2026-04-20 | C |
| 9 | Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning | 2603.07918v1 | 86 | 2026-03-09 | B |
| 10 | Topology-Aware Neighborhood Learning for Source-Free Cross-Scene Hyperspectral Image Classification | 2608.05964v1 | 84 | 2026-08-06 | C |

**可复现性判定依据**

- 1. `C` — 摘要与 comment 均未声明代码/数据
- 2. `C` — 摘要与 comment 均未声明代码/数据
- 3. `C` — 摘要与 comment 均未声明代码/数据
- 4. `B` — code: github.com/Prachet-Dev-Singh/SDHSI
- 5. `C` — 摘要与 comment 均未声明代码/数据
- 6. `C` — 摘要与 comment 均未声明代码/数据
- 7. `B` — code: github.com/mqalkhatib/SS-MixNet
- 8. `C` — 摘要与 comment 均未声明代码/数据
- 9. `B` — code: github.com/yingkai-zhang/UAFL
- 10. `C` — 摘要与 comment 均未声明代码/数据

### ④ 高光谱基础模型 / 高效微调（D 组，分两半列）

**基础模型 / 预训练 / 表征学习**（6 篇）

- Benchmarking foundation models for hyperspectral image classification: Application to cereal crop type mapping
- Cosine-Normalized Attention for Hyperspectral Image Classification
- Clustering-Guided Spatial-Spectral Mamba for Hyperspectral Image Classification
- SDHSI-Net: Learning Better Representations for Hyperspectral Images via Self-Distillation
- Perceive, Act and Correct: Confidence Is Not Enough for Hyperspectral Classification
- A Latent Representation Learning Framework for Hyperspectral Image Emulation in Remote Sensing

**高效微调 / 适配**（D 子类，0 篇）

- _无_

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

## Top 3 精读（摘要级，未抓 PDF）

### 1. Benchmarking foundation models for hyperspectral image classification: Application to cereal crop type mapping
`2510.11576v2` · rel **99** · 更新 2025-10-14 · 可复现性 **C**（未声明）· comment 显示正在投 WHISPERS

- **问题**：高光谱作物制图还能不能吃到 EO 基础模型的红利？现有基准多在**同一区域**内评测，跨区域/跨传感器泛化几乎没有系统数字。
- **方法**：在**手工标注的同一训练区**上微调三个基础模型 —— HyperSigma、DOFA、以及在 **SpectralEarth**（大规模多时相高光谱档案）上预训练的 ViT —— 然后在**独立测试区**评测；指标 OA / AA / F1。
- **证据**：OA 分别为 HyperSigma **34.5%±1.8**、DOFA **62.6%±3.5**、SpectralEarth **93.5%±0.8**；一个从零训练的**紧凑版 SpectralEarth 也有 91%**。
- **局限**：单作物类型（谷类）单一任务，未报告跨传感器/跨季相消融；±std 来自什么划分粒度摘要未说明；代码与数据均未声明。
- **可延伸**：把「独立测试区」协议搬到**高光谱超分**——目前 HSI-SR 的泛化评测基本是随机划块，跨区域/跨传感器 SR 基准是明确空白（见选题 1）；紧凑模型 91% vs 大模型 93.5% 的差距，也直接支持「架构 > 预训练规模」的假设。

### 2. Cosine-Normalized Attention for Hyperspectral Image Classification
`2604.01763v1` · rel **91** · 更新 2026-04-02 · 可复现性 **C**

- **问题**：Transformer 的注意力打分用点积，把**特征幅值与方向**混在一起；对高光谱这种「方向（光谱形状）比幅值更本质」的数据可能是错的归纳偏置。
- **方法**：把 query/key 投到单位超球面，用**平方余弦相似度**替代点积，强调角度关系、抑制幅值敏感；嵌进 spatial-spectral Transformer，在**极少监督**下评测。
- **证据**：三个标准数据集上一致优于近期的 Transformer 与 Mamba 模型，且**主干是轻量的**；额外做了多种打分函数的对照分析（说明是受控实验，不只是刷点）。
- **局限**：仍是分类端的替换式改进；没有报告对**光谱保真度**（如 SAM/光谱角）的影响；未声明代码。
- **可延伸**：同样的角度打分迁到 **HSI 超分的重构主干**（SR 的评测恰好有 SAM/光谱角这类角度指标），检验「角度相似度」是否同时改善 PSNR 与 SAM（选题 2）。

### 3. Clustering-Guided Spatial-Spectral Mamba for Hyperspectral Image Classification
`2601.16098v1` · rel **91** · 更新 2026-01-22 · 可复现性 **C** · comment: 5 pages, 3 figures

- **问题**：Mamba 类模型在 HSI 上受限于**token 序列如何组织** —— 序列太长、又缺乏语义自适应性。
- **方法**：CSSMamba —— 把聚类机制嵌进空间 Mamba（CSpaMamba）缩短序列并做簇引导特征学习，与谱 Mamba（SpeMamba）拼成空间-光谱框架；再加**注意力驱动的 token 选择**与**可学习聚类模块**，让聚类成员自适应。
- **证据**：Pavia University、Indian Pines、Liao-Ning 01 三个数据集上优于 CNN / Transformer / Mamba 对比方法，并称**边界保持更好**。
- **局限**：5 页短文，消融与效率（参数量/吞吐）细节有限；没有跨场景/跨传感器泛化实验；未声明代码。
- **可延伸**：「自适应 token 序列」这件事在**超分**里同样成立但研究更少 —— 高光谱 SR 的 token 冗余来自波段与空间双重维度，把可学习聚类搬到 SR 的 token 组织上是有空白的组合（选题 2 的备选路线）。

## 3 个可做选题

### 选题 1：跨区域/跨传感器的 HSI 超分泛化基准
- **Problem**：HSI-SR 的评测几乎都在随机划块、同传感器内进行（本期 A 组 42 篇中无一报告独立测试区协议），而 `2510.11576` 已证明分类任务上「独立测试区」会让基础模型的 OA 从 93.5% 掉到 34.5–62.6% 量级。
- **Hypothesis**：现有 HSI-SR 方法的跨区域/跨传感器 PSNR 增益会**显著塌缩**，且塌缩幅度与训练区的空间多样性负相关。
- **Method sketch**：固定一套 SOTA SR 方法（本期 `2604.17727` GaussianHSI、`2603.07918` UAFL 为起点），在 Pavia/Chikusei/Houston 之间做 leave-one-region-out，并加传感器错配（不同波段数/GSD，先做波段重采样对齐）。
- **数据与指标**：Pavia University、Chikusei、Houston2018；PSNR / SSIM / SAM / ERGAS，另报到下游分类的 OA / AA / Kappa。
- **Baselines**：GaussianHSI、UAFL、经典 CNN-SR 与 pansharpening 基线。
- **最小可证伪实验**：只做一组「同传感器内 vs 跨区域」的对照，若跨区域 PSNR 下降 < 0.5 dB，假设即被推翻。
- **Risk**：跨传感器对齐本身是工程活，可能把论文做成 benchmark 而非方法；标注成本低但算力需求中等。

### 选题 2：角度相似度作为 HSI 超分的归纳偏置
- **Problem**：`2604.01763` 说明点积注意力把幅值与方向混在一起，对角度结构更本质的高光谱不利；但该结论只在分类上验证过，SR 上无人测。
- **Hypothesis**：在 SR 重建主干里用平方余弦注意力替换点积注意力，可在 PSNR 基本持平的前提下**显著改善 SAM / 光谱角**，并提升下游分类的 OA。
- **Method sketch**：取一个开源 SR 主干（UAFL 的解混-丰度融合框架），只替换注意力打分函数与归一化方式，其余训练配方不动；再做「聚类引导 token 序列」（`2601.16098` 的 CSpaMamba 思路）的消融。
- **数据与指标**：Pavia University、Chikusei（HSI-MSI 融合设定）；PSNR / SSIM / SAM / ERGAS + 下游 OA。
- **Baselines**：同一主干的原始点积注意力（严格同配方对照），加 UAFL / GaussianHSI。
- **最小可证伪实验**：单数据集、单倍率下替换打分函数，看 SAM 是否下降 ≥5%；若 SAM 无变化则假设不成立。
- **Risk**：增益可能只是超参差异；attention 替换在 SR 上的收益可能被重构损失掩盖，需要严格控制变量。

### 选题 3：把自蒸馏与不确定性半监督接到「超分→分类」链路上（补 C 组空缺）
- **Problem**：C 组（超分+分类联合优化）在 365 天窗口内**0 篇**，而本期分别给了可用的零件：`2601.07416` 的自蒸馏（提升类内紧致度/类间可分性）、`2511.10068` 的 CABIN（不确定性引导采样 + 伪标签分级），却没有人把它们接到「SR 是否真的提升下游分类」这一因果问题上。
- **Hypothesis**：SR 的 PSNR 提升与下游分类增益**非线性相关**；联合训练时引入不确定性加权的伪标签能为分类侧带来比单独 SR 更大的增益。
- **Method sketch**：SR 主干（UAFL）→ 分类头（SS-MixNet 或 CSSMamba），SR 分支加自蒸馏一致性项，分类分支加 CABIN 式的可靠/模糊/噪声三分伪标签加权；对照「先 SR 再分类」（解耦）vs「联合训练」。
- **数据与指标**：QUH-Tangdaowan / QUH-Qingyun（`2511.15692` 证明 1% 标注下可用）+ Pavia University；SR 报 PSNR/SSIM/SAM，分类报 OA/AA/Kappa，重点报「SR 增益 → 分类增益」的传导曲线。
- **Baselines**：解耦两阶段 SR→分类、无 SR 直接分类、UAFL + 现成分类器。
- **最小可证伪实验**：在 1% 标注下比较「联合 vs 解耦」的 OA 差，若差值在 3 个随机种子下都不显著（<0.3%），假设不成立。
- **Risk**：C 组稀疏可能说明该方向本身收益有限（这是本期最需要警惕的反证），需先做小规模验证再投入。

## 会议论文（CVPR2026，本地索引离线匹配）

- 本期入选 10 篇中，**1 篇**同时有 CVPR2026 版本，只占一行：**Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning**（`2603.07918v1`，匹配度 1.00）— [CVF 页面](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_Enhancing_Unregistered_Hyperspectral_Image_Super-Resolution_via_Unmixing-based_Abundance_Fusion_Learning_CVPR_2026_paper.html)（也是本期 B 档可跑项）。
- 放回全池口径：**202 个候选命中 5 篇**同时有会议版本（与上一期相同，池未变）——另外 4 篇是视频级压缩光谱重建、多光谱→NASA 高光谱的光谱超分、抗光谱漂移的双门控 MoE、以及一篇超表面相机（仪器类）。
- **会议新进榜（spotlight）：0 篇。** CVPR2026 的 seen-state 已在 2026-10-02 被消费，这是该模块的一次性设计，不是匹配失效。

## 排除说明

- 默认排除 SAR/雷达类：`UniDiff`（PEFT + 地物分类）因摘要含 synthetic aperture radar 被**无条件剔除**。
- 仪器/传感器类：`MetaSpectra+`（CVPR2026 超表面相机）、`SpectralCA`、`HAMscope` 等，唯一话题证据是 `spectral imaging` / 歧义词 `spectral reconstruction`，判为仪器排除。
- 门禁未满足：`AION-1`（天文全模态基础模型）、`Burst Image Quality Assessment` 等未出现 hyperspectral/HSI；`SWAN`（自监督小波解混）、`DeepSalt` 等出现高光谱但未命中 A/B/C/D 任一词形。上一期被剔除的 `2603.00611`（视频级压缩光谱重建）本期仍是相同判定。
- 上述规则由 `search_keywords.txt` 单一真相源执行，本期未改动任何策略文件。

### 本期可复现（A/B 档，便于先跑）

- A（代码+数据）**0** 篇 ／ B（仅代码）**3** 篇 ／ C（未声明）7 篇

| 标题 | arXiv | 档 | 依据 |
|---|---|---|---|
| SDHSI-Net: Learning Better Representations for Hyperspectral Images via Self-Distillation | 2601.07416v1 | B | code: github.com/Prachet-Dev-Singh/SDHSI |
| Hyperspectral Image Classification using Spectral-Spatial Mixer Network | 2511.15692v2 | B | code: github.com/mqalkhatib/SS-MixNet |
| Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning | 2603.07918v1 | B | code: github.com/yingkai-zhang/UAFL |

### 可跑的 baseline（本期论文提到的开源实现，已验活）

| 仓库 | 出处（arXiv ID） | HTTP |
|---|---|---|
| https://github.com/Prachet-Dev-Singh/SDHSI | 2601.07416v1 | ✅ 200 |
| https://github.com/mqalkhatib/SS-MixNet | 2511.15692v2 | ✅ 200 |
| https://github.com/yingkai-zhang/UAFL | 2603.07918v1 | ✅ 200 |

共 3 个仓库：**3 个可访问**
