# 遥感研究雷达日报 · 2026-10-02（CVPR 2026 首次纳入版）

**本期来源与时间窗口**：arXiv API（16 次查询，`sortBy=submittedDate`，去重 902 篇）+ CVF 会议开放获取库（本地缓存 `CVPR2026_index.json`，4,042 条论文条目）｜arXiv 请求窗口 2026-09-25 ~ 2026-10-02，**实际有效窗口 2026-09-25 ~ 2026-09-30**（arXiv 公告延迟：16 次查询中日期最新的高光谱论文为 09-30，跨月投稿尚未进入索引）｜生成日期：2026-10-02｜排除项默认剔除 SAR/雷达/微波与纯光谱仪器。

> 说明：本期与同日早间一次运行窗口重叠，此前已报道的条目在「来源/会议」列标 **（续报）**，正文只补齐新证据与研究取向；新增价值集中在 **CVPR 2026 会议侧**（首次纳入）与 3 篇 arXiv 新增（HyperSAM / NE-LoRA / 原型-规则张量正则）。

## 1. 本期要点（Executive summary）

- **CVPR 2026 首次进入雷达，高光谱超分/光谱重建是会议里的一整块**：本地 CVF 索引 4,042 条论文中筛出 25 条高光谱/多光谱相关（core 级），本期**会议新进榜 15 篇**，其中 **6 篇直接是高光谱超分、光谱超分或全色锐化**（EMR-Diff、Unregistered HSI SR、Adversarial Unfolding、ScaleFormer/PanScale、Diffusion Neural Operator、RWKV Pan-sharpening）。（来源事实）
- **超分主线在会议侧呈现「同题异构」**：同一任务（低分辨率高光谱 → 高分辨率高光谱）分别从**生成式先验**（EMR-Diff 的边缘感知噪声扩散）、**解混-配准耦合**（UAFL 的丰度空间 + 可变形聚合）、**物理先验 + 对抗展开**（UALNet 的 PriorNet + unfolding adversarial）三条路径攻。（来源事实；「三线并进」的判断属**推断**）
- **arXiv 侧本周新增少而集中**：有效窗口内新增 15 篇、更新 5 篇，高光谱相关只有 9 篇；高光谱超分没有第二波投稿，新意主要来自**基础模型适配**——可提示基础模型 HyperSAM（SAM3 冻结 RGB 分支 + 高光谱侧编码器）、星上参数高效适配 NE-LoRA（带宽约束下在线更新），与 Reuse or Relearn 的谱诊断合成同一条主线：**新传感器适配要花多少参数**。（来源事实 + 推断）
- **评测规范化继续且有代码落地**：`Hyperspectral Image Models` 技术报告统一 55 个模型 / 6 大范式 / 24 个基准场景（机载、星载、UAV、火星 CRISM）、1,320 次模型-场景评测与 6,600 次带种子运行，并用 **Chebyshev guard band 的空间不相交划分**消除训练-测试像素重叠；结论是**场景难度差异 > 架构范式差异**（范式均值只差约 15 个百分点，Botswana 96.40% vs Houston 2018 56.70%）。（来源事实）
- **跨传感器泛化成为超分论文的共同验收条件**：OmniHSR（只训 ARAD，6 个未见数据集零适配迁移）、UALNet（Sentinel-2 → AVIRIS-NG，12→186 波段）、UAFL（未配准参考图）都在避免「同传感器同尺度」的温室评测。（来源事实 + 推断）

## 2. Ranked candidates

| 排名 | 标题（链接） | 来源/会议 | 日期 | 任务 | 数据/模态 | 核心贡献 | 代码/数据 | 评分 | 为什么值得看 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | [EMR-Diff: Edge-aware Multimodal Residual Diffusion Model for Hyperspectral Image Super-resolution](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_EMR-Diff_Edge-aware_Multimodal_Residual_Diffusion_Model_for_Hyperspectral_Image_Super-resolution_CVPR_2026_paper.html) | CVPR 2026 | 2026 | LR-HSI + HR-MSI 融合超分 | 高光谱 + 多光谱 | 多模态残差机制贯通 HR-MSI/LR-HSI/HR-HSI；边缘感知噪声策略（对边缘区施加更强扰动）；Bilateral Attention Fusion UNet + 多尺度监督 | 未见代码链接（摘要未给出） | 8.5 | 会议侧最完整的高光谱融合超分方案，边缘感知噪声是可直接复用的训练策略 |
| 2 | [Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_Enhancing_Unregistered_Hyperspectral_Image_Super-Resolution_via_Unmixing-based_Abundance_Fusion_Learning_CVPR_2026_paper.html) | CVPR 2026 + arXiv 预印本 | 2026 | 未配准高光谱超分 | 高光谱 + 未配准参考图 | SVD 初始解混保端元、网络只增强丰度图；coarse-to-fine 可变形聚合（像素级 flow + 相似度图 + 亚像素精修）；空间-通道丰度交叉注意力 + 动态门控融合 | 代码：https://github.com/yingkai-zhang/UAFL | 8.5 | 正面处理真实遥感里最难的一点——参考图未配准，且把超分写进丰度空间 |
| 3 | [Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization: From Multispectral Satellite Data to NASA Hyperspectral Image](https://openaccess.thecvf.com/content/CVPR2026/html/Young_Spectral_Super-Resolution_via_Adversarial_Unfolding_and_Data-Driven_Spectrum_Regularization_From_CVPR_2026_paper.html) | CVPR 2026 + arXiv 预印本 | 2026 | 光谱超分（12→186 波段），空间统一到 5 m | Sentinel-2 → AVIRIS-NG | PriorNet 数据驱动光谱先验替代隐式深先验；把对抗项嵌进展开网络（unfolding adversarial learning，训练+测试双向判别引导） | 代码：https://github.com/IHCLab/UALNet | 8.5 | 与你的光谱超分方向完全同题，且给出 15% MACs / 1/20 参数的效率证据 |
| 4 | [Super-Resolving Unseen Hyperspectral Sensors at Any Scale via Spatial Operators（OmniHSR）](https://arxiv.org/abs/2609.39926) | arXiv（续报） | 2026-09-30 | 跨传感器、任意倍率高光谱超分 | 高光谱（ARAD 训练，6 个未见数据集测试） | 不做谱值预测而预测**波段共享空间算子**；CSM 任意波段数重采样到参考位置；COFR 连续算子场支持 ×2~×48 | 摘要称「code will be publicly released soon」，**本期仍未开源** | 8.5 | 「预测算子而非像素」是目前跨传感器超分里最干净的重构，参数仅 0.538M |
| 5 | [Hyperspectral Image Models: Technical Report](https://arxiv.org/abs/2609.39871) | arXiv（新） | 2026-09-30 | 统一基准/框架（分类为主） | 24 个场景：机载、星载、UAV、火星 CRISM | 55 模型 / 6 范式统一注册表，4D/5D 张量自动适配；Chebyshev 保护带的空间不相交划分消除像素重叠；1,320 次评测 + 6,600 次带种子运行 | 代码：https://github.com/Tanishq251/Hyperspectral-Image-Models | 8.5 | 把「高光谱 SOTA 不可比」这件事工程化解决，是最适合当你实验的评测底座 |
| 6 | [HyperSAM: A Promptable Foundation Model for Hyperspectral Remote Sensing](https://arxiv.org/abs/2609.37340) | arXiv（新） | 2026-09-29 | 可提示高光谱基础模型（分类/异常/变化/目标/油膜） | 合成高光谱（SpaceNet 多光谱 → 物理启发丰度迁移）+ SAM3 伪掩码 | 冻结 SAM3 RGB 分支 + 从 RGB ViT 初始化的高光谱侧编码器 + ControlNet 式零初始化特征注入 + 轻量 MoE 掩码精修；CromSS 式置信度选择抗伪标签噪声 | 摘要未给出代码链接 | 8.0 | 把 SAM3 的交互先验借到高光谱，且自建数据合成管线解决了「高空间×密标注」稀缺 |
| 7 | [Cross-Scale Pansharpening via ScaleFormer and the PanScale Benchmark](https://openaccess.thecvf.com/content/CVPR2026/html/Cao_Cross-Scale_Pansharpening_via_ScaleFormer_and_the_PanScale_Benchmark_CVPR_2026_paper.html) | CVPR 2026 + arXiv 预印本 | 2026 | 跨尺度全色锐化 | 全色 + 多光谱（PanScale 数据集） | 首个大规模跨尺度 pansharpening 数据集 + PanScale-Bench；ScaleFormer 把分辨率泛化改写为序列长度泛化（Scale-Aware Patchify + RoPE 外推） | 代码/数据：https://github.com/caoke-963/ScaleFormer | 8.0 | 数据集 + 基准 + 方法三件套，跨尺度泛化协议可直接搬到高光谱融合 |
| 8 | [Resource-Aware Parameter-Efficient Model Adaptation for Onboard High-Dimensional Data（NE-LoRA）](https://arxiv.org/abs/2609.33687) | arXiv（新） | 2026-09-27 | 星上参数高效适配 | 4 个高光谱数据集 × 3 个骨干 | 低秩主分支 + 非线性辅助分支（NE-LoRA）；针对多矩阵适配器的差异化训练策略；以极小参数比例追平/部分超过全量微调 | 摘要未给出代码链接 | 7.5 | 面向 LEO 上行带宽的真实约束做高光谱在线更新，是「星上 PEFT」最直接的对标工作 |
| 9 | [Spatial-Spectral Residuals Informed Diffusion Neural Operator for Pan-sharpening](https://openaccess.thecvf.com/content/CVPR2026/html/Huang_Spatial-Spectral_Residuals_Informed_Diffusion_Neural_Operator_for_Pan-sharpening_CVPR_2026_paper.html) | CVPR 2026 | 2026 | 全色锐化 | 全色 + 多光谱 | 用 Galerkin 型神经算子替换注意力去噪骨干（函数空间扩散）；把像元级空间-光谱一致性残差写进每一步反向扩散做闭环引导 | 摘要未给出代码链接 | 7.5 | 「神经算子 + 扩散」同时压计算量与提升保真度，和你关注的算子化超分同源 |
| 10 | [Reuse or Relearn? A Spectral View of Earth Observation Foundation Models](https://arxiv.org/abs/2609.32756) | arXiv（续报） | 2026-09-26 | 基础模型微调诊断 | EO 基础模型 vs CLIP/DINO | 谱诊断三量（主子空间保持度、更新秩、更新幅度）：EO 模型更新更大、秩更高、保留预训练结构更少；子空间被保留处少量参数即可追平全量微调 | 未说明开源 | 7.5 | 给「该 PEFT 还是重学」提供可计算的判据，与 NE-LoRA 正好互补 |
| 11 | [Prototype-Rule Neurosymbolic Regularization for Rank-Constrained Tensor Neural Networks under Label Scarcity](https://arxiv.org/abs/2609.40131) | arXiv（新） | 2026-09-30 | 标签稀缺下高光谱分类 | Botswana / Indian Pines / Pavia U / Salinas，空间分离折 + 2~20 样本/类 | 在 Rank-R 张量网络上加可微原型-规则正则，可选推理期证据融合；空间评测下 Macro-F1 提升 +8.82（Botswana）、+5.49（Indian Pines）、+1.59（Pavia U）、−0.62（Salinas） | 摘要未给出代码链接 | 6.5 | 提升主要来自训练期正则而非推理融合，这个拆解比单纯报高准确率诚实 |
| 12 | [HyperDAM: Hyperspectral Distractor-Aware Memory with Amodal Expansion for SAM 3 Tracking](https://arxiv.org/abs/2609.34396) | arXiv（续报） | 2026-09-28 | 高光谱视频目标跟踪 | HOTC 2026 高光谱视频 | 帧零标定的高光谱门控拒绝对记忆的谱不一致更新；因果时空扩展器做向外 amodal 修正；私有评测第 2 名（68.0093% AUC / 87.7703% DP@20） | 自建 HOTC2026-Modal 标注 | 7.0 | 「门控式记忆更新」可平移到多时相变化检测的时序记忆 |
| 13 | [Implicit Neural Representation for Hyperspectral Video Compression](https://arxiv.org/abs/2609.31435) | arXiv（续报） | 2026-09-25 | 高光谱视频压缩 | 快照式高光谱视频（HOT2026 样例） | INR 扩展 RGB 视频压缩模型；BD-PSNR +4.99 dB、BD-rate −88.88%；下游跟踪 AUC 最高 +23.42%、距离精度 +35.56% | 摘要未给出代码链接 | 6.5 | 少见地把「压缩率」与「下游任务可用性」一起评——对星上/机载链路很关键 |
| 14 | [Multigrain-aware Semantic Prototype Scanning and Tri-Token Prompt Learning Embraced High-Order RWKV for Pan-Sharpening](https://openaccess.thecvf.com/content/CVPR2026/html/Li_Multigrain-aware_Semantic_Prototype_Scanning_and_Tri-Token_Prompt_Learning_Embraced_High-Order_CVPR_2026_paper.html) | CVPR 2026 | 2026 | 全色锐化 | 全色 + 多光谱 | 语义驱动扫描替代 RWKV 光栅扫描（LSH 建多粒度语义原型）；全局/原型/寄存器三 token 提示；可逆 Q-Shift 注入高频 | 摘要未给出代码链接 | 6.5 | 线性复杂度序列模型在全色锐化上的落地，适合做效率-精度对照基线 |
| 15 | [QSCP: Beyond Class-Name Prompts for Query-Guided Semantic Change Parsing](https://arxiv.org/abs/2609.33088) | arXiv（新） | 2026-09-27 | 语义变化检测 / 指代变化检测 | SECOND、WHU-CDC（光学） | 支持类别名、同义词与意图句查询，返回查询掩码 + 配对时序语义图；意图-语义槽解析 + 双向视觉证据 + 查询条件解码器 | 代码：https://github.com/qianyuancs/QSCP | 6.0 | 把「变什么→变成什么」写成可查询任务，是视觉语言变化检测的实用接口 |

（评分口径见 skill 参考文件：新颖性、技术深度、证据强度、可复现性、趋势信号、可迁移性、与本人方向契合度。**未开源且摘要未给实验数字的条目已相应扣分**。）

## 3. Top 3 精读（本期把 CVPR 2026 的三篇高光谱超分放在最前）

### 3.1 EMR-Diff（CVPR 2026）
- **核心问题**：硬件无法同时给高空间与高光谱分辨率；扩散模型做 HSI 超分已知的痛点是采样低效、细节生成受限、去噪不足。
- **方法**（来源事实，取自 CVF 摘要）：① **多模态残差机制**在 HR-MSI / LR-HSI / HR-HSI 三者间传递信息，提升融合效率；② **边缘感知噪声策略**用 HR-MSI 的边缘信息对边缘区域施加强噪声扰动，让模型优先重建高频细节；③ **Bilateral Attention Fusion UNet** + 多尺度监督，做渐进式重建与光谱-空间协同优化。
- **证据**：摘要只声明「在定量指标与视觉质量上优于现有方法」，**未给出数据集名与具体数值**——不要在综述里替它编造数字。
- **局限**：扩散采样成本在遥感大图/多时相批处理下仍是瓶颈（摘要未给推理耗时）；未提供代码链接，复现需等待。
- **可延伸**：把「边缘感知噪声调度」与已有的光谱先验（如 UALNet 的 PriorNet）拼成**空间-光谱各向异性噪声调度**，并验收跨传感器场景；也可与 OmniHSR 的算子预测替换去噪骨干，测效率-精度前沿。

### 3.2 Unregistered HSI SR via Unmixing-based Abundance Fusion Learning（CVPR 2026）
- **核心问题**：真实场景里高分辨率参考图往往**未配准**，直接融合会把错位当纹理学进去。
- **方法**（来源事实）：先用 SVD 做初始解混，**保端元不动，让网络只增强丰度图**（把病态的谱恢复问题降维成空间增强问题）；再用 **coarse-to-fine 可变形聚合**（粗金字塔预测像素级 flow 与相似度图 → 细亚像素精修）吸收未配准参考图的空间纹理；随后以空间-通道**丰度交叉注意力**块精修，并用动态门控的空间-通道调制融合模块合并编解码特征。
- **证据**：模拟与真实数据集上 SOTA 级超分性能；代码承诺开源并给出仓库地址（https://github.com/yingkai-zhang/UAFL ）。
- **局限**：解混假设线性混合模型，非线性/强阴影场景端元保真度存疑；可变形聚合在小重叠区可能退化（摘要未讨论失败案例）。
- **可延伸**：把该框架的「解混 → 丰度空间融合」当成通用骨架，替换空间增强分支为扩散（EMR-Diff 式）或算子（OmniHSR 式）；再把它接到跨传感器设定（训练一个传感器、测试另一个）验证是否仍成立。

### 3.3 Spectral Super-Resolution via Adversarial Unfolding（CVPR 2026）
- **核心问题**：Sentinel-2 只有 12 波段且空间分辨率不统一（60/20/10 m），而 AVIRIS-NG 这类高光谱只能覆盖北美局部——**能否用全球可得的 Sentinel-2 重建出 NASA 级高光谱？**
- **方法**（来源事实）：深展开框架 + **PriorNet 数据驱动光谱先验**替代常规的隐式深先验；把对抗项嵌入展开架构（判别器在**训练与测试阶段**都引导重建），作者称之为 unfolding adversarial learning（UAL）。任务是 12→186 波段光谱超分，并把空间分辨率统一到 5 m。
- **证据**：PSNR/SSIM/SAM 三项优于次优的 Transformer，同时只用 15% MACs、参数量少 20 倍；代码开源（https://github.com/IHCLab/UALNet ）。
- **局限**：跨域依赖 S2 → AVIRIS-NG 的配对构造，全球其他区域是否成立未验证；对抗展开的训练稳定性（摘要未报方差/多轮重复）。
- **可延伸**：把 PriorNet 换成 EO 基础模型的谱嵌入（SpectraEarth-FM 一类），看能否减少配对需求；或把「测试期判别引导」搬到跨传感器超分，检验它是真泛化还是测试时过拟合。

## 4. 三个可做的选题

### 选题 A：波长条件化的统一算子超分（Operator-based Unified Spectral-Spatial SR）
- **Problem**：现有高光谱超分按传感器、按尺度、按融合设置各自为政；跨传感器/任意倍率需要重训或适配。
- **Hypothesis**：把「预测逐波段谱值」改为「预测波段共享/波长条件的空间算子」，可同时得到跨传感器泛化、任意尺度重建与参数效率（OmniHSR 与 ScaleFormer 分别在空间侧支持这一点）。
- **Method sketch**：波长编码器（连续 λ 嵌入）+ 算子场（CSM/COFR 变体）+ 连续谱输出头（SSRON 的 DeepONet 式 function-to-function），训练时随机采样波段数与尺度做元训练；推理时给波长即可外推。
- **数据与指标**：ARAD、Pavia U、Chikusei、PanScale、EMIT/Sentinel-2 配对；PSNR/SSIM/SAM/ERGAS + 未见传感器零适配 PSNR 提升 + 参数量/FLOPs/推理时延。
- **Baselines**：OmniHSR、SSRON、ScaleFormer、UALNet/UAFL（会议侧三家）、以及经典耦合张量方法。
- **第一个最小可证伪实验**：在 ARAD 上训练、直接在 Pavia U 上零适配测 ×4/×8/×16，若不如「按目标传感器微调 10% 数据」的基线，则算子假设不成立。
- **Risk**：算子预测的计算成本可能随波段数上升；多传感器评测协议不统一导致对比不公（需固定评测场景，建议直接用 Hyperspectral Image Models 的空间不相交划分）。

### 选题 B：未配准 / 跨分辨率下的解混-扩散联合融合
- **Problem**：真实融合最大杀手是配准误差与分辨率不匹配；现有扩散融合（EMR-Diff）假设已配准，未配准工作（UAFL）用确定性网络增强，缺概率化的不确定性表达。
- **Hypothesis**：在丰度空间做扩散（而非谱空间），配准误差被显式建模为丰度图的形变不确定性时，跨传感器、强错位条件下的融合更稳。
- **Method sketch**：SVD/非负解混得端元与低分辨丰度 → 扩散模型在丰度空间去噪，形变场作为条件变量并输出后验样本 → 多尺度监督 + 空间-通道门控融合；用扩散样本的方差作为不确定度图。
- **数据与指标**：Pavia U/Chikusei + 合成错位（像素级到亚像素级）、真实未配准数据、PanScale；PSNR/SAM（谱保真）+ 错位鲁棒曲线 + 不确定度校准（ECE）。
- **Baselines**：UAFL、EMR-Diff、Diffusion Neural Operator pan-sharpening、少样本微调版 UALNet。
- **第一个最小可证伪实验**：只在合成错位（0/1/2/4 像素平移）上对比 UAFL 与「丰度空间扩散」，若在 4 像素错位下 SAM 无优势就放弃扩散路线。
- **Risk**：扩散推理成本；端元估计误差会直接污染扩散条件（需做端元误差传播的消融）。

### 选题 C：星上自适应更新的「可复用性判据」
- **Problem**：在轨模型随数据分布漂移需要更新，但 LEO 上行带宽有限；什么时候用 LoRA/NE-LoRA 就够、什么时候必须重学，目前没有可计算判据。
- **Hypothesis**：Reuse or Relearn 的谱诊断量（主子空间保持度、更新秩、更新幅度）在**更新前**即可预测参数高效适配的效果，从而把适配预算分配变成可决策问题。
- **Method sketch**：在高光谱分类/分割骨干（含 1D-CNN、HyViT 类、Mamba）上先用诊断量刻画预训练子空间，再按诊断结果选择 NE-LoRA 分支结构 / 秩 / 参与矩阵；把「诊断 → 策略」训练成一个轻量决策器。
- **数据与指标**：Indian Pines、Pavia U、Houston、WHU-Hi 等 + 4 个以上骨干；目标精度保持率 vs 上行字节数（accuracy-per-byte）、诊断量的预测相关性（Spearman）。
- **Baselines**：全量微调、LoRA、NE-LoRA、只冻结骨干的线性探测。
- **第一个最小可证伪实验**：在 2 个数据集 × 3 个骨干上算诊断量并与 PEFT 追平全量微调所需参数量做秩相关，若相关性不显著则判据不成立。
- **Risk**：诊断量在真实星上漂移（云、季节）下的稳定性未知；评测协议若不统一，结论易被质疑（同样建议采用空间不相交划分）。
## 会议论文（Conference）

**arXiv × 会议索引匹配**：464 个候选，命中 7 篇同时有会议版本。

| arXiv 候选标题 | 会议 | 匹配度 | 会议页 |
|---|---|---|---|
| MetaSpectra+: A Compact Broadband Metasurface Camera for Snapshot Hyperspectral+ Imaging | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Liu_MetaSpectra_A_Compact_Broadband_Metasurface_Camera_for_Snapshot_Hyperspectral_Imaging_CVPR_2026_paper.html) |
| Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_Enhancing_Unregistered_Hyperspectral_Image_Super-Resolution_via_Unmixing-based_Abundance_Fusion_Learning_CVPR_2026_paper.html) |
| Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization: From Multispectral Satellite Data to NASA Hyperspectral Image | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Young_Spectral_Super-Resolution_via_Adversarial_Unfolding_and_Data-Driven_Spectrum_Regularization_From_CVPR_2026_paper.html) |
| Exploring Spatiotemporal Feature Propagation for Video-Level Compressive Spectral Reconstruction: Dataset, Model and Benchmark | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Cai_Exploring_Spatiotemporal_Feature_Propagation_for_Video-Level_Compressive_Spectral_Reconstruction_Dataset_CVPR_2026_paper.html) |
| Cross-Scale Pansharpening via ScaleFormer and the PanScale Benchmark | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Cao_Cross-Scale_Pansharpening_via_ScaleFormer_and_the_PanScale_Benchmark_CVPR_2026_paper.html) |
| Lumosaic: Hyperspectral Video via Active Illumination and Coded-Exposure Pixels | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Verma_Lumosaic_Hyperspectral_Video_via_Active_Illumination_and_Coded-Exposure_Pixels_CVPR_2026_paper.html) |
| Brewing Stronger Features: Dual-Teacher Distillation for Multispectral Earth Observation | CVPR2026 | 1.00 | [CVF](https://openaccess.thecvf.com/content/CVPR2026/html/Wolf_Brewing_Stronger_Features_Dual-Teacher_Distillation_for_Multispectral_Earth_Observation_CVPR_2026_paper.html) |

**会议新进榜（Conference spotlight）**：本次首次纳入 15 篇。

### CVPR2026（15 篇）

- **[核心]** Brewing Stronger Features: Dual-Teacher Distillation for Multispectral Earth Observation — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Wolf_Brewing_Stronger_Features_Dual-Teacher_Distillation_for_Multispectral_Earth_Observation_CVPR_2026_paper.html)
- **[核心]** Cross-Scale Pansharpening via ScaleFormer and the PanScale Benchmark — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Cao_Cross-Scale_Pansharpening_via_ScaleFormer_and_the_PanScale_Benchmark_CVPR_2026_paper.html)
- **[核心]** EMR-Diff: Edge-aware Multimodal Residual Diffusion Model for Hyperspectral Image Super-resolution — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_EMR-Diff_Edge-aware_Multimodal_Residual_Diffusion_Model_for_Hyperspectral_Image_Super-resolution_CVPR_2026_paper.html)
- **[核心]** Enhancing Unregistered Hyperspectral Image Super-Resolution via Unmixing-based Abundance Fusion Learning — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Zhang_Enhancing_Unregistered_Hyperspectral_Image_Super-Resolution_via_Unmixing-based_Abundance_Fusion_Learning_CVPR_2026_paper.html)
- **[核心]** Exploring Spatiotemporal Feature Propagation for Video-Level Compressive Spectral Reconstruction: Dataset, Model and Benchmark — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Cai_Exploring_Spatiotemporal_Feature_Propagation_for_Video-Level_Compressive_Spectral_Reconstruction_Dataset_CVPR_2026_paper.html)
- **[核心]** Leveraging Multispectral Sensors for Color Correction in Mobile Cameras — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Cogo_Leveraging_Multispectral_Sensors_for_Color_Correction_in_Mobile_Cameras_CVPR_2026_paper.html)
- **[核心]** Lumosaic: Hyperspectral Video via Active Illumination and Coded-Exposure Pixels — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Verma_Lumosaic_Hyperspectral_Video_via_Active_Illumination_and_Coded-Exposure_Pixels_CVPR_2026_paper.html)
- **[核心]** MetaSpectra+: A Compact Broadband Metasurface Camera for Snapshot Hyperspectral+ Imaging — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Liu_MetaSpectra_A_Compact_Broadband_Metasurface_Camera_for_Snapshot_Hyperspectral_Imaging_CVPR_2026_paper.html)
- **[核心]** Multigrain-aware Semantic Prototype Scanning and Tri-Token Prompt Learning Embraced High-Order RWKV for Pan-Sharpening — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Li_Multigrain-aware_Semantic_Prototype_Scanning_and_Tri-Token_Prompt_Learning_Embraced_High-Order_CVPR_2026_paper.html)
- **[核心]** Regulating Rather than Constraining: Adaptive Guidance for Complex Spectral Reconstruction in Pansharpening — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Wen_Regulating_Rather_than_Constraining_Adaptive_Guidance_for_Complex_Spectral_Reconstruction_CVPR_2026_paper.html)
- **[核心]** SGDE: Self-supervised Geometry Degradation Estimation Framework for Coded Aperture Compressive Spectral Imaging — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/He_SGDE_Self-supervised_Geometry_Degradation_Estimation_Framework_for_Coded_Aperture_Compressive_CVPR_2026_paper.html)
- **[核心]** Spatial-Spectral Residuals Informed Diffusion Neural Operator for Pan-sharpening — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Huang_Spatial-Spectral_Residuals_Informed_Diffusion_Neural_Operator_for_Pan-sharpening_CVPR_2026_paper.html)
- **[核心]** Spectral Super-Resolution via Adversarial Unfolding and Data-Driven Spectrum Regularization: From Multispectral Satellite Data to NASA Hyperspectral Image — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Young_Spectral_Super-Resolution_via_Adversarial_Unfolding_and_Data-Driven_Spectrum_Regularization_From_CVPR_2026_paper.html)
- **[核心]** Spectrum from Defocus: Fast Spectral Imaging with Chromatic Focal Stack — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Aydin_Spectrum_from_Defocus_Fast_Spectral_Imaging_with_Chromatic_Focal_Stack_CVPR_2026_paper.html)
- **[核心]** WHU-MARS: A Multispectral Aerial-Ground Benchmark Towards Any-Scenario Person Re-Identification — [CVPR2026](https://openaccess.thecvf.com/content/CVPR2026/html/Zhao_WHU-MARS_A_Multispectral_Aerial-Ground_Benchmark_Towards_Any-Scenario_Person_Re-Identification_CVPR_2026_paper.html)

_已更新 seen-state（1 个 venue）_

## 排除说明与来源说明

### 6.1 本期排除的候选

| 条目 | 来源 | 排除理由 |
|---|---|---|
| Region-Local Copula Evidence Fusion for Heterogeneous Remote Sensing Change Detection | arXiv 2609.32716（2026-09-26） | 异源变化检测，实验基准为 Lake / UK（光学- SAR 跨模态），按 skill 默认策略归为 SAR 相关排除 |
| Cryo-Bench: Benchmarking Foundation Models for Cryosphere Mapping | arXiv 2603.01576（更新，2026-03-02 首发） | 冰冻圈制图，摘要含 SAR/微波成分，本期不纳入 |
| High-power photoconductive THz emitters… / Phase-resolved wide-field CARS microscopy… / Scanless quantum Fourier-transform mid-infrared spectroscopy… | arXiv 2610.00744、2609.39730、2609.37281（2026-09-29~30） | 纯光谱仪器/物理测量，无 ML 或地理空间角度 |
| MetaSpectra+ / Lumosaic / Spectrum from Defocus / SGDE（编码孔径压缩光谱成像）/ Leveraging Multispectral Sensors for Color Correction / WHU-MARS（多光谱行人重识别） | CVPR 2026 会议索引 | **保留在会议新进榜内**，但按 skill 规则属硬件类/非遥感 CV 任务，不进入加权排名（Lumosaic 与 MetaSpectra+ 属硬件类，WHU-MARS 属非地理空间任务） |

### 6.2 来源与检索方法（可复核）

- **arXiv API**：`https://export.arxiv.org/api/query`，16 次查询全部 200-OK（0 次失败，本轮未触发 429/503），请求间隔 3.6 s，每条请求 `--max-time 30`。核心表述覆盖：`all:"hyperspectral" AND all:"super-resolution"`、`all:"hyperspectral image super-resolution"`、`all:"spectral super-resolution"`、`all:"pansharpening"`、`all:"hyperspectral" AND all:"classification"`、`all:"hyperspectral" AND all:"foundation model"`、`cat:eess.IV AND all:hyperspectral`、`all:"hyperspectral" AND all:"unmixing"`（以上 8 条带 `submittedDate` 窗口限定），另有 8 条无界 `sortBy=submittedDate` 查询用于窗口/延迟核验。
- **窗口核验**：无界查询 `all:"hyperspectral"`（max_results=300）返回的 `published` 跨度为 2026-01-18 ~ 2026-09-30；`all:"spectral super-resolution"` 最新为 09-28，`all:"pansharpening"` 最新为 08-21。**故 09-30 之后的论文不是「没有」，而是尚未进入 arXiv 索引（公告延迟）**，本期有效窗口为 09-25 ~ 09-30。
- **候选复核**：12 个进入榜单/分析的 arXiv ID 逐个请求 `arxiv.org/abs/<id>`，比对 `citation_title` 与本地标题，**12/12 一致**（逐一打印通过）。
- **会议来源**：CVF 开放获取库 `openaccess.thecvf.com` 的 `CVPR2026?day=all` 列表（4,042 条，本地缓存 2,614,128 字节，`conf_index.py` 命中缓存未重新下载）；6 篇重点会议论文的摘要通过 CVF 论文页直接抓取（非二手转述）。
- **未使用**：Semantic Scholar、Papers with Code、Hugging Face（因此本报告不对这三个源的榜单/热度作任何断言）。
- **区分声明**：报告中标「来源事实」的句子可在上述 URL 复核；「推断」性判断（趋势、可迁移性、评分）为本人分析，不属原始论文论断。

### 6.3 数据文件（同目录）

- `papers-2026-10-02.json`（16 次查询解析结果，902 篇去重）
- `window-2026-10-02.json`（窗口内 20 篇：新增 15、更新 5）
- `candidates-2026-10-02.json`（464 个会议匹配候选）
- `conf_fragment-2026-10-02.md`（conf_match.py 原始输出，本节上方的「会议论文」为原样粘贴）
- `verify-2026-10-02.json`（12/12 arXiv ID 复核记录）
- `cvf-abstracts-2026-10-02.json`（6 篇 CVPR 论文页摘要原文）
