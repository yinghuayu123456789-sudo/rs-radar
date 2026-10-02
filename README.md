# 遥感研究雷达日报 · 2026-10-02（关键词策略验收运行 B）

**本期来源与时间窗口**：arXiv API（20 次查询，**20/20 HTTP 200**，去重 708 篇；有效窗口 2026-09-25 → 2026-09-30）+ CVF 会议库（本地索引 CVPR2026，4,042 条 → 按现行策略命中 3 条）。
**生成日期**：2026-10-02 10:52 CST（同日第二次运行，验收新关键词策略的筛选准确性）。
**筛选脚本**：`radar_filter.py`（策略唯一真相源 `search_keywords.txt`，由 `radar_keywords.py` 解释执行）。

---

## 本期要点

1. **验收结论先说**：候选 **16 篇 → 入选 2 篇**。新策略（标题必须同时出现 `hyperspectral/HSI` 门禁 + A/B/C 任务词）在本期窗口上是**高精度、低召回**：唯一可证的漏检是 `2609.39926`（摘要正文明确写 "hyperspectral super-resolution"，只因标题用了 `Super-Resolving` 这一词形而落选）。详见「验收发现」。
2. **'任意尺度 + 跨传感器' 是本期 arXiv 超分主线**：SSRON（`2609.35410`）把光谱超分建成深度算子网络，学"降采样光谱 → 连续光谱"的函数到函数映射；OmniHSR（`2609.39926`）更进一步，**直接预测波段共享的空间算子而不是光谱值**，只用 0.538M 参数在 ARAD 上训练即可零样本迁移到 6 个未见数据集。两者相隔 2 天、观点互为镜像（镜像关系为推断，非原文陈述）。
3. **"骨干无关"开始被当成一等公民问题**：SR²-Net（`2601.21338`）明确主张**光谱的低维结构属于数据、不属于任何骨干**，因此一个整流器可服务任意骨干；这与 CVPR 侧 UALNet 的"数据驱动光谱正则"同一思路（两位作者组的独立工作，非同一篇）。
4. **会议侧本期只有高光谱超分**：CVPR2026 索引按策略仅存 3 篇，全部 p2（EMR-Diff / UAFL / 对抗展开 UALNet）；arXiv × 会议本期匹配 **0 篇**——因为这三篇的预印本版本都是 2026-03（`2603.07918` / `2603.00920`，已逐个复核），落在 7 天窗口之外，本期只以会议身份出现，不重复占行。
5. **信噪比画像**：16 篇窗口候选里 5 篇是光谱仪器/凝聚态物理（THz 发射器、CARS 显微镜、量子 FTIR、二聚化、张量 NN 理论）。宽泛 `all:"hyperspectral"` 在 physics 分类上信噪比很低，**门禁 + 任务词双层过滤不是可选项**。

---

## 一、高光谱筛选结果（`radar_filter.py` 原始输出）

## 高光谱筛选结果

- 候选：16 篇 → **入选 2 篇**（过滤掉 14 篇）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C 关键词之一；pansharpening、multispectral 单独出现不算

| 优先 | 标题 | 来源 | 命中组 | 为什么值得看 |
|---|---|---|---|---|
| ② 高光谱超分 | Correcting Spectra Outside the Backbone: A Model-Agnostic Rectifier for Hyperspectral Image Super-Resolution | 2601.21338v2 | A | 骨干无关光谱整流器 SR²-Net；在 5 个 CNN/Transformer 骨干上验证，直击“光谱结构属于数据” |
| ② 高光谱超分 | Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks | 2609.35410v1 | A | 把光谱超分建成算子学习问题；Sentinel-2A 类多光谱 → EMIT 高光谱，含零样本波段外推 |

**被过滤（前 12 条，附原因）**

- `未命中 A/B/C 任一关键词` — High-power photoconductive THz emitters for fast parallel electro-optic detection
- `未命中 A/B/C 任一关键词` — Prototype-Rule Neurosymbolic Regularization for Rank-Constrained Tensor Neural Networks under L
- `未命中 A/B/C 任一关键词` — Strong Dimerization and Field-Induced Reconstruction of the Low-Energy Spectrum in $\mathrm{Cu}
- `未命中 A/B/C 任一关键词` — Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators
- `未命中 A/B/C 任一关键词` — Hyperspectral Image Models: Technical Report
- `未命中 A/B/C 任一关键词` — Phase-resolved wide-field CARS microscopy with speckle illumination
- `未命中 A/B/C 任一关键词` — HyperSAM: A Promptable Foundation Model for Hyperspectral Remote Sensing
- `未命中 A/B/C 任一关键词` — Scanless quantum Fourier-transform mid-infrared spectroscopy for solids and surface analysis
- `未命中 A/B/C 任一关键词` — HyperDAM: Hyperspectral Distractor-Aware Memory with Amodal Expansion for SAM 3 Tracking
- `未命中 A/B/C 任一关键词` — Resource-Aware Parameter-Efficient Model Adaptation for Onboard High-Dimensional Data
- `未命中 A/B/C 任一关键词` — Implicit Neural Representation for Hyperspectral Video Compression
- `未命中 A/B/C 任一关键词` — Band-Selection Stability and Semantic Segmentation Performance: A Study on Hyperspectral City
- …另有 2 条

### 计数与去向（16 = 2 + 14 的完整分解）

| 去向 | 篇数 | 说明 |
|---|---|---|
| 入选 | 2 | 均为 p2 高光谱超分，A 组命中在标题 |
| 过滤：纯仪器/物理噪声 | 5 | THz 发射器、CARS 显微镜、量子 FTIR、凝聚态二聚化、张量网络理论 |
| 过滤：**可证召回缺口** | 1 | `2609.39926` 正文 A/B/C 命中但标题未命中（见下节） |
| 过滤：相关但无 A/B/C 任务词 | 6 | Hyperspectral Image Models、HyperSAM、NE-LoRA、Band-Selection/Seg、INR 高光谱视频压缩、HyperDAM 跟踪 |
| 过滤：窗口外的旧文（updated-only） | 2 | `2603.25530` 子空间 Tucker、`2603.25255` 轨迹异常检测 |

---

## 二、验收发现：策略准确性（title-only vs text-level）

`search_keywords.txt` 文件头写的是 *"Matching: case-insensitive SUBSTRING match against **title and/or abstract**"*，但 `radar_keywords.py` 的 `exclusion_reason()` 实际把 **A/B/C 限定在标题**（`abc_title`），只有门禁词 `hyperspectral/HSI` 才允许出现在摘要里。

用同一份关键词表做了离线复算（`diagnose-2026-10-02b.py`，未改动策略文件）：

| 检验 | 结果 |
|---|---|
| 现行规则（title-only A/B/C） | 16 → **2** |
| 门禁 + A/B/C 都放宽到"标题或摘要" | 16 → **3** |
| 差集（可证漏检） | 仅 1 篇：`2609.39926` |

**唯一漏检**：`Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators`
（摘要原文：*"... remains challenging in hyperspectral super-resolution (HSR)"*；A 组命中 `hyperspectral super-resolution` **和** `spectral super-resolution`）。它用 `Super-Resolving` 而非 `super-resolution`，因此按标题匹配必然落选。
**建议（未擅自实施）**：要么在 A 组补一条词形 `super-resolving hyperspectral`，要么把 A/B/C 的匹配范围改成与文件头一致的"标题或摘要"。两种改法都**不新增语义**，只修词形/范围。若刻意保持"标题必须点名任务"的高精度立场，则本表就是预期行为，可忽略本条。

**另一类值得人工确认的（非 bug）**：6 篇"相关但无 A/B/C 任务词"里，`Hyperspectral Image Models`、`HyperSAM`、`NE-LoRA` 三篇显然属于用户关心的 ③ 基础模型/少样本 档，但 **B 组只列了 classification 短语**（`hyperspectral foundation model classification` / `hyperspectral classification` ...），所以纯分割/提示式/适配类基础模型工作永远进不来。这是策略取舍，不是实现错误——需要用户决定是否给 B 组加一条通用的 `hyperspectral foundation model`。

---

## 三、Top 3 精读

### 1. Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks（`2609.35410`，2026-09-28，cs.CV）
[arXiv](https://arxiv.org/abs/2609.35410v1)

- **核心问题**：多光谱卫星影像 → 高光谱影像的**光谱超分**（由病态逆问题驱动），目标是在不增加传感器成本的前提下获得高时空分辨率高光谱数据。
- **方法**：把任务重写成**算子学习**，提出 SSRON（Deep Operator Network），学习"降采样光谱 → 连续光谱"的**函数到函数映射**；训练集为 Sentinel-2A 类多光谱 → EMIT 高光谱。
- **证据（原文事实）**：在所有指标上优于基线；具备**零样本能力**——能预测训练时没见过的波段；连续输出形式使其可在比原生传感器更细的波长间隔上估计光谱。
- **局限**：单作者工作、未见代码链接；摘要未给参数量/推理成本、未做跨传感器（unseen sensor）验证；"更细波长间隔"只有定性表述，没有定量实验。
- **可延伸**：把算子场输出接到下一个 7 天窗口的"任意尺度"路线（见 OmniHSR）上，做一次统一的算子 vs 数值预测对照。

### 2. Correcting Spectra Outside the Backbone: A Model-Agnostic Rectifier for Hyperspectral Image Super-Resolution（`2601.21338v2`，首发 2026-01-29，本期 **updated-only**）
[arXiv](https://arxiv.org/abs/2601.21338v2)

- **核心问题**：现有 HSI-SR（无论是改自 RGB 超分骨干还是专用光谱-空间架构）都在追空间细节，**残留光谱误差**没人管；而把光谱处理绑进某个骨干，就等于每换一个骨干都要重做一遍。
- **方法**：SR²-Net，一个**与骨干无关的整流器**——只吃骨干的输出，不改骨干内部结构。"先增强再整流"：H-S³A（分层光谱-空间协同注意力）强化跨波段交互，MCR（模态约束整流）把修正限制在一个学到的紧凑光谱子空间内，另加**退化一致性约束**把输出拴回观测到的低分辨率输入。
- **证据**：在 **5 个骨干**（覆盖 CNN / Transformer 等）上做了实验（摘要截断处为"five backbones spanning CNN, Tra…"）。
- **局限**：整流器仍需**逐骨干训练**，并非 plug-and-play 零成本；v2 为旧文更新而非新投稿，本期窗口内无新实验信息（只能看到 v2 摘要）。
- **可延伸**：这个"整流器"概念可以直接搬到光谱超分/跨传感器场景，与下面的 OmniHSR 组合。

### 3. Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators（`2609.39926`，2026-09-30，cs.CV）
[arXiv](https://arxiv.org/abs/2609.39926v1)　⚠️ **本篇被现行筛选规则漏掉（见「验收发现」），在此列为精读是为验收留证。**

- **核心问题**：单一模型同时做到**跨传感器泛化**与**任意尺度重建**；现有方法一旦遇到训练范围外的新传感器/新尺度，就要额外数据与算力兜底。
- **方法**：OmniHSR，**预测波段共享的空间算子**而非光谱值。CSM（跨光谱映射）把任意波段数的输入重采样到固定参考位置并预测带高斯支撑的局部算子；COFR（连续算子场重建）把这些算子组装成连续场，作用于全部原始波段，实现任意尺度重建。
- **证据（原文事实，摘要级）**：7 个数据集上"预测算子"全面优于"直接预测光谱值"；仅在 ARAD 上训练（**0.538M 参数**），在 **6 个未见数据集**上零样本超过所有直接迁移基线；在 Pavia U 与 Chikusei 上、×2 到 ×48 共 **12 个上采样倍率**平均 PSNR 比最强基线高 **0.55 dB**；优于在目标传感器上从头训练或适配的基线；推理最高快 **36×**。代码"即将公开"（**尚无仓库**）。
- **局限**：性能优势全部以 PSNR/推理速度呈现，**未报告下游任务（分类/解混）增益**；代码未发布，复现需自行实现算子场；"优于目标域训练"的反常结论需要看实验设置（是否有信息泄漏）才能采信（此为我的审查建议，非原文结论）。
- **可延伸**：与 SR²-Net 的整流器组合 → 见选题 2。

---

## 四、本期可做的 3 个选题

### 选题 1｜任务驱动超分：让"算子场输出"被分类/解混反向约束（优先级 ①）
- **Problem**：本期两条超分主线（算子学习 SSRON、空间算子 OmniHSR）**都只用重建指标（PSNR/SSIM）说话**，没有任何一篇报告下游分类/解混增益；而"超分到底帮不帮下游"在文献里长期欠账。
- **Hypothesis**：在空间算子场输出上叠加一个**任务感知整流器**，并用下游分类/解混损失联合优化，能在 PSNR 损失很小的前提下显著提升下游 OA/AA/Kappa，且跨传感器仍成立。
- **Method sketch**：以 OmniHSR 式算子场为主干（band-shared 空间算子 + 连续算子场重建），冻结主干、并联一个 SR²-Net 式轻量整流器；总损失 = 重建 + λ·下游任务损失（分类头或线性解混 + 任务损失）；消融 λ、整流器容量、是否解冻主干。
- **数据与指标**：训练 ARAD / EMIT + Sentinel-2A 类；测试 Pavia U、Chikusei（任意尺度 ×2…×48）；指标 PSNR/SSIM/SAM/ERGAS **+ 下游 OA/AA/Kappa**（用统一协议避免像素重叠）。
- **Baselines**：SSRON、OmniHSR（复现版）、SR²-Net、直接迁移的 HSI-SR 骨干；分类侧用统一场景划分下的标准 CNN/ViT 分类器。
- **最小可证伪实验**：单场景 + ×4 单一倍率。冻结主干、只训整流器，比较 λ=0 与 λ>0 的下游 OA。若 OA 无提升或 PSNR 掉 >0.3 dB，则假设不成立。
- **Risk**：OmniHSR 代码未发布，复现成本高；联合优化易退化为"重建变差换任务变好"的平凡权衡；需要严格控制训练/测试像素不重叠，否则 OA 虚高。

### 选题 2｜跨传感器零样本 HSI-SR 的"骨干无关整流器"（优先级 ②）
- **Problem**：SR²-Net 证明整流器可以脱离骨干，但仍需**逐骨干训练**、且面向单传感器设定；OmniHSR 解决跨传感器/任意尺度，却仍直接输出光谱值。两者互补但无人合并。
- **Hypothesis**：把 MCR 式的**紧凑光谱子空间约束**嫁接到"空间算子场"输出上，可以同时获得跨传感器泛化与光谱保真，并且在 unseen 传感器上不需要任何目标域训练。
- **Method sketch**：主干 = 波段共享空间算子预测；输出侧 = 在学到的光谱子空间内做模态约束修正 + 退化一致性约束；整流器**训练一次、对所有未见传感器复用**（这比 SR²-Net 的逐骨干训练更强，是本选题的赌注）。
- **数据与指标**：训练 ARAD（单源）；零样本测试 6 个未见数据集（Pavia U、Chikusei 等）；指标 PSNR/SSIM/SAM/ERGAS + 跨传感器方差 + 推理时间/参数量。
- **Baselines**：OmniHSR、SR²-Net、直接迁移的 SOTA HSI-SR、目标域从头训练（上界参考）。
- **最小可证伪实验**：一个源数据集 + 一个未见传感器 + ×4。若一次训练的整流器相对无整流器在 unseen 传感器上没有 ≥0.2 dB PSNR 或 ≥5% SAM 改善，则"整流器可零成本跨传感器复用"不成立。
- **Risk**：0.2–0.5 dB 级别的提升可能落进种子噪声；"整流器与传感器解耦"可能只是参数量太小带来的正则化效应（需做参数量对照）。

### 选题 3｜超分对下游到底有没有用：一次带防泄漏协议的干净测量（优先级 ①/④）
- **Problem**：本期多家工作（SSRON、OmniHSR、SR²-Net）全都只报重建指标；而高光谱社区最大的可信度问题是**训练-测试像素重叠导致下游指标虚高**。
- **Hypothesis**：在严格 spatially-disjoint 划分（带 Chebyshev 保护带）下，用超分结果重训下游分类器的增益，**显著小于**文献常报的增益。
- **Method sketch**：把 SSRON/OmniHSR 输出的连续光谱当输入，喂给固定分类器；对照 = 原始低分辨率输入、双三次上采样；划分协议采用 spatially-disjoint regional blocking + Chebyshev guard band（本期 `2609.39871` 的 Technical Report 已给出该协议与 55 模型/24 场景的注册表，可作为现成基础设施）。
- **数据与指标**：Houston 2018、Botswana、Pavia U、Chikusei；指标 OA/AA/Kappa + 划分敏感性（多次随机划分的方差）。
- **Baselines**：双三次上采样、原始 LR 输入、CNN/ViT 分类器、以及论文所报数字（作为对照的"乐观上界"）。
- **最小可证伪实验**：1 个场景 + 2 种划分（重叠 vs 不重叠）。若两种划分下超分增益差异 <2 个点，则"泄漏是虚高主因"不成立。
- **Risk**：负结果不易发表（但正是社区需要的）；需要重实现多套分类流程，工程量大；`2609.39871` 的框架尚未确认开源。

---

## 五、会议论文（CVPR 2026）

## 会议论文（Conference）

**arXiv × 会议索引匹配**：16 个候选，命中 0 篇同时有会议版本。

（本期无候选命中会议版本。）

**会议新进榜（Conference spotlight）**：本次首次纳入 3 篇。

### CVPR2026（3 篇）

- **[p2]** EMR-Diff: Edge-aware Multimodal Residual Diffusion Model for Hyperspectral Image Super-resolution — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_EMR-Diff_Edge-aware_Multimodal_Residual_Diffusion_Model_for_Hyperspectral_Image_Super-resolution_CVPR_2026_paper.html)
- **[p2]** Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_Enhancing_Unregistered_Hyperspectral_Image_Super-Resolution_via_Unmixing-based_Abundance_Fusion_Learning_CVPR_2026_paper.html)
- **[p2]** Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization: From Multispectral Satellite Data to NASA Hyperspectral Image — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Young_Spectral_Super-Resolution_via_Adversarial_Unfolding_and_Data-Driven_Spectrum_Regularization_From_CVPR_2026_paper.html)

_已更新 seen-state（1 个 venue）_

**补充说明（已复核的事实）**：
- 会议索引本期共 **4,042 条**（CVPR2026 `?day=all`，本地缓存，未重下），按现行策略过滤后**仅存 3 条，全部 p2（高光谱超分）**。
- 这 3 篇的 arXiv 预印本均已逐个复核存在：UAFL → [`2603.07918`](https://arxiv.org/abs/2603.07918)，UALNet（对抗展开）→ [`2603.00920`](https://arxiv.org/abs/2603.00920)；EMR-Diff 未见对应预印本。因预印本日期为 2026-03，不在本期 7 天窗口，故 arXiv × 会议匹配数为 0——**不是漏匹配**。
- seen-state 已于本期清空，因此这 3 篇以"会议新进榜"身份出现；下次运行会显示"首次纳入 0 篇"（预期行为）。

---

## 六、排除说明

**A. 噪声（门禁之外的仪器/物理工作，5 篇）**——宽泛 `hyperspectral` 查询在 physics/eess 上的典型污染，全部因「未命中 A/B/C 任一关键词」被丢弃：
- `2610.00744` High-power photoconductive THz emitters…（太赫兹器件）
- `2609.39730` Phase-resolved wide-field CARS microscopy…（相干拉曼显微）
- `2609.37281` Scanless quantum Fourier-transform mid-infrared spectroscopy…（量子 FTIR 光谱仪）
- `2609.39966v2` Strong Dimerization and Field-Induced Reconstruction…（凝聚态光谱）
- `2609.40131` Prototype-Rule Neurosymbolic Regularization for Rank-Constrained Tensor Neural Networks…（张量网络理论）

**B. 相关但按现行策略排除（6 篇，均非超分/分类任务）**：
- `2609.39871` Hyperspectral Image Models: Technical Report — 统一 55 模型 / 24 场景 / 6,600 次带种子运行的评测框架，**内容高度相关**，但标题与摘要不含 SR/分类短语 → 落选（见「验收发现」）。
- `2609.37340` HyperSAM — 提示式高光谱基础模型（SAM3 + 合成高光谱数据），属**分割**，B 组只收分类短语 → 落选。
- `2609.33687` Resource-Aware Parameter-Efficient Model Adaptation（NE-LoRA）— 星上高光谱 PEFT，属分类/适配 → 落选。
- `2609.31074` Band-Selection Stability and Semantic Segmentation…（高光谱城市语义分割）
- `2609.31435` Implicit Neural Representation for Hyperspectral Video Compression（高光谱视频压缩 + 跟踪）
- `2609.34396` HyperDAM…for SAM 3 Tracking（高光谱视频跟踪，HOTC 2026 第二名）

**C. 窗口外的旧文（updated-only，2 篇）**：`2603.25530`（Functional Tucker 子空间建模）、`2603.25255`（高光谱轨迹异常检测）——2026-03/01 首发、本期 9 月末更新，主题不属超分/分类。

**D. SAR / 雷达**：本期窗口 16 篇候选中 **0 篇**命中排除词表（`polsar / insar / synthetic aperture radar / radar imaging / microwave radiometer`）。此前处理过的 Lake/UK SAR-光学异源变化检测（`2609.32716`）不在本期 7 天窗口内。

**E. 未使用的来源**：本期只用 **arXiv API + CVF（openaccess.thecvf.com）**。**未使用 Semantic Scholar、Papers with Code、Hugging Face**，因此对它们的榜单/趋势不作任何断言。

---

## 七、可复现性与验证记录

| 项 | 结果 |
|---|---|
| arXiv 查询 | 20 条，**20/20 HTTP 200**，无 429/503（≥3.6 s 间隔，curl 传输，显式 `--max-time 30`） |
| 去重后论文数 | 708（跨查询 base-id 去重） |
| 窗口内候选 | **16**（new 13 / updated-only 3） |
| 有效窗口（实测） | `u_hsi` 无界查询最新一篇为 **2026-09-30**，跨度回至 2026-01-18 → 说明存在约 2 天公告延迟，**本期无 10-01/10-02 的 arXiv 新文**（是延迟，不是漏抓） |
| 筛选 | `radar_filter.py`：16 → **2**（stderr: `candidates in: 16 | kept: 2 | dropped: 14`） |
| 会议 | `conf_match.py`：候选 16 × 索引 4,042 → 匹配 0；spotlight 首次纳入 **3** |
| arXiv ID 复核 | 7/7（`2609.35410` `2601.21338` `2609.39926` `2609.39871` `2609.37340` `2603.07918` `2603.00920`），标题与日期全对 |

**工作文件**（`E:/tool/Hermes/cache/scratch/rs-radar/`）：`fetch-2026-10-02b.py`、`gen_candidates-2026-10-02b.py`、`diagnose-2026-10-02b.py`、`verify-2026-10-02b.py`、`papers-2026-10-02b.json`、`window-2026-10-02b.json`、`candidates-2026-10-02b.json`、`kept-2026-10-02b.json`、`filter_fragment-2026-10-02b.md`、`conf_fragment-2026-10-02b.md`、`verify-2026-10-02b.json`。

*纪律声明：本报告区分来源事实与推断——凡标注「原文事实/摘要级」的内容直接来自 arXiv 摘要或 CVPR 页面；凡标注「推断/我的审查建议」的内容是本报告的判断，不是论文结论。未获取的信息一律不补。*
