# 遥感研究雷达日报 · 2026-10-02（高光谱超分 / 分类专题 · 正式第一期）

**本期来源与时间窗口**：arXiv API（`export.arxiv.org/api/query`，**`sortBy=relevance`**，`submittedDate:[202510030000 TO 202610022359]` 即 **365 天窗口**，每查询 `max_results=300`）— **31 次查询全部 HTTP 200**（话题查询 28 + 无界诊断查询 3），去重后 **202 篇**候选；补充来源 openaccess.thecvf.com（本地 CVPR2026 索引 4,042 条，本期只做离线匹配，未重下）。候选标题用 `arxiv.org/abs/<id>` 页面逐篇复核（**10/10 标题一致**）；开源仓库用 HTTP 状态码复核（**3/3 = 200**）。**生成日期：2026-10-02（中国标准时间）**。

**有效窗口说明（来源事实）**：窗口下界 2025-10-03，池内最早 `published` 恰为 **2025-10-03**；上界受 arXiv 公告队列延迟限制 —— 无界按日期排序的 `all:"hyperspectral"` 最新一条为 **2026-09-30**，故**本期实际有效窗口 = 2025-10-03 ～ 2026-09-30**。这不是漏抓，是公告延迟。

**去重口径**：本期使用**真实 seen-state**（`E:/tool/Hermes/cache/radar/arxiv_seen.json`，本期起始为空），按**裸 arXiv ID**（剥离 `vN`）去重；选中的 10 篇已写回该文件，明日起从剩余的**113 篇**里继续推。

---

## 1. 本期要点（Executive summary）

- **C 组（超分 × 下游任务联合优化）在 365 天窗口内是真空缺，不是筛选 bug。** 全池 202 篇里只有 **1 篇**命中任何 C 类词形 —— `2601.08807` *S3-CLIP: Video Super Resolution for Person-ReID*，且它不含高光谱门禁，被正确剔除（原因：`未出现 hyperspectral/HSI`）。C 组 7 个词形在本年度内没有任何高光谱论文命中。**这是本期最硬的一条结论，并直接构成选题一。**
- **A 组（纯超分）42 篇 vs B 组（纯分类）58 篇**（通过策略的 123 篇内部计数，两组可重叠）：这一年高光谱分类的投稿量约为超分的 1.4 倍。但超分那 42 篇的**技术重心明显偏向"光谱侧与无监督侧"**——RGB→HSI 光谱重建、物理引导的连续光谱场、无监督/自监督融合（Phy-CoSF、Radiative-Structured Neural Operator、Registration-Free Hyperspectral Reconstruction、Unsupervised SR with Full……），而不是继续卷空间 PSNR。
- **D 组出现"基础模型已到、适配层开始"的双层结构。** 池内 D 组 18 篇，其中既有模型/评测类（HyperFM、Hyperspectral Image Models Technical Report、HyperSAM），也有适配类（Cross-Domain Transfer of Hyperspectral Foundation Models、LESSViT、Spectral Gaps and Spatial Priors、Transfer learning RGB models to HSI、Resource-Aware PEFT / NE-LoRA）。本期入选前十的 2 篇 D 组论文都落在**基础模型/表征学习**一半，**高效微调/适配一半本期为 0 篇**（详见第 3 节 ④；NE-LoRA 等适配论文在池内但未进前十）。
- **可复现性依旧稀缺，且分布不均：本期 10 篇 A 档 0 篇、B 档 3 篇，且 3 篇全部是分类论文；入选的 3 篇超分论文一律未声明代码。** 这与上一期"最高相关度的论文最不开放"的信号一致 —— 相关度高 ≠ 能跑。
- **⚠️ 排序口径存在实测偏差，需要你定夺（我未改动任何文件）。** `radar_filter.py` 的排序分 = 相关度 + **上限 20 分**的新鲜度加分，而本池相关度区间是 72–99 分，所以"更新时间仅用于打破相近分数的平局"**在实现上并不成立**。实测后果：全池**相关度最高**的一篇 `2510.11576`（rel=99，*Benchmarking foundation models for hyperspectral image classification: Application to cereal crop type mapping*，2025-10-13 投稿）只能排到**第 24 名**（新鲜度加分仅 0.66）；按纯相关度排的话它与本期榜的重合度只有 **4/10**。详见第 11 节。

---

## 2. 筛选结果（四个计数 + 主榜）

**候选 202 篇 → 通过关键词策略 123 篇 → 已推过（去重剔除）0 篇 → 本期新推 10 篇**（另有 113 篇通过但未进前十，留待后续）。

- 过滤规则：标题或摘要需同时命中 `hyperspectral / hyper-spectral / HSI` 与 A/B/C/D 关键词之一；`pansharpening`、`multispectral` 单独出现不算（门禁满足时才作数）；SAR/雷达类无条件剔除。
- 排序：与「超分+分类」方向的相关度（主）+ 更新时间（仅用于打破相近分数的平局），**不按投稿时间**。
- 可复现性：**A（代码+数据）0 篇** / B（仅代码）3 篇 / C（未声明）7 篇 — 由摘要 + arXiv comment 判定，**C 表示「未声明」，不等于核实不存在**。

| # | 标题 | arXiv | 命中组 | 相关度 | 新鲜度 | 总分 | 可复现性 | 首次投稿 / 更新 |
|---|---|---|---|---|---|---|---|---|
| 1 | MBTI: A Multi-Branch Efficient Fine-Tuning Framework for Hyperspectral Image Classification with Foundation Models | 2607.12782v1 | B, D | 91 | 15.62 | 106.62 | B | 2026-07-14（new） |
| 2 | LegoQ: Density-Matrix Representation Learning with Spectral-Spatial State Transitions for Hyperspectral Classification | 2607.28970v1 | B, D | 89 | 16.55 | 105.55 | C | 2026-07-31（new） |
| 3 | Learning Spatial-Spectral Refinement and Calibrating Complementary Observations for Hyperspectral Image Super-Resolution | 2609.05303v1 | A | 86 | 18.47 | 104.47 | C | 2026-09-04（new） |
| 4 | Semi-Supervised Hyperspectral Image Classification with Edge-Aware Superpixel Label Propagation and Adaptive Pseudo-Labeling | 2601.18049v2 | B | 86 | 18.47 | 104.47 | C | 01-26 投 / **09-04 更新（updated-only）** |
| 5 | Correcting Spectra Outside the Backbone: A Model-Agnostic Rectifier for Hyperspectral Image Super-Resolution | 2601.21338v2 | A | 84 | 19.78 | 103.78 | C | 01-29 投 / **09-28 更新（updated-only）** |
| 6 | AGSA-Net: Abundance-Guided Self-Attention Network for Spectral Unmixing-Aware Hyperspectral Remote Sensing Image Classification | 2609.06359v1 | B | 84 | 18.58 | 102.58 | B | 2026-09-06（new） |
| 7 | High-Dimensional Noise to Low-Dimensional Manifolds: A Manifold-Space Diffusion Framework for Degraded Hyperspectral Image Classification | 2604.26279v1 | A, B | 91 | 11.45 | 102.45 | B | 2026-04-29（new） |
| 8 | Ten Architectures, One Error: Shared Failure Modes in Hyperspectral Classification under Spatially Disjoint Evaluation | 2609.01786v1 | B | 84 | 18.30 | 102.30 | C | 2026-09-01（new） |
| 9 | Graph-Based Semi-Supervised Hyperspectral Image Classification with Distance-Aware Spatial Measure | 2609.29367v1 | B | 82 | 19.56 | 101.56 | C | 2026-09-24（new） |
| 10 | Token Clustering and Semantic Sequence Mamba for Hyperspectral Image Classification | 2609.28580v1 | B | 82 | 19.51 | 101.51 | C | 2026-09-23（new） |

> 「命中组」按**标题＋摘要**匹配（不是只匹配标题）；`#1`/`#2`/`#7` 多组同时命中，说明它们同时具备分类主线与基础模型/超分信号。
> 第 10 名的切线为 **101.51**；紧随其后的 `2603.21911`（A Latent Representation Learning Framework for HSI Emulation，tot=101.41）以 **0.10 分**之差落榜。

**可复现性判定依据（逐篇可审计）**

- 1. `B` — code: `github.com/Azhenmiddleblock/MBTI/tree/main`（arXiv comment 原文：*The code will be available at ...*）
- 2. `C` — 摘要与 comment 均未声明代码/数据
- 3. `C` — 同上
- 4. `C` — 同上
- 5. `C` — 同上
- 6. `B` — code: `github.com/nnuvi/AGSA-Net`
- 7. `B` — code: `github.com/yangboxiang1207/MSDiff`
- 8. `C` — 摘要与 comment 均未声明代码/数据
- 9. `C` — 同上
- 10. `C` — 同上

**被过滤典型例子（附脚本给出的原因）**

| 候选 | 脚本判定原因 | 说明 |
|---|---|---|
| UniDiff: Parameter-Efficient Adaptation of Diffusion Models for Land Cover Classification … | `雷达/微波类：synthetic aperture radar` | 含 SAR 数据，按默认口径无条件剔除（尽管标题像 PEFT 主题） |
| MetaSpectra+: A Compact Broadband Metasurface Camera for Snapshot Hyperspectral+ Imaging（`2603.09116`，**CVPR2026**） | `纯传感器/仪器类（spectral imaging/metasurface），未命中 A/B/C/D` | 仪器/硬件设计 |
| Exploring Spatiotemporal Feature Propagation for Video-Level Compressive Spectral Reconstruction（`2603.00611`，**CVPR2026**） | `疑似光谱仪器/传感器（唯一话题证据是 spectral reconstruction，且出现 spectral imaging）` | 歧义词 `spectral reconstruction` 的守卫规则生效 |
| S3-CLIP: Video Super Resolution for Person-ReID（`2601.08807`） | `未出现 hyperspectral/HSI` | **全池唯一的 C 组命中**，但不含高光谱门禁 → C 组本期为 0 |
| A UAV-Based VNIR Hyperspectral Benchmark Dataset for Landmine and UXO Detection | `未命中 A/B/C/D 任一关键词` | 有门禁但没有 A/B/C/D 话题词（数据集类但词形是 benchmark 之外） |

---

## 3. 六档分组（① C → ② A → ③ B → ④ D → ⑤ benchmark → ⑥ 其他）

分组按 `radar_keywords.priority()` 的**组优先级**判定（C > A > B > D），因此同一篇可能命中多组，但只出现在其最高优先级档里。

- **① 超分 + 下游任务联合优化（C 组）：本期无交叉项（0 篇）。** 证据：202 篇池内仅 1 篇命中 C 类词形（`2601.08807`），且不含高光谱门禁 —— 这是 365 天窗口下的真实空白，不是窗口太窄。
- **② 高光谱超分（A 组，3 篇）**：`2609.05303`（TSR-ITNR，rel=86）／`2601.21338`（SR²-Net，rel=84）／`2604.26279`（Manifold-Space Diffusion，rel=91，同时属 B 组）。
- **③ 高光谱分类（B 组，7 篇）**：`2607.12782`、`2607.28970`、`2601.18049`、`2609.06359`、`2609.01786`、`2609.29367`、`2609.28580`。
- **④ 高光谱基础模型 / 表征学习（D 组，分两半列）**
  - **基础模型 / 预训练 / 表征学习（2 篇）**：`2607.12782` MBTI、`2607.28970` LegoQ —— 两篇同时命中 B 组，故也出现在 ③。
  - **高效微调 / 适配（D 子类，0 篇）**：_本期入选前十中无。_
  - 备注（透明化）：MBTI 其实是一篇**高效微调**论文（LoRA 多分支、仅 2.33–2.36% 可训练参数），但它的摘要命中 `hyperspectral foundation models` 短语而非 `hyperspectral adaptation` / `parameter-efficient hyperspectral`，所以被归到"基础模型"一半。归类的依据是词形，不是论文性质。
- **⑤ benchmark / 数据集：0 篇。**（池内 benchmark 类论文不少，如 `2510.11576`、`2603.04720`、`2605.21671` HyperBench、`2607.21050` HyperImageNet，但都没有进前十。）
- **⑥ 其他高光谱：0 篇。**

---

## 4. Top 3 精读（摘要级，未抓 PDF）

### 4.1 MBTI: A Multi-Branch Efficient Fine-Tuning Framework for Hyperspectral Image Classification with Foundation Models（`2607.12782v1`，07-14，B+D 组）

- **核心问题（来源事实）**：高光谱基础模型（HSFM）提供了"大规模无标注预训练 + 少量标注适配"的范式，但**不同传感器的波段配置差异巨大**，直接迁移困难；现有适配手段靠压缩 / 选择 / 重排光谱去迁就模型固定输入，会**丢光谱信息、破坏光谱连续性**。
- **方法**：① **保光谱连续性的多分支预处理** —— 把原始 HSI 切成多段连续光谱子集，余下波段用**波段复用**补齐，避免无效 padding 与光谱损失；② 每个分支插入**独立的 LoRA**，各光谱区间学各自的任务判别特征，预训练参数冻结；③ **多分支通道注意力融合**自适应重标定并整合各分支特征。
- **证据（来源事实）**：3 个公开高光谱数据集；rank-8 配置下**可训练参数仅约 2.33%–2.36%**；作者称与代表性分类方法相比"competitive and superior"。
- **局限**：摘要未给出逐数据集数值 / 消融，「competitive and superior」缺少数字；多分支意味着**推理要跑 N 次前向**，推理成本未报告；波段复用规则对不同波段数的传感器是否稳定未知；代码状态是 *"will be available"*（仓库已 200，但论文自身的可复现性仍属 B 档——代码声明在先、验证在后）。
- **可延伸**：① 把"波段复用 + 多分支 LoRA"接到**超分**主干上（当前 HSI-SR 同样受传感器波段数约束）；② 与 `2607.28970` 的密度矩阵头部组合，做"多分支 LoRA + 矩阵态分类头"的少样本适配；③ 报告**推理成本**（N 分支 vs 单分支）作为一等指标，这是 PEFT 论文普遍缺的一列。

### 4.2 LegoQ: Density-Matrix Representation Learning with Spectral-Spatial State Transitions for Hyperspectral Classification（`2607.28970v1`，07-31，B+D 组）

- **核心问题（来源事实）**：主流分类器把像素/图块编码成**确定性向量**再接 softmax 头，虽然判别有效，但**不直接暴露样本的混合度与不确定度** —— 而混元、类不平衡、标注少恰恰是高光谱分类的固有难点。
- **方法**：把光谱分组，每组映射为**半正定、Hermitian、迹归一化的密度矩阵态**；用可组合的**光谱 / 空间 / 组间转移**反复更新状态并投影回合法状态集合；最终不做扁平化，而是按 **Uhlmann fidelity** 与可学习的**类原型密度矩阵**比较；额外给出归一化本征谱、**von Neumann 熵**、纯度、原型保真度等**样本级诊断量**。
- **证据（来源事实）**：Indian Pines 十次运行 OA **96.20±0.70%**、AA **95.57±1.29%**、kappa **95.66±0.80%**；WHU-Hi-LongKou 十次运行最好 OA **97.52%**；作者明确说明**不需要量子硬件**。
- **局限**：十次运行报告的是 OA 方差，主实验仍是**随机划分**（没有像 `2609.01786` 那样用空间不重叠协议），跨传感器/跨场景泛化未验证；无代码；"矩阵态"的额外计算开销未报告；未与其他不确定性方法（证据深度学习、温度标定）做校准比较。
- **可延伸**：① 把 **von Neumann 熵当拒识 / OOD 分数**，在跨场景（source-free）设定下验证它是否优于 softmax 置信度 —— 这正是把"好看的诊断量"变成"可用的选择机制"；② 与 `2609.01786`（十种架构在空间不重叠划分下共同失效）交叉：矩阵态表征能否缓解该失效模式？③ 把密度矩阵状态从分类迁到**解混**（半正定 + 迹归一化天然对应丰度约束）。

### 4.3 Learning Spatial-Spectral Refinement and Calibrating Complementary Observations for Hyperspectral Image Super-Resolution（`2609.05303v1`，TSR-ITNR，09-04，A 组）

- **核心问题（来源事实）**：高光谱-多光谱融合（HMIF）要从 HR-MSI 取空间细节、从 LR-HSI 取光谱信息；现有 INR 类方法**对细粒度空间结构与光谱依赖刻画不足**，且 LR-HSI/HR-MSI 主要通过**退化一致性约束**进入模型，**互补信息利用不足**。
- **方法**：两阶段自监督框架 —— Stage 1 学**隐式 Tucker 表示**，精修低秩空间系数张量与光谱基，并用固定预训练去噪器提供深度先验；Stage 2 用**无参数校准**从两个观测分别导出互补且互不干扰的修正项。作者给出**理论分析**：光谱精修的几何保持性 + 校准项的正交互补性。
- **证据（来源事实）**：多个基准数据集上量化/视觉/光谱重建均强，且**不需要 HR-HSI 真值监督**；除常规重建指标外，**额外用下游语义分割精度**评估增益。
- **局限**：无代码（C 档）；摘要只给了"多基准"没有逐数据集数值，无法判断相对 SOTA 的幅度；"几何保持 / 正交互补"的理论结论在什么噪声与配准误差水平下成立未说明；下游分割用的是何种分割模型/协议未说明 —— 而"用下游任务评估超分"恰恰是本期最稀缺的证据类型。
- **可延伸**：① 它的"**无参数校准 + 两观测互补**"结构可以搬到**跨传感器**设定（把 LR-HSI 换成另一传感器的 HSI）；② 这是本期唯一**把下游任务指标（分割）与重建指标一起报告**的超分论文，值得当作评测协议模板；③ 与 `2601.21338`（骨干外光谱校正器）组合：一个是"校准观测"，一个是"校准光谱输出"，两者是否冗余值得做消融。

---

## 5. 三个可做的选题

### 选题一：超分对分类的**因果**增益（填 C 组的真空缺）
- **Problem**：365 天窗口内没有任何一篇把"超分"与"分类"联合优化/联合评估的高光谱论文（C 组 0 命中）。而 HSI-SR 普遍声称"有助于下游"，却几乎只报 PSNR/SAM —— 增益是相关性的，不是被证明的（`2609.05303` 是本期唯一例外，报了分割指标）。
- **Hypothesis**：超分带来的分类增益**主要来自光谱保真度的恢复而不是空间锐度的提升**；因此该增益可由超分后的 SAM / 光谱角变化预测，而不能由 PSNR 预测。
- **Method sketch**：固定一个分类器（如 `2607.12782` 的多分支 LoRA 或 `2607.28970` 的矩阵态头），对其输入施加三种超分：(a) 空间 SR、(b) 光谱 SR（RGB/MS→HSI）、(c) 联合；同时**控制重建误差预算**（同 PSNR 不同光谱误差）。用同一位点配对检验做因果分解，并做"把空间细节抹掉只留光谱恢复"的消融。
- **数据与指标**：Pavia / Indian Pines / Salinas / WHU-Hi-LongKou（分类，**空间不重叠折**，参考 `2609.01786` 的失效协议）；指标：分类 OA/Macro-F1、PSNR、SAM、ERGAS，以及 **PSNR 与 OA 的偏相关（控制 SAM）**。
- **Baselines**：双三次/Lanczos 上采样 + 分类器；`2609.05303` TSR-ITNR（无监督融合）；`2601.21338` SR²-Net（骨干外校正）；`2609.35410` 光谱超分算子网络。
- **最小可证伪实验**：在 Pavia + Indian Pines 上，构造两组同 PSNR 但 SAM 不同的超分结果，比较分类 OA；若 OA 差异不显著（配对检验 p>0.05），则"增益来自光谱保真"的假设被证伪。
- **Risk**：超分方法多数无代码（本期 3 篇超分全 C 档）→ 需自实现，偏差风险高；把 PSNR 对齐再比较是人为构造，需谨慎说明；小数据集上分类差异可能被划分噪声淹没（必须多折重复 + 报告方差）。

### 选题二：**骨干无关的光谱校正器**作为跨传感器超分的统一模块 + 首个独立横向复现
- **Problem**：跨传感器高光谱超分有一批"解耦光谱处理"的工作（`2601.21338` 的骨干外即插即用校正器、`2609.39926` 的共享空间算子、`2609.35410` 的连续光谱场算子），但**它们都无代码，且尺度集合、传感器集合、评测协议各不相同**，无法横向比较。
- **Hypothesis**：把"光谱校正"与"空间重建"彻底解耦（校正器只读主干输出、不改主干）后，单一校正器可在**未见传感器**上稳定迁移，且其增益可由"主干残余光谱误差"预测（即校正器是误差的补集算子）。
- **Method sketch**：以 3–5 个开源超分主干（SwinIR/HAT/Mamba-SR 等）为宿主；训练一个 0.05M 量级的校正器（光谱低秩 + 保几何约束）；在 ARAD 多传感器仿真上训练、在未见传感器上零样本测试；显式报告"主干残余光谱误差 vs 校正器增益"的曲线。
- **数据与指标**：ARAD（训练）/ Chikusei、Pavia、Houston、EMIT（测试）；指标 PSNR、SAM、ERGAS、跨传感器 zero-shot SAM；**统一尺度集合 ×2/×4/×8/×16/×48**。
- **Baselines**：纯主干（无校正器，上界/下界对照）；`2601.21338` 复现；逐传感器微调（性能上界）；CNMF/HySure（经典融合）。
- **最小可证伪实验**：用一个主干 + 一个校正器，在 ARAD 训练后直接测 Chikusei；若 SAM 相对纯主干无统计显著改善，则"解耦校正可跨传感器迁移"假设被证伪。
- **Risk**：ARAD 的退化仿真是否覆盖真实传感器 PSF/配准误差，摘要不足以判断；横向复现三篇无代码方法的工作量很大，可能变成"工程复现"而新颖性不足 —— **这恰恰是本选题的机会：可复现性本身是本期全池的稀缺资源（A 档 0 篇）**。

### 选题三：密度矩阵表征的**熵**作为少样本/跨域分类的拒识与选择信号
- **Problem**：少样本/跨域高光谱分类（`2601.22581` Cross-Domain Few-Shot、`2608.05964` Source-Free Cross-Scene）普遍用 softmax 置信度做伪标签筛选，而 softmax 在分布偏移下校准很差。`2607.28970` 已经证明密度矩阵态能给出 von Neumann 熵、纯度、原型保真度等**样本级诊断量**，但只当"可解释性副产品"报告，没有当决策变量用。
- **Hypothesis**：密度矩阵的 von Neumann 熵与原型保真度构成比 softmax 置信度更好的**跨域不确定性分数**，用于拒识与伪标签筛选时，能在 source-free 跨场景设定下提升 Macro-F1 并降低负迁移。
- **Method sketch**：复现/自实现矩阵态分类头；在源域训练，目标域做 (a) 直接推理、(b) 熵阈值拒识、(c) 熵排序选取伪标签自训练；把熵 / 纯度 / 原型保真度分别与 softmax 置信度、MC-dropout、证据深度学习做校准比较（ECE、AURC、风险-覆盖曲线）。
- **数据与指标**：跨场景配对（Pavia→Pavia University、Indian Pines→Salinas、WHU-Hi 系列）；指标 OA、Macro-F1、ECE、AURC、风险-覆盖率曲线下面积、拒识率-精度曲线。
- **Baselines**：softmax 置信度、温度标定、MC-dropout、证据深度学习（EDL）、`2601.22581` 的跨域少样本方法、`2608.05964` 的拓扑感知邻域学习。
- **最小可证伪实验**：单个跨场景配对（Pavia→PaviaU）上比较熵阈值与 softmax 阈值的 AURC；若 AURC 无改善，假设被证伪。
- **Risk**：矩阵态分类头无代码 → 自实现引入偏差；熵分数的绝对尺度依赖迹归一化与分组方式，跨数据集可比性需谨慎；小数据集的校准指标方差大，需多次划分。

---

## 6. 会议论文（CVF / CVPR2026）

**arXiv × 会议索引匹配**：202 个候选，命中 **5 篇**同时有 CVPR2026 版本。

| arXiv 候选标题 | 会议 | 匹配度 | 会议页 |
|---|---|---|---|
| Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization: From Multispectral Satellite Data to NASA Hyperspectral Image | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Young_Spectral_Super-Resolution_via_Adversarial_Unfolding_and_Data-Driven_Spectrum_Regularization_From_CVPR_2026_paper.html) |
| Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_Enhancing_Unregistered_Hyperspectral_Image_Super-Resolution_via_Unmixing-based_Abundance_Fusion_Learning_CVPR_2026_paper.html) |
| Local Precise Refinement: A Dual-Gated Mixture-of-Experts for Enhancing Foundation Model Generalization against Spectral Shifts | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Chen_Local_Precise_Refinement_A_Dual-Gated_Mixture-of-Experts_for_Enhancing_Foundation_Model_CVPR_2026_paper.html) |
| Exploring Spatiotemporal Feature Propagation for Video-Level Compressive Spectral Reconstruction: Dataset, Model and Benchmark（脚本按仪器类剔除） | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Cai_Exploring_Spatiotemporal_Feature_Propagation_for_Video-Level_Compressive_Spectral_Reconstruction_Dataset_CVPR_2026_paper.html) |
| MetaSpectra+: A Compact Broadband Metasurface Camera for Snapshot Hyperspectral+ Imaging（脚本按仪器类剔除） | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Liu_MetaSpectra_A_Compact_Broadband_Metasurface_Camera_for_Snapshot_Hyperspectral_Imaging_CVPR_2026_paper.html) |

**本期入选的 10 篇中，没有一篇有会议版本。** 5 篇匹配项在相关度排序中的位置（实测）：`2603.07918` 第 44 名（rel=86，tot=94.66）、`2603.00920` 第 78 名（rel=80，tot=88.22）、`2603.13352` 第 118 名（rel=0，靠 `multispectral` 宽免入池，tot=9.64），另 2 篇被仪器类规则剔除。**（推断）** 会议论文在这场 365 天窗口的竞争里并不占优，因为它们普遍是年初（2026-03）投稿，新鲜度加分只有 8–10 分，被 5–9 月的新论文挤掉。

**会议新进榜（spotlight）：本次首次纳入 0 篇。** 原因已查实：CVPR2026 的本地索引（4,042 条）经策略筛出 3 条高光谱条目，其 seen-state 已在**同日更早的运行中被消费**，所以现在重跑必然是 0 —— 这是 `conf_match.py` 的"一次性 spotlight"设计，不是匹配器失效。3 条已收录条目（供查考）：Enhancing Unregistered HSI-SR via Unmixing-based Abundance Fusion Learning / Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization / EMR-Diff: Edge-aware Multimodal Residual Diffusion Model for Hyperspectral Image Super-resolution。

---

## 7. 排除说明与来源局限

**被排除的典型候选（及原因）** 见第 2 节表格（UniDiff=含 SAR；MetaSpectra+ / 2603.00611=仪器类；S3-CLIP=无高光谱门禁）。

**关于 C 组为空的口径声明**：C 组 0 篇是**真实空缺**，不是筛选器缺失。判定依据是全池扫描：202 篇里唯一命中 C 类词形的 `2601.08807`（*Video Super Resolution for Person-ReID*）明确不含 `hyperspectral/HSI`，被门禁正确剔除。C 组 7 个词形在 365 天内没有高光谱论文命中。

**本期实际使用的来源与未做的事（如实声明）**
- 已完成：arXiv API **31 次查询全部 HTTP 200**（28 次 A/B/C/D 话题查询 + 3 次无界诊断查询；`sortBy=relevance`，`max_results=300`，请求间隔 ≥3.6 s），去重 202 篇；`arxiv.org/abs/<id>` 复核 10 篇（标题 10/10 一致）；3 个开源仓库 HTTP 复核（3/3 = 200）。召回核对：无界按日期排序的 `all:"hyperspectral"` 300 条覆盖 2026-01-18 ～ 2026-09-30（最新一条 09-30 = 公告延迟 2 天）；无界 `all:"hyperspectral" AND all:"super-resolution"` 全时段仅 154 条，其中 36 条落在本窗口内 → 说明窗口已覆盖到该主题的全量。
- **未使用**：Semantic Scholar（本期无需 discovery 检索）、Papers with Code、Hugging Face、EvalAI/Codalab、以及任何竞赛/日程页 —— 因此本报告**不对这些来源的活动作任何断言**。
- **未抓 PDF**：按要求只做摘要级分析；第 4 节的数值全部来自摘要原文。
- **事实与推断的区分**：第 2/3/4 节的"日期 / 任务 / 数据 / 贡献 / 开源状态 / 数值"均为 arXiv 官方元数据与摘要原文（来源事实）；标「**（推断）**」处为基于多篇工作的趋势判断。相关度分是筛选脚本的规则打分，不等于质量。

**运行一致性**：本期运行期间未改动任何脚本或关键词文件。运行开始时（14:39）冻结的策略哈希为
`radar_filter.py 037b5b9fb17c` / `radar_keywords.py d405ccb11486` / `search_keywords.txt 4382dbe26daf`（`search_keywords.txt` 自上一轮起未变），`radar_filter.py --selftest` **18/18 通过**。

---

## 8. 本期可复现（A/B 档，便于先跑）

- A（代码+数据）**0** 篇 ／ B（仅代码）**3** 篇 ／ C（未声明）**7** 篇

| 标题 | arXiv | 档 | 依据 |
|---|---|---|---|
| MBTI: A Multi-Branch Efficient Fine-Tuning Framework for Hyperspectral Image Classification with Foundation Models | 2607.12782v1 | B | code: `github.com/Azhenmiddleblock/MBTI/tree/main` |
| AGSA-Net: Abundance-Guided Self-Attention Network for Spectral Unmixing-Aware Hyperspectral Remote Sensing Image Classification | 2609.06359v1 | B | code: `github.com/nnuvi/AGSA-Net` |
| High-Dimensional Noise to Low-Dimensional Manifolds: A Manifold-Space Diffusion Framework for Degraded Hyperspectral Image Classification | 2604.26279v1 | B | code: `github.com/yangboxiang1207/MSDiff` |

**注意**：三篇 B 档全部是**分类**论文；本期入选的 3 篇超分论文（`2609.05303`、`2601.21338`、`2604.26279` 中的超分部分除外）没有任何代码声明。**C 档 = 未声明，不是核实不存在。**

## 9. 可跑的 baseline（本期论文提到的开源实现，已 HTTP 验活）

| 仓库 | 出处（arXiv ID） | HTTP |
|---|---|---|
| https://github.com/Azhenmiddleblock/MBTI/tree/main | 2607.12782v1 | ✅ 200 |
| https://github.com/nnuvi/AGSA-Net | 2609.06359v1 | ✅ 200 |
| https://github.com/yangboxiang1207/MSDiff | 2604.26279v1 | ✅ 200 |

共 3 个仓库：**3 个可访问**。（活链接判定：HTTP 200，跟随重定向；GitHub 对不存在的仓库/分支返回 404，故 200 视为可解析。）

---

## 10. 附：排序口径的实测偏差（需你决策，我未改动任何文件）

**现象**：脚本排序分 = 相关度 + 新鲜度加分，`RECENCY_MAX_BONUS = 20.0`，而本池相关度区间为 72–99（满分由 C/A/B/D 组权重 + 标题命中 + 关键词深度构成）。20 分的加分足以**跨越 15 分以上的相关度差距**，因此"更新时间只用于打破相近分数的平局"在实现上不成立 —— 相邻分数被打平的情况（如 #3/#4 同为 104.47）确实是平局裁决，但更多排序是被新鲜度主导的。

**实测后果（同一 123 篇池）**：

| 口径 | 第 1 名 | 与前十一的交集 |
|---|---|---|
| 现行 `rank_score`（相关度 + ≤20 新鲜度） | `2607.12782`（rel=91，tot=106.62） | — |
| 纯相关度排序 | `2510.11576`（rel=99，*Benchmarking foundation models for HSI classification: Application to cereal crop type mapping*，2025-10-13） | **仅 4/10 重合** |

全池**相关度最高**的 `2510.11576` 在现行口径下**排第 24**（新鲜度加分仅 0.66），因而本期没有入选；同样落榜的还有 `2604.01763`（rel=91，第 13）、`2601.16098`（rel=91）、`2601.07416`（rel=91）。第 10 名的切线为 101.51。

**可选修法（供你选，我没有动）**：① 把 `RECENCY_MAX_BONUS` 从 20 降到 4–6，使其真的只裁决平局；② 改为**分档排序**——先按相关度分档（如 90+/85–89/80–84），档内再用新鲜度；③ 保持现状，接受"新的优先"作为事实口径（但那就应该改掉"只打破平局"的说明）。另外，若你希望"相关度最高的几篇优先出版"，可以把 top-N 里固定保留 2–3 个名额给纯相关度榜首。

---

*本期推送：`README.md` @ `main`（见文末仓库与 commit 链接）。本地报告：`E:/tool/Hermes/cache/scratch/rs-radar/README-2026-10-02-final.md`；候选池：`candidates-2026-10-02.json`（202 篇）；选中：`selected-2026-10-02.json`；seen-state：`E:/tool/Hermes/cache/radar/arxiv_seen.json`（10 条）。*
