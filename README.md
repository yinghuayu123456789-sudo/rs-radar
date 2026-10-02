# 遥感研究雷达日报 · 2026-10-02（高光谱超分 / 高光谱学习专题）

**本期来源与时间窗口**：arXiv API（`export.arxiv.org/api/query`，`sortBy=submittedDate`，无日期约束抓取 + 客户端日期过滤），三次成功抓取共 32 次查询、去重后 1,963 条记录；窗口定为 **2026-09-25 ～ 2026-10-02**，但 arXiv 索引中新增高光谱论文的最新 `submittedDate` 为 **2026-09-30**（公告队列延迟），故本期有效窗口实际为 **2026-09-25 ～ 2026-09-30**。候选条目的标题/投稿日期用 `arxiv.org/abs/<id>` 页面逐一复核（17/17 一致）；开源仓库用 HTTP 状态码复核。**生成日期：2026-10-02（中国标准时间）**。上一期为 2026-10-01（窗口 09-24～10-01），本期标出「续报」的条目为窗口重叠所致，正文明确区分。

---

## 1. 本期要点（Executive summary）

- **窗口内高光谱相关新增仅 16 篇 new + 3 篇 updated-only，其中 2 篇为纯光谱仪器/光学论文被排除**——这是本期最需要如实说明的一点：本周期属于「小周」，且与上期窗口高度重叠（arXiv 索引最新日期只到 09-30）。高光谱超分主线本周**没有第二波新投稿**，仍是 OmniHSR / SSRON / SR²-Net 三条线（上期已报，本期标「续报」并补可执行细节）。
- **趋势转折信号：高光谱正在脱离「单帧图像」范式，走向视频 / 时序 / 非图像表示。** 本期三篇新工作同时出现：HyperDAM（高光谱视频目标跟踪，HOTC 2026 私评第 2 名）、INR for Hyperspectral Video Compression（WHISPERS 2026，BD-rate −88.88% 且下游跟踪 AUC +23.42%）、TITAnD v3（把 GPS 轨迹编码成 "Hyperspectral Trajectory Image" 的日×时刻双循环张量）。空间-光谱张量结构开始被当作**通用表示语言**，而不只是遥感影像的属性。**（推断）** 这是本期最值得押注的方向性变化。
- **EO 基础模型迎来「可复用性」诊断工具。** Reuse or Relearn?（ETH/UZH 组）用奇异子空间保持度、更新秩、更新幅度三项谱诊断量，发现 EO 模型微调时**保留的预训练结构远少于 CLIP/DINO**，且「预训练子空间被保留的地方，适配一小部分参数即可追平全量微调；没被保留的地方就会掉队」。这为 NE-LoRA 一类的星上 PEFT 提供了**先诊断再决定适配策略**的方法论，是上期「低标签/受限算力」线索的升级。
- **评测规范化的延续，并有可跑代码落地。** Hyperspectral Image Models 技术报告（统一 55 模型 / 24 场景，含带保护带的空间不重叠分块协议）已开源到 `github.com/Tanishq251/Hyperspectral-Image-Models`；本期另外两个新工作把评测推向未解决的评测盲区：PolyTopoBench（NeurIPS 2026 D&B，**带洞/多环复杂多边形**，11 个方法在建筑/道路/植被上集体退化）与 QSCP（查询引导的语义变化解析，支持同义词与「意图句子」提示，SECOND + WHU-CDC 跨数据集）。**（推断）** "现有方法在复杂几何/组合式查询上集体翻车"已成为一条可复用的选题模板。
- **高光谱分类的输入侧仍有未解决的坑**：Band-Selection Stability（WHISPERS 2026）在 Hyperspectral City V2 上用 10 组独立采样 ROI、6 种选带方法、60 个子集证明「**选带方法的稳定性与下游分割性能没有一致关联**」，K=9 时 mIoU +2.01、CPU 推理快 18–22×，但性能不随 K 单调。这意味着报选带结果必须报告重复采样方差，单次划分的 SOTA 不可信。

---

## 2. Ranked candidates（窗口 2026-09-25 ～ 2026-09-30）

评分 = 新颖性 / 技术深度 / 证据强度 / 可复现性 / 趋势信号 / 可迁移性 / 与用户方向（高光谱超分-分类）契合度 的综合（0–10）。「续报」= 上期已列，本期补充新信息，不重复计数。

| 排名 | 标题（arXiv 链接） | 来源 / 日期 | 任务 | 数据 / 模态 | 核心贡献 | 代码 / 数据 | 评分 | 为什么值得看 |
|---|---|---|---|---|---|---|---|---|
| 1 | [Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators](https://arxiv.org/abs/2609.39926)（OmniHSR） | arXiv cs.CV / 09-30（**续报**） | 高光谱超分（跨传感器、任意尺度） | HSI；ARAD 训练，6 个未见数据集测试 | 用**空间算子**替代逐波段卷积，0.538M 参数即在未见传感器上超过迁移基线，×2–×48 任意尺度 | 未声明（abs 页无仓库链接） | **9.2** | 直接命中跨传感器 + 任意尺度两大痛点，参数量比常规 SR 小 2–3 个数量级；**本期仍是高光谱超分最强的可复现起点** |
| 2 | [Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks](https://arxiv.org/abs/2609.35410)（SSRON） | arXiv cs.CV / 09-28（**续报**） | 光谱超分（RGB/MS → 连续光谱） | Sentinel-2 → EMIT；连续光谱场 | 残差算子网络回归**连续光谱场**而非离散波段值，支持零样本未见波段 | 未声明 | **8.8** | 与 OmniHSR 同源思路（算子 + 连续表示）但任务相反方向（空间→光谱），两篇合起来是「算子化 HSR」的完整拼图 |
| 3 | [Correcting Spectra Outside the Backbone: A Model-Agnostic Rectifier for Hyperspectral Image Super-Resolution](https://arxiv.org/abs/2601.21338)（SR²-Net，v2） | arXiv cs.CV / 首次 01-29，**09-28 更新至 v2**（续报） | 高光谱超分（光谱保真度校正） | HSI 多数据集 + 5 种主干 | 0.048M 参数的**即插即用光谱校正器**，置于主干之外，消除 22.6% 残余光谱误差 | 未声明 | **7.8** | v2 = 新实验；思路（把光谱保真度从主干解耦）可零成本加到你自己主干的输出端，性价比极高 |
| 4 | [HyperSAM: A Promptable Foundation Model for Hyperspectral Remote Sensing](https://arxiv.org/abs/2609.37340) | arXiv cs.CV / 09-29（**续报**） | 高光谱基础模型（可提示分割） | 合成高光谱立方体 → 真实 HSI（GRSM 接收） | 物理引导的丰度迁移合成全谱立方体 + **冻结 SAM3** 适配，主张合成数据优于扩大噪声监督 | 未声明 | **8.6** | 目前最完整的高光谱基础模型落地范式；其「合成 + 冻结 RGB 先验」配方可迁移到超分与解混 |
| 5 | [HyperDAM: Hyperspectral Distractor-Aware Memory with Amodal Expansion for SAM 3 Tracking](https://arxiv.org/abs/2609.34396) | arXiv cs.CV / 09-28（**新**） | 高光谱视频目标跟踪 | HOTC 2026 高光谱视频 + 新标注 | ①HOTC2026-Modal 人工帧级模态掩码/框；②帧零标定的 HSI 门控拒绝光谱不一致的记忆更新；③因果时空扩展器做仅外扩的 amodal 修正 | 标注贡献为主，未声明代码 | **7.4** | 冻结 SAM 家族 + 光谱门控的接口设计可搬到高光谱变化检测/解混；私评 68.01% AUC 说明光谱线索在跟踪上确有增益 |
| 6 | [Hyperspectral Image Models: Technical Report](https://arxiv.org/abs/2609.39871) | arXiv cs.CV / 09-30（**续报**） | 评测规范（分类等 24 场景） | 55 个模型 × 24 个高光谱场景 | 统一评测协议，含**带保护带的空间不重叠分块**，抑制空间泄漏；结论：场景难度主导，<1M 参数可追平大两个数量级的模型 | **开源**：[github.com/Tanishq251/Hyperspectral-Image-Models](https://github.com/Tanishq251/Hyperspectral-Image-Models)（已 HTTP 200 复核） | **8.5** | 本期唯一确认开源的高光谱基准；空间不重叠划分协议应直接替换你现有实验的随机划分 |
| 7 | [Reuse or Relearn? A Spectral View of Earth Observation Foundation Models](https://arxiv.org/abs/2609.32756) | arXiv cs.LG / 09-26（**新**） | 基础模型适配诊断 | EO 基础模型 vs CLIP/DINO | 三项谱诊断量（主子空间保持度、更新分布广度、更新幅度）：EO 模型微调更新**更大、秩更高、保留预训练结构更少**；子空间被保留处，少量参数适配即追平全量微调 | 未声明 | **8.2** | 给出「该 PEFT 还是该重学」的可计算判据；把「微调到底学到了什么」变成可测量问题，是本周期最有方法论价值的一篇 |
| 8 | [Implicit Neural Representation for Hyperspectral Video Compression](https://arxiv.org/abs/2609.31435) | arXiv cs.CV · **IEEE WHISPERS 2026** / 09-25（**新**） | 高光谱视频压缩 + 下游保持 | 高光谱视频（HOT2026） | 将 RGB 视频 INR 压缩扩展到高光谱，BD-PSNR +4.99 dB、BD-rate −88.88%；下游跟踪 AUC 最高 +23.42%、DP 最高 +35.56% | 未声明 | **7.2** | 首次把「压缩指标」和「下游任务指标」一起报告——为星上高光谱处理（与 NE-LoRA 同一条链路）提供压缩-精度权衡的评测范式 |
| 9 | [Label Less, Learn More: Resource-Efficient Active Semi-Supervised Learning for Onboard Satellite Image Annotation](https://arxiv.org/abs/2609.37481)（SatLabel） | arXiv cs.CV / 09-25（**新**） | 主动 + 半监督（星上标注/适配） | 11 个遥感数据集（核心/扩展/未见域） | 在模型不确定性×类不平衡×伪标签质量之间闭环采样；可选 MoE 学生 + 图特征精修；学生 11.2M/42.8MB vs RemoteCLIP 151.3M/577MB，GFLOPs 3.65 vs 5.89，吞吐 ~2× | 未声明 | **7.6** | 以 RemoteCLIP 零样本为对照组、并做未见域迁移，协议规范；「小模型 + 主动采样打败零样本大模型」的路线对你做低标签高光谱分类可直接照搬 |
| 10 | [Resource-Aware Parameter-Efficient Model Adaptation for Onboard High-Dimensional Data](https://arxiv.org/abs/2609.33687)（NE-LoRA） | arXiv cs.CV / 09-27（**续报**） | 星上 PEFT（高维光谱-空间输入） | 4 个高光谱数据集 × 3 种主干 | 低秩主分支 + **非线性辅助分支**双分支适配器 + 针对不同适配矩阵的非对称初始化/梯度差异化训练；以极小参数比例达到/超过全量微调 | 未声明 | **7.3** | 明确以 LEO 上行带宽为约束建模，是与第 8、7 条同一条「受限算力/受限带宽」链条；非线性分支可视为对标准 LoRA 的有效修正 |
| 11 | [QSCP: Beyond Class-Name Prompts for Query-Guided Semantic Change Parsing](https://arxiv.org/abs/2609.33088) | arXiv cs.CV / 09-27（**新**） | 查询引导语义变化解析 / 指代变化检测 | SECOND、WHU-CDC | 支持类名、同义词与**带意图的句子**查询，解析为 intent + 语义槽，双向视觉证据组合 + 查询条件解码器，输出配对的双时相语义图（而不仅二值掩码） | **开源**：[github.com/qianyuancs/QSCP](https://github.com/qianyuancs/QSCP)（已 HTTP 200 复核） | **7.5** | 把「变化检测」升级为「按需检索变化 + 说出变成了什么」；句子级查询与跨数据集一致性的评测设计，是多时相学习与遥感 VLM 的结合点 |
| 12 | [PolyTopoBench: A Benchmark for Complex Vector Polygon Generation from Remote Sensing Imagery](https://arxiv.org/abs/2609.32856) | arXiv cs.CV · **NeurIPS 2026（Evaluations & Datasets Track）** / 09-26（**新**） | 矢量多边形生成基准 | 2 个遥感数据集（建筑/道路/植被/裸地） | 统一评测框架，同时评外环与**内环**，横评 11 个方法（分割+后处理、视觉基础模型、专用矢量生成器）；现有方法在带洞/多环多边形上大幅退化 | **开源**：[github.com/seai-lab/PolyTopoBench](https://github.com/seai-lab/PolyTopoBench)（已 HTTP 200 复核） | **7.0** | 「光栅→矢量」比「类别 mIoU」更接近制图交付；拓扑感知是明确的未解问题，且基准已接收，投稿风险低 |

**其他入选但不入榜（详见第 6 节排除说明）**：自适应子空间建模（Functional Tucker Decomposition，09-25 v2，跨域高光谱分类，理论性重建误差界）、TITAnD 高光谱轨迹图像（09-28 v3，任务非遥感）、原型-规则神经符号正则（09-30，上期已列）、波段选择稳定性 WHISPERS 2026（09-25，上期已列，见要点 5）。

---

## 3. Top 3 精读

### 3.1 Reuse or Relearn? A Spectral View of Earth Observation Foundation Models（09-26，新）

- **核心问题**：下游精度无法回答「微调之后，模型是在**复用**预训练表示，还是**重新学**了一套？」——而这恰恰决定了一个 EO 基础模型是否值得在星上反复适配。
- **方法**：对适配前后的权重做谱诊断，量化三件事：(a) 主导奇异子空间的保持程度；(b) 权重更新分布的广度（有效秩）；(c) 更新幅度。以 CLIP / DINO 等自然图像模型为参照系。
- **证据（来源事实）**：在所评测的微调设置下，**EO 模型的更新幅度更大、秩更高、预训练结构保留更少**；且诊断量对「适配成本」有预测力——预训练子空间被保留的地方，只调一小部分参数就能追平全量微调，没保留的地方就落后。
- **局限**：摘要未给出具体数据集/模型清单与各诊断量的阈值，不能据此断言某个具体 EO 模型「不可复用」；诊断量本身是相关性的，未建立与下游收益的因果曲线。
- **可延伸**：① 把诊断量当作**多光谱/高光谱适配策略的路由器**（子空间保持度低 → 上 NE-LoRA 的非线性分支或重学光谱编码器）；② 「子空间保持度 → 达到全量微调精度所需参数比例」这条曲线可用高光谱超分/分类任务独立复现，是一条低算力、可独立成文的实验线；③ 对高光谱基础模型（HyperSAM 一类）重跑同一诊断，检验「合成数据预训练」是否比自然图像预训练更耐微调。

### 3.2 HyperDAM: Hyperspectral Distractor-Aware Memory with Amodal Expansion for SAM 3 Tracking（09-28，新）

- **核心问题**：高光谱视频提供**材质线索**（可区分伪彩外观相似的干扰目标），但现有基础模型跟踪器主要用空间与外观证据更新记忆——光谱信息没有被接进 foundation-model tracker 的状态更新里。
- **方法**：基于 DAM4SAM3 三个组件——(1) **HOTC2026-Modal**：给 HOTC 2026 全部 481 段视频补人工核验的帧级模态掩码与紧贴框；(2) **帧零标定的 HSI 门控**：拒绝光谱不一致的记忆更新，且不改变当前帧预测（拒更新 ≠ 改预测，这个解耦设计很干净）；(3) **因果时空扩展器**：在冻结 SAM 特征上做仅向外扩的 amodal 修正；另配静态场景恢复与空掩码 RTS 平滑处理目标切换/全遮挡。
- **证据（来源事实）**：HOTC 2026 组织方私有评测中排名第 2，AUC 68.0093%、DP@20 87.7703%；模型选择显式以跨域鲁棒性优先于榜单特化。
- **局限**：无代码/权重声明；方法高度围绕竞赛榜单工程化（作者自述以跨域鲁棒性优先，但未报告消融数值）；「门控拒更新」的阈值来自帧零标定，对光谱漂移（不同传感器/光照）的敏感性未知；模态标注数据集是否公开未说明。
- **可延伸**：① 「门控式记忆更新」可迁移到**多时相变化检测**的记忆/时序融合模块——用光谱一致性拒绝对应未发生变化的伪更新；② 帧零标定思想可用于跨传感器高光谱超分中的**逐景自适应**（只在一帧/一小块上标定，其余零样本）；③ 把 HOTC2026-Modal 作为高光谱视频理解的下游评测场，替代常见的单帧分类。

### 3.3 高光谱超分主线续报：OmniHSR + SSRON + SR²-Net v2（09-28 ～ 09-30）

- **核心问题**：超分要在**未见传感器、未见波段、任意尺度**上成立，而不是在固定传感器固定倍率的 benchmark 上刷分。
- **本期状态（来源事实）**：窗口内没有新的高光谱超分投稿；三篇已在榜的工作提供的是三种互补的「去传感器依赖」手法——
  - **OmniHSR**（09-30）：把逐波段卷积换成**空间算子**，0.538M 参数、仅用 ARAD 训练即在 6 个未见数据集上超过迁移基线，×2–×48 任意尺度；
  - **SSRON**（09-28）：残差算子网络回归**连续光谱场**，S2→EMIT 零样本未见波段；
  - **SR²-Net v2**（09-28 更新）：主干之外的 0.048M 参数光谱校正器，5 种主干通用，削减 22.6% 残余光谱误差。
- **证据**：均为作者自报的跨数据集结果，**三篇都未声明代码/权重**——这是本主线目前最大的可复现性缺口（与第 6 条基准的开源形成反差）。
- **局限（推断）**：ARAD 的退化仿真是否覆盖真实传感器 PSF/配准误差，摘要不足以判断；未见传感器评测仍以 PSNR/SAM 为主，缺少「跨传感器 + 下游分类」的联合验证；三篇对任意尺度的尺度因子集合不统一，横向比较需自建统一协议。
- **可延伸**：① 用 Hyperspectral Image Models 的空间不重叠协议 + 统一尺度集合，做 OmniHSR/SSRON/SR²-Net 的**首个独立横向复现**（本身即是可发表的工作量）；② 把 OmniHSR 的空间算子与 SSRON 的连续光谱场合并成「算子 + 连续波长条件」的单模型；③ 用 Reuse-or-Relearn 的谱诊断分析：跨传感器超分微调到底改动了哪些子空间（预期：光谱解码比空间主干改动更大）。

---

## 4. 三个可做的选题

### 选题 A：波长条件化的算子超分（Wavelength-Conditioned Operator SR）
- **Problem**：现有 HSR 要么绑定固定传感器/波段（迁移到未见传感器即崩），要么固定倍率；算子/连续场方法各自只解决一半（OmniHSR 管空间尺度，SSRON 管光谱轴）。
- **Hypothesis**：把「退化算子」与「波长条件」显式作为输入，单一模型可在未见传感器上同时获得任意空间尺度与任意波段输出，且零样本 SAM 误差显著低于分别迁移的两条基线。
- **Method sketch**：主干沿用空间算子的隐式核参数化（把卷积核作为坐标/波长的函数）；输入为 (LR 立方体, 目标波段中心波长向量, 空间尺度因子, 传感器响应函数估计)；训练用 ARAD 的多传感器仿真 + 波段随机遮罩，损失 = L1(重建) + 光谱角 + 算子正则。
- **数据与指标**：训练 ARAD；测试 Chikusei / Pavia / Houston / EMIT / Hyperion（跨传感器）；指标 PSNR、SAM、ERGAS、跨传感器 zero-shot SAM、尺度外推（训练 ×8 测 ×2/×48）+ 下游分类 OA。
- **Baselines**：OmniHSR、SSRON、SR²-Net + 通用 SR（SwinIR）、经典融合（CNMF/HySure）、逐传感器微调（上界）。
- **第一个最小可证伪实验**：ARAD 训练 → Chikusei 直接测试，仅改变波长条件向量；若 SAM 不优于 OmniHSR 复现基线，则「波长条件显式建模」假设被证伪。
- **Risk**：三篇基线无代码 → 需自实现，工作量与偏差风险高；传感器响应函数真实值难获取；跨传感器测试集的地面真值配准质量会污染指标。

### 选题 B：EO 基础模型的「可复用性」诊断用于高光谱适配策略选择
- **Problem**：星上/低算力场景下，无法靠试错决定「用 PEFT 还是重学光谱编码器」；Reuse-or-Relearn 只诊断了自然图像式 EO 模型，未覆盖高光谱与超分任务。
- **Hypothesis**：谱诊断量（子空间保持度、更新秩、更新幅度）能预测「达到全量微调精度所需的参数比例」，从而在训练前选出适配策略。
- **Method sketch**：对 3–5 个高光谱基础模型/预训练主干，在 {分类, 超分, 解混} 三类下游上分别做全量微调、LoRA、NE-LoRA 式双分支；记录诊断量与「参数-精度」曲线；拟合诊断量→最小参数比例的映射，并在留出任务上验证。
- **数据与指标**：Indian Pines / Pavia / Salinas / Botswana（分类，用空间分离折防泄漏）、Chikusei 或 ARAD（超分）、公开解混数据；指标 OA/Macro-F1、PSNR/SAM、达到全量微调精度所需可训练参数比例、GPU 吞吐。
- **Baselines**：全量微调、LoRA、NE-LoRA、只调 head、线性探测（frozen）。
- **第一个最小可证伪实验**：在 Indian Pines + Pavia 两个任务上计算子空间保持度，与「LoRA 达到全量微调精度所需 rank/参数比例」求相关；若 Spearman ρ < ~0.5，假设不成立。
- **Risk**：诊断量的实现细节（如何定义「主导子空间」）需自行设定，可比性存疑；高光谱数据规模小，微调差异可能被划分噪声掩盖（需多折重复，参考本期选带稳定性结论）；算力需求集中在多组全量微调上。

### 选题 C：压缩感知域内的高光谱时序下游推理（compress-and-infer）
- **Problem**：星上高光谱视频/时序受下行带宽限制，现行做法是先压缩、下行、解码、再推理；压缩误差与下游任务误差之间缺少可控的联合优化，且「解码」本身是可省的一步。
- **Hypothesis**：在 INR（隐式神经表示）域内直接接轻量下游头，可在同等比特率下同时取得更好的重建与更高的下游精度，且比特率–下游精度曲线优于 JP2K/PCA 基线。
- **Method sketch**：以 INR 表示高光谱时序（时间轴与光谱轴连续化），在表示上接小型 head 做变化检测/跟踪；训练目标 = 重建损失 + 下游损失（可加比特率约束的拉格朗日项）；对比「先解码再推理」的流水线。
- **数据与指标**：HOT2026 / HOTC 2026 高光谱视频（复用 HyperDAM 论文的下游跟踪指标）、多时相高光谱变化检测数据；指标 BD-rate、BD-PSNR、下游 AUC / DP@20 / F1，以及比特率–精度曲线下的面积。
- **Baselines**：JPEG2000 + PCA 逐帧压缩、RGB 视频 INR 扩展（INR 论文复现）、先解码后推理的独立 head。
- **第一个最小可证伪实验**：取 5 段 HOT2026 序列，在固定比特率下比较「INR 域内推理」与「解码后推理」的跟踪 AUC；若无优势，则联合优化假设被证伪。
- **Risk**：数据集获取与许可（HOTC/HOT 系列多为竞赛数据）；INR 训练成本高于传统编解码；「下游 head 在表示域内」可能只是变相过拟合到特定任务，需跨任务验证。

---

## 5. 下一步阅读队列

1. [Reuse or Relearn? A Spectral View of EO Foundation Models](https://arxiv.org/abs/2609.32756) — 先看诊断量的定义与实现细节，判断能否直接复用。
2. [Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators](https://arxiv.org/abs/2609.39926) + [SSRON](https://arxiv.org/abs/2609.35410) — 精读算子参数化与连续光谱场回归，评估合并成单选题目 A 的可行性。
3. [Hyperspectral Image Models: Technical Report](https://arxiv.org/abs/2609.39871) — 抄它的空间不重叠分块协议，替换现有实验划分。
4. [HyperDAM](https://arxiv.org/abs/2609.34396) + [INR for Hyperspectral Video Compression](https://arxiv.org/abs/2609.31435) — 高光谱视频这条新线的两个入口。
5. [PolyTopoBench](https://arxiv.org/abs/2609.32856)（NeurIPS 2026 D&B）— 看复杂多边形上 11 个方法的失效模式表，找可迁移的拓扑感知损失。
6. [QSCP](https://arxiv.org/abs/2609.33088) — 看句子级查询如何解析为语义槽，判断能否迁移到高光谱语义变化解析。
7. [Band-Selection Stability ... Hyperspectral City](https://arxiv.org/abs/2609.31074)（WHISPERS 2026）— 报告实验时如何做重复采样方差，避免单次划分结论。

---

## 6. 排除说明与来源说明

**被排除的高分候选（及原因）**

| 候选 | 日期 | 排除原因 |
|---|---|---|
| [Phase-resolved wide-field CARS microscopy with speckle illumination](https://arxiv.org/abs/2609.39730) | 09-30 | 纯光谱成像仪器/显微光学（physics.optics），无机器学习或地理空间角度 |
| [Scanless quantum Fourier-transform mid-infrared spectroscopy for solids and surface analysis](https://arxiv.org/abs/2609.37281) | 09-29 | 纯光谱硬件/量子计量（physics.optics, quant-ph），同上 |
| [Region-Local Copula Evidence Fusion for Heterogeneous Remote Sensing Change Detection](https://arxiv.org/abs/2609.32716) | 09-26 | 实验数据集为 Lake / UK（典型 SAR 变化检测基准），属 SAR / 异源跨模态变化检测，按默认规则排除；其「区域-局部依赖证据融合」的统计表述有一定跨模态可迁移性，若后续明确做光学-多光谱版本可重新入选（低优先级） |

**其他说明**：原型-规则神经符号正则（09-30）、波段选择稳定性（09-25）、NE-LoRA（09-27）、HyperSAM（09-29）、Hyperspectral Image Models（09-30）、OmniHSR（09-30）、SSRON（09-28）、SR²-Net（09-28 v2）在上期（10-01）已报道，本期按「不重复报道」原则不作新条目展开，仅标注续报状态与新增信息（OmniHSR/SSRON/SR²-Net 见 3.3，其余见要点）。**Functional Tucker Decomposition**（09-25 v2）与 **TITAnD 高光谱轨迹图像**（09-28 v3）列在备注：前者为张量函数分解理论 + 跨域高光谱分类，理论与用户方向相关但无代码、以重建误差界为主；后者「Highspectral Trajectory Image」是命名借用（日×时刻双循环网格），实际任务为 GPS 轨迹异常检测，非遥感高光谱，只作为趋势信号记录。

**本次实际使用的来源与局限（如实声明）**

- 已完成：arXiv API 三次抓取（sweep A 12 次查询含日期受限查询、sweep B 8 次无界查询 max_results 200–300、sweep C 8 次无界查询），去重 1,963 条记录；`arxiv.org/abs/<id>` 复核 17 篇（标题与日期 17/17 一致）；2 个 GitHub 仓库 HTTP 200。召回核对：无界的 `all:"hyperspectral"` 300 条记录覆盖 2026-01-18 ～ 2026-09-30，说明窗口内无遗漏。
- **未完成**：第四次针对不含 "hyperspectral" 字样的高光谱超分表述（如 `all:"multispectral" AND all:"hyperspectral"`、`all:"super-resolution" AND all:"multispectral"`）的补充抓取，被 arXiv 返回 **HTTP 429 / 503 限流**，多次重试（含 30 s 退避）均失败。因此**可能存在少量以 "multispectral/Sentinel-2" 表述、未含 hyperspectral 关键词的融合/超分新投稿未被覆盖**，下期优先补齐。
- **未检索**：Papers with Code、Hugging Face、CVPR/NeurIPS/WHISPERS 等会议日程页、EvalAI/Codalab 竞赛页；故本报告不对这些来源的活动作任何断言。
- **事实与推断的区分**：第 2 节表格中的「日期 / 任务 / 数据 / 贡献 / 开源状态」均来自 arXiv 官方元数据与摘要原文（来源事实）；标注「**（推断）**」处为基于本期多篇工作的趋势判断，非原文结论。评分是主观综合排序，不代表质量绝对量级。
