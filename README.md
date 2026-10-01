# 遥感研究雷达日报 · 2026-10-01

**本期来源与时间窗口**：arXiv API（`export.arxiv.org/api/query`）共 26 次查询（关键词检索 + `submittedDate:[202609240000 TO 202610012359]` 日期受限检索），时间窗口 **2026-09-24 ~ 2026-10-01（近 7 天）**，按高光谱超分 / 光谱超分 / pansharpening / 高光谱分类 / 解混 / 基础模型 / 光学遥感与非 SAR 对地观测为主线筛选；候选论文的标题与投稿日期已用 `arxiv.org/abs/<id>` 页面复核，声明开源的仓库已用 HTTP 状态码复核。本期为**首期运行，无上一期输出**可对比。未检索 Papers with Code / Hugging Face / 会议日程，故不作相关断言。

**生成日期**：2026-10-01（中国标准时间）

---

## 一、本期要点（Executive summary）

1. **高光谱超分（HSR）本期只有 2 篇真正的新投稿，但都指向同一条路线：算子/场式表示取代"直接预测光谱值"。** OmniHSR 预测"波段共享空间算子"并用连续算子场做任意尺度重建；SSRON 把光谱超分写成 DeepONet 式的"函数到函数"算子学习。两者都把"跨传感器 / 未见尺度 / 未见波段"当作一等公民，而不是靠目标域微调补救。
2. **光谱保真度正在从"主干内部"被解耦出来。** SR²-Net 用 0.048M 参数即插即用地校正主干输出（5 种主干平均减少 22.6% 残余光谱误差，2026-09-28 更新）。这与 OmniHSR/SSRON 的组合天然互补：算子场负责尺度与传感器泛化，整流器负责光谱形状。
3. **高光谱基础模型进入"合成数据 + 复用 RGB 先验"阶段。** HyperSAM（GRSM 接收）用物理引导的丰度迁移从 SpaceNet 多光谱合成全谱立方体、冻结 SAM3 图像分支做提示式分割；作者明确主张"高质量合成高光谱优于粗暴扩大噪声监督"。
4. **评测规范成为本期最强趋势信号。** 《Hyperspectral Image Models》技术报告统一 55 个模型、6 大范式、24 个场景（含 Mars CRISM），并提供带 Chebyshev 保护带的**空间不重叠分块**协议；其结论"场景难度主导架构、范式间平均只差 15 分、<1M 参数模型可追平大两个数量级的模型"直接挑战当前高光谱论文的对比方式。
5. **低标签 / 高效适配在本期密集出现**：NE-LoRA（星上 PEFT，带宽受限）、Prototype-Rule 神经符号正则（2–20 样本/类，空间分离折）、波段选择稳定性研究（K=9 时 mIoU +2.01、CPU 推理快 18–22×）共同指向"高光谱的算力/标注约束"而非单纯精度竞赛。

---

## 二、Ranked candidates（12 条，高光谱超分方向置顶）

| 排名 | 标题 | 来源/日期 | 任务 | 数据/模态 | 核心贡献 | 代码/数据 | 评分 | 为什么值得看 |
|---|---|---|---|---|---|---|---|---|
| 1 | [Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators (OmniHSR)](https://arxiv.org/abs/2609.39926) | arXiv cs.CV / 2026-09-30 新投 | 高光谱超分（跨传感器 + 任意尺度） | 高光谱；仅用 ARAD 训练，Pavia U / Chikusei 等 7 数据集评测 | 预测"波段共享的空间算子"而非光谱值：CSM 把任意波段数重采样到固定参考位置并由高斯支撑预测局部算子，COFR 组合成连续算子场实现任意尺度重建；0.538M 参数，无目标域数据/适配即在 6 个未见数据集上超过直接迁移基线，×2–×48 共 12 个尺度上 Pavia U/Chikusei 平均 PSNR +0.55 dB，推理最快 36× | 摘要称"代码即将公开" | **9.0** | 同时命中"跨传感器泛化"和"任意尺度"两个最难痛点，且模型极小、无需目标域适配，是本方向当前最值得复现的基线 |
| 2 | [HyperSAM: A Promptable Foundation Model for Hyperspectral Remote Sensing](https://arxiv.org/abs/2609.37340) | arXiv cs.CV / 2026-09-29，IEEE GRSM 接收 | 提示式高光谱基础模型（分类/异常检测/变化检测/目标检测等） | 合成全谱立方体（SpaceNet 多光谱 + 物理引导丰度迁移），HOTC 等真实高光谱下游 | 冻结 SAM3 RGB 图像分支 + 由 RGB ViT 初始化的可训练高光谱侧编码器 + ControlNet 式零初始化特征注入 + 轻量 MoE mask 精修；用 CromSS 式置信度选择加权噪声伪标签；论证高质量合成高光谱比扩大噪声监督更有效 | 摘要未给链接 | **8.5** | "复用 RGB 视觉基础模型 + 合成光谱数据"是目前最完整的落地范式，直接回答"高光谱基础模型能不能不从头训" |
| 3 | [Hyperspectral Image Models: Technical Report](https://arxiv.org/abs/2609.39871) | arXiv cs.CV / 2026-09-30 | 统一基准与模型库（分类为主） | 55 个模型 × 6 范式；24 个场景（Airborne / Spaceborne / UAV / Mars CRISM） | 统一注册表 + 自动 4D/5D 张量适配 + 标准评估；支持类别均衡随机划分与带 Chebyshev 保护带的**空间不重叠分块**以消除训练/测试像元重叠；1320 组"模型×场景"评估、6600 次种子运行，结论：场景难度主导、范式均值仅差约 15 分、<1M 参数模型可追平大两个数量级的架构 | **开源**（GitHub 已验证 200） | **8.5** | 直接解决高光谱社区"张量约定不统一、窗口重叠导致精度虚高"的顽疾，是现成可用的评测协议与对照表 |
| 4 | [Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks (SSRON)](https://arxiv.org/abs/2609.35410) | arXiv cs.CV / 2026-09-28，IGARSS 2026 | 光谱超分（MSI → HSI） | Sentinel-2A 类多光谱 → EMIT 高光谱 | 把光谱超分建为算子学习问题，用 Deep Operator Network 学习"降采样光谱 → 连续光谱"的函数到函数映射；所有指标优于基线，并对训练中未见波段做零样本超分，连续输出可外推到比原生传感器更细的波长间隔 | 摘要未声明 | **8.5** | "连续光谱输出 + 未见波段零样本"对跨传感器光谱重建与少样本高光谱生成都很有启发 |
| 5 | [Resource-Aware Parameter-Efficient Model Adaptation for Onboard High-Dimensional Data (NE-LoRA)](https://arxiv.org/abs/2609.33687) | arXiv cs.CV / 2026-09-27 | 星上高光谱模型高效适配（分类） | 4 个高光谱数据集 × 3 个主干 | 低秩主分支 + 非线性辅助分支，同时捕捉全局更新趋势与复杂光谱-空间变化；针对多矩阵适配器的差异化训练策略；仅更新很小比例参数即稳定超过 LoRA 基线，部分设置与全量微调相当甚至更优 | 摘要未声明 | **7.5** | 面向 LEO 上行带宽受限的真实部署约束，是"数据/带宽高效高光谱适配"的可用配方 |
| 6 | [Correcting Spectra Outside the Backbone: A Model-Agnostic Rectifier for HSI-SR (SR²-Net)](https://arxiv.org/abs/2601.21338) | arXiv cs.CV / 2026-01-29 首发，**2026-09-28 更新** | 高光谱超分（光谱保真后处理） | 高光谱；CNN / Transformer / 扩散共 5 种主干、30 个域内设置 | 与主干解耦的"增强—校正"整流器：H-S³A 强化跨波段交互，MCR 把校正限制在学习到的紧致光谱子空间，另加退化一致性约束；固定配置在全部报告设置中改善光谱保真度，30 个设置平均消除 22.6% 残余光谱误差，代价仅 0.048M 参数 | 摘要未声明 | **8.0** | 不与主干耦合、即插即用，可直接挂到你现有的任何 HSR 网络上做增益实验 |
| 7 | [Reuse or Relearn? A Spectral View of Earth Observation Foundation Models](https://arxiv.org/abs/2609.32756) | arXiv cs.LG / 2026-09-26 | 基础模型适配诊断（方法学） | EO 基础模型，CLIP / DINO 作自然图像对照 | 用谱诊断（主子空间保持度、权重更新的秩与幅度）区分"复用预训练表示"与"重学新表示"；结果显示 EO 模型在当前微调设置下更新更大更高秩、保留预训练结构显著更少；主子空间保留好时可只调少量参数即追平全量微调 | 摘要未声明 | **7.0** | 提供"高光谱/EO 基础模型的预训练先验到底用没用上"的可量化评估视角，能直接用于你的 PEFT 对比实验 |
| 8 | [Prototype-Rule Neurosymbolic Regularization for Rank-Constrained Tensor Neural Networks under Label Scarcity](https://arxiv.org/abs/2609.40131) | arXiv cs.LG / 2026-09-30 | 少样本高光谱分类 | Botswana / Indian Pines / Pavia University / Salinas；类支持预算 2–20 样本 | 为 Rank-R 张量学习引入可微原型-规则正则（推理端可选融合原型证据与 logits）；在**空间分离折**（缓解泄漏）下 Macro-F1 变化 +8.82（Botswana）/ +5.49（Indian Pines）/ +1.59（Pavia U）/ −0.62（Salinas），收益主要来自训练期正则 | 摘要未声明 | **6.5** | 少样本高光谱分类里少见的"空间分离折 + 支持预算曲线"严谨评测，方法简单易复现 |
| 9 | [Adaptive Subspace Modeling With Functional Tucker Decomposition](https://arxiv.org/abs/2603.25530) | arXiv stat.ML / 2026-03-26 首发，**2026-09-25 更新** | 张量/子空间建模，跨域高光谱分类 | 高光谱影像 + 多变量时间序列 | 把连续模态建模为 RKHS 中的函数（无需预设基），保留 Tucker 多线性子空间结构；给出"一个域上估计的子空间复用到另一个域"的重建误差界，为子空间迁移提供理论依据 | 摘要未声明 | **6.5** | 为"跨区域/跨传感器复用光谱子空间"提供理论支撑，可解释你在跨域实验里观察到的增益 |
| 10 | [Band-Selection Stability and Semantic Segmentation Performance: A Study on Hyperspectral City](https://arxiv.org/abs/2609.31074) | arXiv cs.CV / 2026-09-25，IEEE WHISPERS 2026 | 波段选择 + 高光谱语义分割 | Hyperspectral City V2（128 波段，450–950nm） | 6 种波段选择方法 × 10 组独立采样类均衡 ROI（60 个 top-25 子集）× 3 个分割模型；Top-K 在 K=9 时 mIoU 最高 +2.01、mF1 +1.72、CPU 推理快 18–22×，但性能随 K 非单调、稳定性与下游性能无一致关联 | 摘要未声明 | **6.0** | 给出"波段选择稳定性≠下游收益"的反面证据，对高效推理与波段精简方案是必要的风险提示 |
| 11 | [Implicit Neural Representation for Hyperspectral Video Compression](https://arxiv.org/abs/2609.31435) | arXiv cs.CV / 2026-09-25，IEEE WHISPERS 2026 | 高光谱视频压缩 | 高光谱视频（HOT2026 等） | RGB 视频压缩模型的 INR 扩展：相对逐帧传统高光谱压缩 BD-PSNR +4.99 dB、BD-rate −88.88%；并评测下游跟踪（低数据量下 AUC 最高 +23.42%、距离精度 +35.56%） | 摘要未声明 | **6.0** | "压缩后仍评估下游任务"的范式值得迁移到高光谱超分/分类的数据与部署管线 |
| 12 | [Aperture: Training-Free Multiscale Concept Bottlenecks for Remote Sensing](https://arxiv.org/abs/2609.38603) | arXiv cs.CV / 2026-09-29 | 可解释遥感识别（概念瓶颈） | 新数据集 SiFC（三国、人工审核类别概念图） | 免训练多尺度概念瓶颈：图像侧用贪心四叉树路由定位小目标概念，概念侧用预训练 MLLM 取代 CLIP 获取可靠概念分数，再融合全局与原生尺度概念分数；宏 F1 比最强免训练基线高 10 个百分点以上，并超过有监督概念瓶颈模型 | 摘要未声明 | **7.0** | 免训练 + 可解释 + 描述子更新无需重训，契合高光谱可交互解释与开放词汇应用路线 |

---

## 三、Top 3 精读

### 1. OmniHSR：把"超分"重写成算子场预测（9.0）
- **核心问题**：现有任意尺度 HSR 方法一旦换传感器或超出训练尺度范围，就需要额外数据与算力才能维持质量——即"跨传感器泛化"与"任意尺度"不能同时成立。
- **方法（来源事实）**：不预测光谱值，而预测**波段共享的空间算子**。Cross-Spectral Mapping (CSM) 把任意波段数的输入重采样到固定参考位置，用高斯支撑预测局部算子；Continuous Operator-Field Reconstruction (COFR) 把这些算子组合成连续场并作用到全部原始波段，从而支持任意尺度重建。
- **证据（来源事实）**：仅用 ARAD 训练、0.538M 参数即可在 6 个未见数据集上超过直接迁移基线，且不需要目标域训练数据或适配；×2 到 ×48 共 12 个上采样倍率下，Pavia U 与 Chikusei 平均 PSNR 比最强基线高 0.55 dB；相对最强的"从零训练/目标域适配"基线仍占优，推理最高快 36×；算子预测在全部 7 个数据集上优于直接预测光谱值。
- **局限（推断 + 可核查点）**：摘要未给出 SAM/ERGAS 等光谱保真度指标，"算子预测优于光谱值预测"是否同样带来光谱形状（SAM）优势需看论文；0.55 dB 的平均增益在部分倍率上可能不稳定；跨传感器评测集中在几个经典机载/星载数据集（Pavia U、Chikusei、ARAD），未覆盖 EnMAP/EMIT 等新传感器；代码尚未放出（摘要称"即将公开"）。
- **可延伸**：把算子场输出接到光谱保真整流器（SR²-Net 式 MCR）或直接以下游分类为监督；把"波段共享算子"思想用于跨传感器波段对齐（S2 ↔ EMIT ↔ EnMAP）；测试算子场在跨区域（不同大陆）时的稳定性。

### 2. HyperSAM：合成高光谱 + 冻结 RGB 基础模型的提示式范式（8.5）
- **核心问题**：高光谱缺少"高空间分辨率 + 可靠稠密标注"的大规模语料；同时大量高光谱模型几乎从头训练，浪费了现代视觉基础模型学到的几何与交互先验。
- **方法（来源事实）**：数据侧用物理引导的**丰度迁移生成器**从 SpaceNet 高分辨率多光谱合成全谱高光谱立方体，并用 SAM3 派生伪掩膜提供目标级监督；模型侧为冻结 SAM3 RGB 分支 + 由 RGB ViT 初始化的可训练高光谱侧编码器 + ControlNet 式零初始化特征注入 + 轻量 MoE mask 精修，配合 CromSS 式置信度选择应对噪声伪标签。
- **证据（来源事实）**：在分类、异常检测、变化检测、目标检测及机载溢油制图等多任务上报告强泛化；作者报告"高质量合成高光谱数据比单纯扩大噪声高光谱监督更有效"。已被 IEEE GRSM 接收。
- **局限**：期刊接收不代表全部细节可复现；摘要未给代码/数据链接，合成管线依赖 SpaceNet 与 SAM3 的可得性与许可；跨传感器泛化证据以任务泛化为主，未见明确的 leave-one-sensor-out 协议。
- **可延伸**：把合成数据管线用于**高光谱超分训练集扩充**（合成低分辨率-高分辨率谱对）；用 HyperSAM 的分割掩膜为超分提供区域级注意力；在其上验证 NE-LoRA/PEFT 的少样本适配。

### 3. Hyperspectral Image Models：把"评测"本身当作贡献（8.5）
- **核心问题**：高光谱深度学习横跨光谱-空间 CNN、ViT、Mamba、图网络、KAN、自监督掩码自编码，但仓库碎片化、张量约定互不兼容、评测不标准，导致精度常常被"窗口重叠"抬高。
- **方法（来源事实）**：统一注册表 + 自动 4D/5D 张量适配 + 标准化构造器，整合 55 个代表性模型（6 大范式）、24 个基准场景（机载、星载、UAV、火星 CRISM），支持缓存、标签重映射、PCA、显式波段选择或原始光谱、可选空间最大池化与任意 P×P 图块提取；提供类别均衡随机划分与带 Chebyshev 保护带的**空间不重叠区域分块**；单一 `config.yaml` + 确定种子 + 完整溯源，自动产出 LaTeX 基准表与分类图。
- **证据（来源事实）**：1320 组"模型×场景"评估、6600 次种子运行；平均精度从 Botswana 的 96.40% 到 Houston 2018 的 56.70%；场景难度主导，范式间均值仅差约 15 分；没有范式普遍占优；<1M 参数模型可匹配大两个数量级的架构。代码已在 GitHub 公开（本期已 HTTP 复核为 200）。
- **局限**：以分类任务为主，未覆盖超分/解混/检测；结论基于该库内的模型与配置选择，摘要中的"15 分差距"是范式均值，不能外推为"架构不重要"；对超大模型只做了有限采样。
- **可延伸**：直接采用其"空间不重叠分块"协议重跑你的 HSI 分类实验，量化重叠窗口带来的虚高；把该库当作 HSI-SR 的**下游评测器**（超分后分类精度）；用其配置网格做 PEFT 与神经符号正则的横向对比。

### 补充精读：高光谱超分的光谱保真线（SSRON 8.5 / SR²-Net 8.0）
- **SSRON**（[2609.35410](https://arxiv.org/abs/2609.35410)）把 MSI→HSI 光谱超分视为算子学习：DeepONet 学"降采样光谱 → 连续光谱"的映射，训练中未见波段可零样本预测，连续输出可外推到比传感器原生更细的波长间隔；训练对为 Sentinel-2A 类多光谱 → EMIT 高光谱，这对"用免费高频多光谱生成高光谱产品"的路线是关键证据（**注意**：EMIT 为星载成像光谱仪，非 SAR，符合本雷达范围）。
- **SR²-Net**（[2601.21338](https://arxiv.org/abs/2601.21338)，2026-09-28 更新）主张"光谱的低维结构属于数据、不属于主干"：一个整流器设计可服务任意主干，只吃主干输出、不改其内部，平均消除 22.6% 残余光谱误差、仅 0.048M 参数。
- **组合假设（本文推断）**：OmniHSR 负责尺度与传感器泛化，SSRON 提供连续光谱表示，SR²-Net 提供光谱形状约束——三者在"跨传感器 + 任意尺度 + 光谱保真"上互补，尚未有人报告联合方案。

---

## 四、三个可做的选题

### 选题 1：算子场高光谱超分 + 光谱保真约束的联合重建（跨传感器 / 任意尺度）
- **Problem**：现有 HSR 要么用光谱值回归（跨传感器差），要么只优化 PSNR/SSIM（光谱形状漂移，损害下游定量分析），且跨传感器与任意尺度不能兼得。
- **Hypothesis**：在波段共享算子场（OmniHSR 式）之上加入"紧致光谱子空间约束 + 退化一致性"（SR²-Net 式 MCR），可在不牺牲空间指标的前提下显著降低 SAM/ERGAS，并提升跨传感器零样本迁移的下游分类精度。
- **Method sketch**：CSM 重采样 → 局部算子预测 → 连续算子场重建；重建后接一个轻量整流头（分层光谱-空间注意力 + 子空间投影校正 + 低分辨率一致性损失）；训练目标 = 空间 L1/感知损失 + 光谱角 + 退化一致性；评测分两轨：合成下采样（可控）与真实跨传感器（ARAD 训练、Pavia/Chikusei/EMIT 测试）。
- **数据与指标**：ARAD、Pavia University、Chikusei、Indian Pines、Botswana、Houston 2013、EMIT/EnMAP（若可得）；指标 PSNR/SSIM + SAM/ERGAS + 下游 OA/AA/kappa/Macro-F1，另有参数量与推理时延。
- **Baselines**：OmniHSR、SSRON、SR²-Net、CNN/Transformer/扩散三类 HSR 主干、双三次插值。
- **第一个最小可证伪实验**：只用 ARAD 训练，在 Pavia U 上取一个**超出训练范围的尺度**（如 ×24），比较"纯算子场"与"算子场 + 整流头"的 SAM 与分类 OA；若 SAM 无改善或分类精度下降，假设即被否证。
- **Risk**：EMIT/EnMAP 下载与配准成本高；跨传感器波段不重叠会削弱零样本；0.55 dB 级别的空间增益可能被整流头抵消；算子场训练不稳定（高斯支撑尺度是敏感超参）。

### 选题 2：传感器无关的连续光谱超分与不确定性估计（S2 → EMIT/EnMAP）
- **Problem**：光谱超分本质不适定，多解性未被量化；现有方法给出点估计，无法告诉下游用户哪些波段/像元的预测可信。
- **Hypothesis**：在连续光谱算子学习框架上引入"波段级不确定性（预测区间/分位数）"，其区间宽度与真实误差强相关，且可用于**零样本未见波段**时的可靠度筛选；据不确定性加权能把下游（如作物分类）精度提升到与全监督相当。
- **Method sketch**：SSRON 式连续输出 + 多假设/分位数回归或轻量扩散先验；用真实传感器光谱（EMIT/EnMAP）校准；引入波长条件嵌入以支持任意查询波长；下游用不确定性阈值过滤低置信像元再分类。
- **数据与指标**：Sentinel-2 → EMIT 训练对；EnMAP / PRISMA 作未见传感器零样本测试；指标为逐波段 RMSE、SAM、连续区间的校准误差（ECE/覆盖率）、下游分类 OA 与选择性预测曲线（risk-coverage）。
- **Baselines**：SSRON、其他 MSI→HSI 光谱超分方法、直接波段插值 + 线性光谱解混。
- **第一个最小可证伪实验**：在 S2→EMIT 上训练，仅用 EnMAP 一个场景测试"未见传感器"的逐波段误差与校准误差；若区间覆盖率严重偏离标称值，假设被否证。
- **Risk**：跨传感器光谱响应函数与点扩散函数差异会造成系统偏差（需先做 S2/EMIT/EnMAP 的波段对齐）；不确定性建模会提高训练复杂度；真实高光谱数据获取与配对最难。

### 选题 3：高光谱基础模型的可复用性诊断 + 空间不重叠协议下的少样本适配
- **Problem**：高光谱/EO 基础模型微调后的收益，无法区分"复用了预训练先验"还是"重学了新表示"；同时社区广泛存在的重叠窗口划分让少样本结论不可比。
- **Hypothesis**：用谱诊断（主子空间保持度、更新秩/幅度）+ 空间不重叠划分，可预测 PEFT（LoRA/NE-LoRA）在哪些场景能追平全量微调；把"主子空间保留度"作为选择适配策略的可操作指标。
- **Method sketch**：取 Hyperspectral Image Models 库中的标准模型与 24 个场景；对每场景在"类别均衡随机划分"与"带保护带的空间不重叠分块"下各跑 full-FT / LoRA / NE-LoRA / 神经符号原型正则；同时计算适配前后的谱诊断曲线；分析(诊断指标 → 精度差)的相关性，并按支持样本预算 2–20 扫描。
- **数据与指标**：库内 24 场景（Botswana、Indian Pines、Pavia U、Houston 2018 等）；指标 OA/AA/kappa/Macro-F1 + 可训练参数比例 + 主子空间保留度 + 两种划分下的精度差。
- **Baselines**：全量微调、LoRA、HyperSAM 零样本/少样本、原型-规则正则（2609.40131）。
- **第一个最小可证伪实验**：选 2 个场景 × 1 个主干，比较"随机划分"与"空间不重叠划分"的精度落差，并测量 LoRA 与全量微调差距是否随"主子空间保留度"单调变化；若两者无相关性，假设被否证。
- **Risk**：算力开销（该库规模为千级模型-场景评估，需裁剪子集）；部分模型/权重未放出导致子集偏差；谱诊断指标本身需要论证其与任务精度的因果性；新意可能被"又一个基准研究"质疑，需要用诊断-适配的预测能力来立住贡献。

---

## 五、下一步阅读队列

1. **Hyperspectral Image Models**（先读其 GitHub 的划分协议与 `config.yaml`）：决定你后续实验的评测规范。[代码](https://github.com/Tanishq251/Hyperspectral-Image-Models) / [论文](https://arxiv.org/abs/2609.39871)
2. **OmniHSR**（等代码放出）：复现 0.538M 参数、跨传感器任意尺度的基线。[论文](https://arxiv.org/abs/2609.39926)
3. **HyperSAM**：合成高光谱管线与 SAM3 注入方式的实现细节。[论文](https://arxiv.org/abs/2609.37340)
4. **SSRON**：连续光谱算子学习的损失设计与 EMIT 配对细节。[论文](https://arxiv.org/abs/2609.35410)
5. **SR²-Net**：MCR 子空间约束与退化一致性约束的形式，作为即插即用模块。[论文](https://arxiv.org/abs/2601.21338)
6. **NE-LoRA**：星上 PEFT 的双分支与多矩阵训练策略。[论文](https://arxiv.org/abs/2609.33687)
7. **Reuse or Relearn?**：谱诊断的具体度量（子空间保持、更新秩）如何计算。[论文](https://arxiv.org/abs/2609.32756)
8. **Prototype-Rule 神经符号正则**：空间分离折与支持预算实验设计。[论文](https://arxiv.org/abs/2609.40131)
9. 交叉参考（非高光谱主线的 RS/CV 前沿）：[PolyTopoBench](https://arxiv.org/abs/2609.32856)（NeurIPS 2026 D&B，矢量多边形/拓扑评测）、[SatNav](https://arxiv.org/abs/2609.31507)（NeurIPS 2026 D&B，卫星影像长时程 VLN）、[HyperDAM](https://arxiv.org/abs/2609.34396)（SAM3 + 高光谱记忆，HOTC 2026 第二名）、[QSCP](https://arxiv.org/abs/2609.33088)（查询式语义变化解析）、[Cropland PAtteRNS](https://arxiv.org/abs/2609.38165)（时空谱三因子分解注意力，代码开源）。

---

## 六、排除说明与来源说明

**被排除的高分候选（及原因）**
- [2609.39730] *Phase-resolved wide-field CARS microscopy with speckle illumination*（physics.optics）：光谱硬件/显微成像，无 ML 或地理空间角度，按规则排除（关键词含 speckle）。
- [2609.37281] *Scanless quantum Fourier-transform mid-infrared spectroscopy*（physics.optics）：纯仪器与光谱测量，无 ML/地理空间角度。
- [2609.34954] *Toward Enhanced Water Detection in SWOT Pixel Clouds using Dynamic Graph Neural Networks*（physics.geo-ph）：SWOT 为 Ka 波段雷达高度计，属雷达/微波范畴，按默认排除规则排除（其图神经网络方法本身与 SAR 强绑定）。
- 名称含 "hyperspectral" 但与光谱影像无关：[2603.25255] *Hyperspectral Trajectory Image*（轨迹图像通道表征，非高光谱遥感数据）、[2609.39083] MRI 超分、[2609.37850]/[2609.37831] 视频超分、[2609.33582] Fill2SR 等通用/医学超分工作：不属于光学遥感或对地观测，未纳入榜单。
- 本期候选池共 48 条窗口内更新/新投稿、其中遥感相关 23 条、高光谱相关 14 条；榜单只保留 12 条，其余（如 *USAI-Quant* 定量推理基准、*Region-Local Copula* 变化检测、*Label Less, Learn More* 星上主动半监督、*Dual-Track Sentinel-2 小麦面积*）作为背景阅读未入榜。

**来源说明（如实声明）**
- 实际使用的来源：arXiv API（Atom XML），26 次查询分四轮执行（关键词轮 + 日期受限轮 + 扩展轮 + 字段对比轮），请求间隔 ≥3.5 秒；论文标题与投稿日期用 `arxiv.org/abs/<id>` 页面复核；开源声明用 HTTP 状态码复核（Hyperspectral-Image-Models、PolyTopoBench、QSCP、CroplandPAtteRNS 均返回 200）。
- 未使用的来源：Papers with Code、Hugging Face、GitHub 趋势、会议/工作坊日程、排行榜页面（本次未检索，故报告不对这些来源作任何断言）。
- **已知检索局限**：arXiv 日期受限检索显示本窗口内标题/摘要含 "hyperspectral" 的新投稿仅 13 篇、其中 8 篇为标题含该词——高光谱本身是小众方向，本期"高光谱超分"真正的新投稿只有 2 篇（OmniHSR、SSRON），另有 1 篇更新（SR²-Net）。若有论文使用了非标准术语（如仅在正文提 HSI-SR），可能未被捕获。
- 报告中的"来源事实"均来自摘要、comment 或已验证的页面；标注为"推断/假设"的内容为本文分析，未经原文实验确认。
