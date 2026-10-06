# 高光谱研究雷达日报 · 2026-10-06（第 5 期）

## 来源与窗口

- **arXiv：本期按硬性限制未发起任何网络请求**（不 curl、不 urllib、不做新扫）。数据全部来自**本地 365 天缓存池** `candidates-2026-10-04.json`（**202 篇**，池内 `generated_at = 2026-10-04`，`fresh_sweep_status` 自记为「HTTP 429 (Rate exceeded.) on all 11 queries -> 0 rows added」）。**该池与第 4 期是同一份、未变化的文件**，本期也没有把它重新抓取。
- 因此本期报出的「新」**完全来自 seen-state 去重推进**（40 → 50 条），不是池内出现新论文。
- 池口径（实测）：`published` 跨度 **2025-10-03 → 2026-09-30**（= 本报告的真实有效窗口），`updated` 跨度 2025-10-07 → 2026-09-30；其中 `published ≥ 2026-09-01` 的近期投稿 **26 篇**。
- **CVF**：CVPR2026 本地索引 **4,042** 条（2026-10-02 缓存，本期只做离线匹配，未重下）。
- 策略冻结与运行健康：`selftest 18/18 passed`；`radar_filter.py 66877f5979fe` / `radar_keywords.py d405ccb11486` / `search_keywords.txt 4382dbe26daf` —— **与第 4 期三个哈希完全一致，运行期间未修改任何策略文件**，计数可与第 4 期直接比较。
- 排名回读校验（证据，非自报）：把 seen-state 回滚到本期推送前的 40 条，对同一 202 篇池重算两键排序 `(-relevance, -updated)`，**top-10 与本期实际推送的 10 篇完全一致（10/10）**。

## 本期要点

1. **本期是又一次「平局截断」**：入选 10 篇**全部相关度 84**；推送前 83 篇待推里 **12 篇并列 84**，两键排序取其中 **updated 最新的 10 篇**（2026-03-03 → 2025-11-10）。排名第 11/12 位**仍是 84**（`2510.07556` Label Semantics upd 2025-10-08、`2510.06098` Compact Multi-level-prior Tensor upd 2025-10-07），第 13 位才降到 82（82 档共 16 篇）。**截断发生在相关度平局内部，不是跨档降级，也不是漏筛**（设计预期）。
2. **C 组（超分+分类交叉项）连续第 5 期 0 篇 —— 本期无交叉项**；**D 组本期 0 篇**（④ 的两半都是 0）。
3. **结构：本期 10 篇 = 纯超分（A 组）4 篇 + 纯分类（B 组）6 篇。** 放回全池：123 篇过筛中 A **42** / B **59** / D **18**（D 内部：基础模型/预训练 **15**、仅适配 **2**、兼有 **1**）、C **0**；另有 **13 篇走 carve-out 通道入池**（pansharpening / multispectral / 高光谱融合类），**相关度为 0、不会进榜**——这是既定策略行为，不是漏筛。
4. **可复现性继续走低**：10 篇中 A（代码+数据）**0** / B（仅代码）**1** / C（未声明）**9**（第 4 期尚有 6 篇 B 档）。「高相关度 ⇄ 低开放度」的负相关在本期更明显，与首期宽窗口时的结论一致。
5. **同族重复投稿进了榜，值得注意**：本期同时入选 mHC 家族两篇 —— `2603.03418`（mHC-HSI）与 `2601.15757`（White-Box mHC），且前者的 arXiv `comment` 明写 **"text overlap with arXiv:2601.15757"**，而只有前者给了代码地址。另一例：本期 `2601.16602` 与第 4 期已推的 `2601.22755` 摘要都在用**死叶模型合成丰度**做超分——**去重只按 arXiv ID，不看内容相似度**（「同一研究线的两篇」为**推断**，arXiv ID 不同、作者信息池内未存，无法核实）。

## 筛选结果

## 高光谱筛选结果（365 天窗口 + 去重）

- 拉取候选 **202** 篇 → 通过关键词策略 **123** 篇 → 已推过（去重剔除）**40** 篇 → **本期新推 10 篇**（另有 73 篇通过但未进前十，留待后续）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C/D 关键词之一；pansharpening、multispectral 单独出现不算；SAR/雷达类无条件剔除
- 排序：与「超分+分类」方向的相关度（主）+ 更新时间（仅用于打破相近分数的平局），**不按投稿时间**

- 可复现性：**A（代码+数据）0 篇** / B（仅代码）1 篇 / C（未声明）9 篇　— 由摘要 + arXiv comment 判定，C 表示「未声明」而非核实不存在

| # | 标题 | arXiv | 相关度 | 更新时间 | 可复现性 |
|---|---|---|---|---|---|
| 1 | mHC-HSI: Clustering-Guided Hyper-Connection Mamba for Hyperspectral Image Classification | 2603.03418v1 | 84 | 2026-03-03 | B |
| 2 | VP-Hype: A Hybrid Mamba-Transformer Framework with Visual-Textual Prompting for Hyperspectral Image Classification | 2603.01174v1 | 84 | 2026-03-01 | C |
| 3 | DSXFormer: Dual-Pooling Spectral Squeeze-Expansion and Dynamic Context Attention Transformer for Hyperspectral Image Classification | 2602.01906v1 | 84 | 2026-02-02 | C |
| 4 | Unsupervised Super-Resolution of Hyperspectral Remote Sensing Images Using Fully Synthetic Training | 2601.16602v1 | 84 | 2026-01-23 | C |
| 5 | White-Box mHC: Electromagnetic Spectrum-Aware and Interpretable Stream Interactions for Hyperspectral Image Classification | 2601.15757v1 | 84 | 2026-01-22 | C |
| 6 | CLAReSNet: When Convolution Meets Latent Attention for Hyperspectral Image Classification | 2511.12346v2 | 84 | 2025-12-19 | C |
| 7 | A Dual-Domain Convolutional Network for Hyperspectral Single-Image Super-Resolution | 2512.09546v1 | 84 | 2025-12-10 | C |
| 8 | Enhancing Knowledge Transfer in Hyperspectral Image Classification via Cross-scene Knowledge Integration | 2512.08989v1 | 84 | 2025-12-08 | C |
| 9 | Hyperspectral Super-Resolution with Inter-Image Variability via Degradation-based Low-Rank and Residual Fusion Method | 2511.15052v1 | 84 | 2025-11-19 | C |
| 10 | GEWDiff: Geometric Enhanced Wavelet-based Diffusion Model for Hyperspectral Image super-resolution | 2511.07103v1 | 84 | 2025-11-10 | C |

**可复现性判定依据**

- 1. `B` — code: github.com/GSIL-UCalgary/mHC_HyperSpectral
- 2. `C` — 摘要与 comment 均未声明代码/数据
- 3. `C` — 摘要与 comment 均未声明代码/数据
- 4. `C` — 摘要与 comment 均未声明代码/数据
- 5. `C` — 摘要与 comment 均未声明代码/数据
- 6. `C` — 摘要与 comment 均未声明代码/数据
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

- **① 超分+下游任务联合优化（C 组）：0 篇** —— **本期无交叉项**（连续第 5 期）。
- **② 纯高光谱超分（A 组）：4 篇** —— `2601.16602`（无监督/全合成训练）、`2512.09546`（DDSRNet 双域）、`2511.15052`（DLRRF 解混式融合，处理 inter-image variability）、`2511.07103`（GEWDiff，AAAI 2026 已接收）。
- **③ 纯高光谱分类（B 组）：6 篇** —— `2603.03418`（mHC-HSI）、`2603.01174`（VP-Hype）、`2602.01906`（DSXFormer）、`2601.15757`（White-Box mHC）、`2511.12346v2`（CLAReSNet）、`2512.08989`（CKI 跨场景知识集成）。
- **④ 高光谱基础模型 / 高效微调（D 组，分两半）：0 篇**
  - **基础模型 / 预训练 / 表征学习：0 篇**
  - **高效微调 / 适配：0 篇**
  - 说明（来源事实）：池内 D 组共 18 篇（基础模型 15 / 仅适配 2 / 兼有 1），但相关度均低于 84，本期全部落在截断线之外，随后的每日期次会逐步推出。
- **⑤ benchmark / 数据集：0 篇**（本期无 benchmark 类进前 10；C 组亦为 0，故 `priority=1` 档本期为空）。
- **⑥ 其他高光谱：0 篇。**
- 计数口径（来源事实，回读脚本实测）：优先组分布为 ② 42 / ③ 58 / ④ 10 / ⑤ 9 / ⑥ 4 = 123，① 组 **0**；另有 **13 篇经 carve-out 入池但无 A/B/C/D 命中、相关度为 0**（这 13 篇即分布在 ⑤/⑥ 两档）。一个易混点：**B 组词形命中 59 篇 > 优先组 ③ 的 58 篇**，差额来自 `2604.26279`（同时命中 A 的 `spectral reconstruction` 与 B，按规则归入 ② 档，不重复计）。

## Top 3 精读（摘要级，未抓 PDF）

挑选说明：本期 6 分类 / 4 超分、C 与 D 组为空。Top 3 取「**唯一带代码入选者** + **唯一有会议接收状态的超分** + **与用户方向最贴的免 GT 超分**」，与第 4 期的 Top 3 不重复。

### 1. mHC-HSI: Clustering-Guided Hyper-Connection Mamba for Hyperspectral Image Classification
`2603.03418v1` · rel **84** · 更新 2026-03-03 · 可复现性 **B**（code: github.com/GSIL-UCalgary/mHC_HyperSpectral，HTTP 200 已验活）

- **问题**：DeepSeek 提出的 manifold-constrained hyper-connection（mHC）在通用深度模型上优于残差连接，但未针对 HSI 分类设计。
- **方法**：聚类引导的 mHC Mamba —— ①用聚类引导的 Mamba 模块同时学空间与光谱；②把 mHC 的**残差矩阵**实现为**软聚类隶属度图**（提升可解释性）；③按物理意义把光谱波段分组，作为 mHC 的「并行流」。
- **证据**：在 benchmark 数据集上与 SOTA 比较，称精度与可解释性双升（**摘要未给任何数值**）。
- **局限**：纯分类、无超分；**comment 是 arXiv admin note「text overlap with arXiv:2601.15757」**（本期同榜收录的另一篇 mHC 工作）——同一研究线的重复度需自行判断；无跨传感器验证；未报告参数量/延迟。
- **可延伸**：其「谱组作为并行流 + 软隶属度」天然能当超分网络的光谱先验（见选题 3），也是把分类侧结构迁移到超分侧的最低成本入口。

### 2. GEWDiff: Geometric Enhanced Wavelet-based Diffusion Model for Hyperspectral Image Super-resolution
`2511.07103v1` · rel **84** · 更新 2025-11-10 · 可复现性 **C**（未声明）· **`comment` = "This manuscript has been accepted for publication in AAAI 2026"**（来源事实）

- **问题**：高光谱维度过高难以直接喂扩散模型；通用生成模型不懂遥感地物的拓扑/几何结构；多数扩散在噪声层优化损失，收敛不直观。
- **方法**：①**小波编码-解码**把 HSI 压到 latent 且保留光谱-空间信息；②**几何增强的扩散过程**保持地物几何特征；③**多级损失**引导扩散、稳定收敛。目标为 **4× 超分**。
- **证据**：称在保真度、光谱精度、视觉真实感与清晰度多维度达 SOTA（**摘要未给数值**）。
- **局限**：**无代码/数据声明**；未报告推理步数、参数量、显存（扩散类超分最关键的部署成本）；未给跨传感器结果；摘要未量化「几何增强」的增益。
- **可延伸**：其小波 latent 是**插入轻量光谱通道再校准**的天然位置（选题 2）；AAAI 接收也意味着它会被后续工作频繁对比，值得早读。

### 3. Unsupervised Super-Resolution of Hyperspectral Remote Sensing Images Using Fully Synthetic Training
`2601.16602v1` · rel **84** · 更新 2026-01-23 · 可复现性 **C**（未声明）

- **问题**：主流 HSI 单图超分是**监督**的，需要高分 GT，而真实场景常常拿不到。
- **方法**：**无监督**训练策略 —— ①先把 HSI 解混成丰度与端元；②用**死叶模型**合成丰度图（刻意模仿真实丰度统计）；③**只用合成丰度**训练一个丰度超分网络；④推理时对真实 LR 丰度做超分，再与端元重组回高分 HSI。**训练全程不需要 HR 参考**。
- **证据**：实验显示合成图像具备训练价值且方法有效（**摘要未给 PSNR/SSIM 数值**）。
- **局限**：**强依赖解混质量**（解混差 → 合成分布偏）；无参考设定下 PSNR 类指标本身不可用（正是选题 1 要处理的问题）；未报告跨传感器泛化；大缩放因子下无监督方法普遍退化。
- **可延伸**：与第 4 期已推的 `2601.22755` 同属「合成丰度 + 死叶模型」路线（**推断**：同一研究线），两篇一起读能看清该路线的演进与未解决问题。

**另两篇值得单独看（未展开为 Top 3）**：`2603.01174` VP-Hype 在**仅 2% 训练样本**下声称 Salinas OA **99.69%**、Longkou **99.45%**（摘要给出数值，属强声明，建议自行核对实验设置）；`2512.08989` CKI 处理**标签空间不重叠**的完全异构跨场景迁移，并提出利用**目标域私有信息**，是分类侧少见的「非共类」设定。

## 3 个可做选题

### 选题 1：没有 HR GT 时，用什么评价超分？——用下游跨场景分类收益当无参考代理
- **Problem**：免 GT 的超分越来越多（`2601.16602` 训练不需要 HR 参考），但**没有 HR GT 时 PSNR/SSIM 无法使用**，超分质量失去可信度量；分类侧的跨场景工作（`2512.08989` CKI）只关心标签空间与目标域私有信息，把输入分辨率当作既定条件。两侧缺一个「超分有没有用」的判据。
- **Hypothesis**：在无标签目标域上，「超分→分类」的 OA/AA 提升可作为超分的**无参考代理指标**，且其排序与源域有参考的 PSNR/SAM 排序**秩相关 ρ > 0.7**。
- **Method sketch**：源域 LR HSI → 解混 → 合成丰度训练 SR（`2601.16602`）→ 重组 HR HSI；目标域无标签，仅用源域训练的冻结分类器推理，统计伪标签一致性与少量留出标注的 OA。对照：不超分 / 双三次上采样 / 监督超分（有 GT 上限）。
- **数据与指标**：Pavia University、Chikusei、WHU-Hi-LongKou + 跨传感器对（Pavia→Chikusei）；PSNR/SSIM/SAM/ERGAS（源域有参考）+ 目标域 OA/AA/Kappa；**代理指标与真值排序的 Spearman ρ**。
- **Baselines**：`2601.16602`（免 GT SR）、双三次、监督 SR（上限）、`2512.08989` CKI 分类器。
- **最小可证伪实验**：一对跨传感器、1% 目标域标注；若代理排序与 PSNR 排序 ρ < 0.4，或分类 OA 提升 < 1%，假设不成立。
- **Risk**：目标域小样本噪声大；增益可能来自单纯上采样而非 SR 质量（需双三次对照严格隔离）；**C 组连续 5 期为空本身就是该联结收益有限的反证信号**。

### 选题 2：把分类侧的廉价光谱再校准搬进生成式超分（DSX 块 → GEWDiff 小波 latent）
- **Problem**：生成式超分（扩散/小波 latent）空间保真强，但**高光谱的光谱保真缺少轻量约束**，4× 生成常带来光谱漂移；分类侧已有极低成本的光谱重标定（`2602.01906` 的 Dual-Pooling Spectral Squeeze-Expansion：global avg+max 双池化通道重标定 + Dynamic Context Attention）。
- **Hypothesis**：在 latent 中插入 dual-pooling 光谱挤压-激励块，可在 PSNR 下降 ≤ 0.05 dB 的代价内把 **SAM 改善 ≥ 5%**，并降低跨传感器退化。
- **Method sketch**：以 `2511.07103` 的小波编码-解码为骨架，在 latent 上加 DSX 式通道重标定（组内共享权重、组间独立），多级损失中加入 SAM 项；与 `2512.09546` 的双域 CNN（轻量对照）比较成本-精度。
- **数据与指标**：Chikusei、Pavia、4×；PSNR/SSIM/SAM/ERGAS + 参数量 + 单图延迟 + 显存；跨传感器（Pavia 训练、Chikusei 测试）。
- **Baselines**：`2511.07103` 原版（消融基线）、`2512.09546` DDSRNet、双三次。
- **最小可证伪实验**：单数据集单尺度，加块 vs 不加块，固定随机种子与扩散步数；SAM 改善 < 2% 即不成立。
- **Risk**：扩散采样成本高、复现成本大（原版无代码）；仅改 latent 易被质疑为工程 trick；必须公开采样步数与种子协议。

### 选题 3：用「物理谱组交互矩阵」当超分的光谱分组先验，治 inter-image variability
- **Problem**：HSI-MSI 融合受**光谱变异与局部空间变化**（inter-image variability）影响，现有方法直接对图像做变换，加剧病态性（`2511.15052`）；分类侧的 White-Box mHC（`2601.15757`）用**电磁谱分组 + 结构化定向交互矩阵**把谱组间交互显式参数化，并能可视化其空间模式。
- **Hypothesis**：用固定物理谱组（如 VIS/NIR/SWIR 分段）+ **结构化交互矩阵正则**约束超分网络的谱混合，可提升跨采集条件鲁棒性，且退化算子可解释（矩阵模式与谱变异性一致）。
- **Method sketch**：把 mHC 的谱组交互矩阵作为 SR 网络的谱混合算子（组间结构化、组内共享），替换/正则 `2511.15052` 的 DLRRF 低秩+残差分解中的退化建模；对照无结构混合版本。
- **数据与指标**：Pavia、Chikusei + 人为注入的谱变异；PSNR/SSIM/SAM/ERGAS + 退化估计误差 + 交互矩阵可视化的一致性检验。
- **Baselines**：`2511.15052` DLRRF、无分组结构消融、经典融合方法。
- **最小可证伪实验**：注入固定谱变异，加/不加结构先验对比；SAM 改善 < 3% 且矩阵无可解释模式即不成立。
- **Risk**：不同传感器波段定义不一，普适的「物理谱组」划分难统一；可解释性证据容易被质疑为事后可视化。

## 会议论文（CVPR2026，本地索引离线匹配）

- 本期入选 10 篇中，**0 篇**同时有 CVPR2026 版本（多为 2025-11 至 2026-03 的分类/超分 preprint，尚无会议版；本期唯一有接收状态的是 `2511.07103`，接收于 **AAAI 2026**，不在 CVF 索引内）。
- 放回全池口径：**202 个候选命中 5 篇**同时有 CVPR2026 版本（与第 4 期完全相同，池未变）——视频级压缩光谱重建、多光谱卫星→NASA 高光谱的光谱超分、抗光谱漂移的双门控 MoE、无配准 HSI 超分（解混丰度融合）、超表面快照相机（仪器类）。

| arXiv 候选标题 | 会议 | 匹配度 |
|---|---|---|
| Exploring Spatiotemporal Feature Propagation for Video-Level Compressive Spectral Reconstruction | CVPR2026 | 1.00 |
| Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization | CVPR2026 | 1.00 |
| Local Precise Refinement: A Dual-Gated Mixture-of-Experts against Spectral Shifts | CVPR2026 | 1.00 |
| Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning | CVPR2026 | 1.00 |
| MetaSpectra+: A Compact Broadband Metasurface Camera for Snapshot Hyperspectral+ Imaging | CVPR2026 | 1.00 |

- **会议新进榜（spotlight）：0 篇。** CVPR2026 seen-state 已于 2026-10-02 被消费（3 条），这是该模块的一次性设计，不是匹配失效。

## 排除说明

- 默认排除 SAR/雷达类：`UniDiff`（PEFT + 地物分类，与 CVPR 版同名）摘要含 **synthetic aperture radar**，被**无条件剔除**。
- 仪器/传感器类：`SpectralCA`（UAV 高光谱视觉）、`HAMscope`（快照自体荧光显微）、`Visible to Longwave-infrared imaging via an inverse-designed monolithic lens` —— 唯一话题证据是 spectral imaging，判为仪器排除。
- 门禁/话题未命中：`A UAV-Based VNIR Hyperspectral Benchmark Dataset for Landmine and UXO Detection`（有高光谱但未命中 A/B/C/D）、`SWAN`（自监督小波解混）、`DeepSalt`、`Raman Microspectroscopy`、`A Provably-Correct and Robust Convex Model for Smooth Separable NMF` 等。
- 门禁未满足：`AION-1`（天文全模态基础模型）、`Burst Image Quality Assessment` —— 未出现 hyperspectral/HSI。
- 边界情形（来源事实）：`2603.13352`（Dual-Gated MoE against Spectral Shifts）**通过 carve-out 通道入池但相关度为 0**，本期不会进榜；carve-out 只给「入场资格」，不给相关度。
- 本期排除清单与第 4 期同源（池未变、策略未变）；上述规则全部由 `search_keywords.txt` 单一真相源执行。

### 本期可复现（A/B 档，便于先跑）

- A（代码+数据）**0** 篇 ／ B（仅代码）**1** 篇 ／ C（未声明）9 篇

| 标题 | arXiv | 档 | 依据 |
|---|---|---|---|
| mHC-HSI: Clustering-Guided Hyper-Connection Mamba for Hyperspectral Image Classification | 2603.03418v1 | B | code: github.com/GSIL-UCalgary/mHC_HyperSpectral |

### 可跑的 baseline（本期论文提到的开源实现，已验活）

| 仓库 | 出处（arXiv ID） | HTTP |
|---|---|---|
| https://github.com/GSIL-UCalgary/mHC_HyperSpectral | 2603.03418v1 | ✅ 200 |

共 1 个仓库：**1 个可访问**（由 `radar_filter.py` 内置的 HTTP 校验实测，非自报）
