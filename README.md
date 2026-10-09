# 高光谱研究雷达日报 · 2026-10-09

> **数据来源**：本地缓存池 `candidates-2026-10-07.json`（365 天窗口 2025-10-07 ~ 2026-10-07，`sortBy=relevance`），**本期未做任何新扫**（无 arXiv/学术站点网络请求）。池的每日刷新由独立低风险任务负责，不在本任务职责内。
> **去重**：已推过 arXiv ID 一律不再推送（seen-state 已含 60 个 ID）。排序 = 相关度为主键，更新时间仅用于打破平局。

---

## 1. 本期要点

- **本期 10 篇新推全部落在 A/B 两组，C（超分+下游交叉项）与 D（基础模型/高效微调）两期为 0**——这不是入选失败，而是缓存池中该类论文确实稀疏；C 组是已知的真稀疏主题。
- **超分侧（A，6 篇）**：三篇给了可直接复用的评测/建模资产——`HyperBench`（统一 Wald 协议、70 组退化配置）、`Phy-CoSF`（ICML 2026，连续光谱场 + 深度展开）、`SpectraMorph`（自监督隐空间超分）。
- **分类侧（B，4 篇）**：主线是「少标注 + 预训练特征迁移」——FiLM 调制扩散特征、跨域自监督空谱建模、单像素浅层边缘模型。
- **最值得注意的信号**：`HyperBench` 实测报告，同一批 HSR 方法在「最易 PSF」上 PSNR 差距约 5 dB，在「最难 PSF」上扩大到 13 dB 以上——**单配置评测会系统性掩盖跨传感器退化下的鲁棒性差距**。这是一个可复现性 + 泛化性的双重缺口。
- **可复现性偏低**：本期 A 档（代码+数据）**0 篇**，B 档 2 篇，其余 8 篇 C（摘要/comment 未声明，非核实不存在）。高相关度 ≠ 高可复现。

---

## 2. 筛选结果

## 高光谱筛选结果（365 天窗口 + 去重）

- 拉取候选 **203** 篇 → 通过关键词策略 **123** 篇 → 已推过（去重剔除）**60** 篇 → **本期新推 10 篇**（另有 53 篇通过但未进前十，留待后续）
- 过滤规则：标题或摘要需同时命中 `hyperspectral / HSI` 与 A/B/C/D 关键词之一；pansharpening、multispectral 单独出现不算；SAR/雷达类无条件剔除
- 排序：与「超分+分类」方向的相关度（主）+ 更新时间（仅用于打破相近分数的平局），**不按投稿时间**

- 可复现性：**A（代码+数据）0 篇** / B（仅代码）2 篇 / C（未声明）8 篇　— 由摘要 + arXiv comment 判定，C 表示「未声明」而非核实不存在

| # | 标题 | arXiv | 相关度 | 更新时间 | 可复现性 |
|---|---|---|---|---|---|
| 1 | Data Efficient Complex Feature Fusion Network For Hyperspectral Image Classification | 2606.04710v1 | 82 | 2026-06-03 | C |
| 2 | HyperBench: Standardizing and Scaling Synthetic Evaluation for Hyperspectral Super-Resolution | 2605.21671v1 | 82 | 2026-05-20 | B |
| 3 | Phy-CoSF: Physics-Guided Continuous Spectral Fields Reconstruction and Super-Resolution for Snapshot Compressive Imaging | 2605.13583v1 | 82 | 2026-05-13 | B |
| 4 | AI-enabled Satellite Edge Computing: A Single-Pixel Feature based Shallow Classification Model for Hyperspectral Imaging | 2601.18560v1 | 82 | 2026-01-26 | C |
| 5 | Cross-Domain Transfer with Self-Supervised Spectral-Spatial Modeling for Hyperspectral Image Classification | 2601.18088v1 | 82 | 2026-01-26 | C |
| 6 | Rethinking Coupled Tensor Analysis for Hyperspectral Super-Resolution: Recoverable Modeling Under Endmember Variability | 2512.19489v1 | 82 | 2025-12-22 | C |
| 7 | Label-Efficient Hyperspectral Image Classification via Spectral FiLM Modulation of Low-Level Pretrained Diffusion Features | 2512.03430v1 | 82 | 2025-12-03 | C |
| 8 | SpectraMorph: Structured Latent Learning for Self-Supervised Hyperspectral Super-Resolution | 2510.20814v1 | 82 | 2025-10-23 | C |
| 9 | Spectral Super-Resolution using Spatial-Spectral Residual Operator Networks | 2609.35410v1 | 80 | 2026-09-28 | C |
| 10 | Sensor-Adaptive Infrared Spectral Reconstruction with Plug-and-Play Diffusion Priors | 2607.05636v1 | 80 | 2026-07-06 | C |

**可复现性判定依据**

- 1. `C` — 摘要与 comment 均未声明代码/数据
- 2. `B` — code: github.com/ritikgshah/HyperBench
- 3. `B` — code: github.com/PaiDii/Phy-CoSF.git
- 4. `C` — 摘要与 comment 均未声明代码/数据
- 5. `C` — 摘要与 comment 均未声明代码/数据
- 6. `C` — 摘要与 comment 均未声明代码/数据
- 7. `C` — 摘要与 comment 均未声明代码/数据
- 8. `C` — 摘要与 comment 均未声明代码/数据
- 9. `C` — 摘要与 comment 均未声明代码/数据
- 10. `C` — 摘要与 comment 均未声明代码/数据

**按主题分组（① ~ ⑥）**

- **① 超分 + 下游联合优化（C 组）**：本期无（C 组 0 篇）。
- **② 纯超分（A 组，6 篇）**：#2 HyperBench、#3 Phy-CoSF、#6 Rethinking Coupled Tensor、#8 SpectraMorph、#9 Spatial-Spectral Residual Operator、#10 Sensor-Adaptive Infrared Spectral Reconstruction。
- **③ 纯分类（B 组，4 篇）**：#1 DE-CFFN、#4 Satellite Edge Computing 单像素浅层分类、#5 Cross-Domain Transfer 自监督、#7 Label-Efficient FiLM 扩散特征。
- **④ 基础模型 / 高效微调（D 组，分两半）**：
  - **基础模型 / 预训练 / 表征学习**（0 篇）：_本期无_。
  - **高效微调 / 适配（D 子类，0 篇）**：_本期无_。
- **⑤ benchmark / 数据集**：#2 HyperBench（HSI-SR 合成评测框架与配置扫描）。
- **⑥ 其他**：本期无。

---

## 3. Top 3 精读（摘要级）

### Top 1 · Data Efficient Complex Feature Fusion Network for HSI Classification（2606.04710v1，rel 82，C 档）

- **方法**：DE-CFFN 是 CFFN 的数据高效变体。双分支：RVNN 处理原始高光谱 patch，CVNN 处理其傅里叶变换；降维由主成分分析（PCA）改为**因子分析**；两条 3D 卷积流的滤波器数逐层减半以压缩复杂度；两分支输出拼接后经 SE block 融合。
- **实验（摘要级）**：Pavia University 与 Salinas；报告「性能与 CFFN 相当，同时显著降低模型体积、显存与推理时延」。
- **局限**：改动属工程压缩（换降维 + 减半通道），摘要未给 OA/Kappa 数值、未给量化压缩比；两个小规模经典数据集，未涉跨传感器/downstream 联合任务。
- **延伸**：把「因子分析 vs PCA 降维」与 SE 融合消融量化为可复现表格（当前 C 档，无代码声明）。

### Top 2 · HyperBench: Standardizing and Scaling Synthetic Evaluation for HSR（2605.21671v1，rel 82，**B 档**）

- **问题**：HSR 缺真实配对数据，几乎全部依赖 Wald 协议的合成实验；但各单位实现差异大（通常 1 个高斯 PSF、1~2 个 SRF、少数下采样因子），导致**跨文献数值不可比、复现困难、且不能泛化到真实成像条件**。
- **贡献**：`HyperBench` 统一并扩展合成实验——**10 种 PSF、4 种取自在轨多光谱传感器的 SRF**、可配置空间下采样因子、匹配的加性高斯噪声；把「模型开发」与「实验设计」解耦，支持大规模自动评测与结构化日志。
- **关键实测**：用 6 个近期 HSR 方法在 4 个常用场景上跑 **70 组配置扫描**，方法间 PSNR 差距从最易 PSF 的约 **5 dB** 扩大到最难 PSF 的 **>13 dB**——这一脆弱性是现行单配置协议**结构性看不见**的。
- **代码**：https://github.com/ritikgshah/HyperBench （已验活 HTTP 200）。
- **延伸**：可直接作为选题 2 的评测底座。

### Top 3 · Phy-CoSF: Physics-Guided Continuous Spectral Fields（2605.13583v1，rel 82，**B 档** · ICML 2026）

- **问题**：CASSI 快照高光谱压缩成像中，既有重建方法多输出**固定离散波长**，无法做连续光谱重建/光谱超分。
- **方法**：把**深度展开网络**与**隐式神经表示（INR）**结合——两阶段架构桥接「离散波长训练」与「连续光谱渲染」，可在任意目标波长合成 HSI；核心 CoSF 模块作为每个展开阶段的动态先验，含三分支跨域特征混合器（空-频-通道）+ 按连续波长坐标查询的光谱合成头。
- **结论（摘要级）**：支持任意光谱分辨率的连续建模，在重建保真度与光谱细节上优于多数 SOTA。
- **代码/备注**：https://github.com/PaiDii/Phy-CoSF.git （已验活 HTTP 200）；comment 注明 **accepted by ICML 2026**。
- **延伸**：INR + 展开的「连续光谱」思路可迁移到 HSI 空谱超分（把输出波长/波段数解耦）。

---

## 4. 三个可做选题

### 选题 1（填补 C 组缺口）：超分—分类端到端联合优化

- **假设**：当前 HSI-SR 多以 PSNR/SAM 为目标，与下游分类目标存在偏差；联合优化可让 SR 输出更利于分类，尤其在少标注下。
- **方法草图**：SR 主干（如 #6 张量低秩 / #8 隐空间自监督）+ 轻量分类头，损失 = 重建项 + 分类项（可加不确定性加权或梯度手术避免主导）。
- **数据**：Pavia University、Salinas、Indian Pines、Houston 2013（同时可评重建与分类）。
- **指标**：重建 PSNR/SAM/ERGAS + 分类 OA/AA/Kappa。
- **baseline**：先用 `HyperBench` 固定一组退化配置，对照纯 SR→后接分类的两阶段方案。
- **风险**：联合训练不稳定；两任务尺度不匹配需权重/梯度策略调参。

### 选题 2（用 HyperBench 做鲁棒性）：跨退化配置鲁棒的 HSI-SR

- **假设**：在单一 PSF/SRF 上训练的 SR 模型换到未见退化会显著掉点（HyperBench 已证 >13 dB 差距）；对退化做随机化训练可提升跨配置泛化。
- **方法草图**：以 `HyperBench` 的 10 PSF × 4 SRF × 下采样因子做 degradation randomization / 一致性正则；评测「同配置」与「留出配置」两种协议。
- **数据/评测**：HyperBench 70 配置扫描（4 个经典场景）。
- **指标**：跨配置 PSNR 均值和最差配置 PSNR（worst-case），配 SAM。
- **baseline**：HyperBench 论文复现的 6 个 HSR 方法。
- **风险**：随机化可能牺牲同配置峰值；需报告 Pareto 权衡而非只看均值。

### 选题 3（填补 D 组缺口）：扩散/预训练特征的高效适配做少标注 HSI 分类

- **假设**：冻结大规模预训练特征 + 轻量适配（FiLM/Adapter/LoRA）即可在极少标注下接近全监督，且比全量微调更省显存。
- **方法草图**：以 #7 的「光谱 FiLM 调制低层扩散特征」为出发点，扩展到多源预训练特征并做参数高效微调对比（FiLM vs Adapter vs LoRA）；对齐方式引入跨域自监督（参考 #5）。
- **数据**：Pavia/Salinas/Indian Pines + 一个跨域场景（如 Houston→其他）。
- **指标**：每类 1/5/10 样本下的 OA/AA/Kappa、参数量、训练成本。
- **baseline**：SpectralFormer / 现有 HSI 基础模型 + 全量微调。
- **风险**：预训练域与 HSI 光谱域差距大；#7 属 C 档无代码，需自复现。

---

## 5. 会议论文

## 会议论文（Conference）

**arXiv × 会议索引匹配**：10 个候选，命中 0 篇同时有会议版本。

（本期无候选命中会议版本。）

**会议新进榜（Conference spotlight）**：本次首次纳入 0 篇。

_已更新 seen-state（0 个 venue）_

> 说明：spotlight 是一次性的——同一会议的条目在首次纳入后即写入 seen-state，同日后继 run 会报「首次纳入 0 篇」。此为本期与前次 run 的差集为空的正常结果，非索引故障。

---

## 6. 排除说明（典型示例）

过滤在「门禁（hyperspectral/HSI）+ A/B/C/D 主题词」两步上进行，SAR/雷达类无条件剔除。典型被过滤项：

| 被过滤标题（节选） | 原因 |
|---|---|
| UniDiff: Parameter-Efficient Adaptation of Diffusion Models for Land Cover Classification … | 雷达/微波类（synthetic aperture radar）→ 默认范围外 |
| HAMscope: a snapshot Hyperspectral Autofluorescence Miniscope for real-time molecular imaging | 纯传感器/仪器类（spectral imaging），未命中 A/B/C/D |
| SWAN: Self-supervised Wavelet Neural Network for Hyperspectral Image Unmixing | 未命中 A/B/C/D 任一关键词（解混不在冻结范围） |
| A UAV-Based VNIR Hyperspectral Benchmark Dataset for Landmine and UXO Detection | 未命中 A/B/C/D 任一关键词（数据集，非 SR/分类主线） |

（另有 68 条同因被滤，明细见 `selected-2026-10-09.json` 的 `dropped` 字段。）

> 范围已冻结：焦点 A（超分）+ B（分类）+ D（基础模型/适配），不引入视频压缩/跟踪/检测类任务词形。

---

## 7. 本期可复现（A/B 档，便于先跑）

- A（代码+数据）**0** 篇 ／ B（仅代码）**2** 篇 ／ C（未声明）8 篇

| 标题 | arXiv | 档 | 依据 |
|---|---|---|---|
| HyperBench: Standardizing and Scaling Synthetic Evaluation for Hyperspectral Super-Resolution | 2605.21671v1 | B | code: github.com/ritikgshah/HyperBench |
| Phy-CoSF: Physics-Guided Continuous Spectral Fields Reconstruction and Super-Resolution for Snapshot Compressive Imaging | 2605.13583v1 | B | code: github.com/PaiDii/Phy-CoSF.git |

## 8. 可跑的 baseline（本期论文提到的开源实现，已验活）

| 仓库 | 出处（arXiv ID） | HTTP |
|---|---|---|
| https://github.com/PaiDii/Phy-CoSF.git | 2605.13583v1 | ✅ 200 |
| https://github.com/ritikgshah/HyperBench | 2605.21671v1 | ✅ 200 |

共 2 个仓库：**2 个可访问**。

---

_本期报告由本地缓存池生成，未做新扫。排序按相关度，更新时间仅用于打破平局；④ 组分两半（基础模型 / 高效微调），本期两半均为 0 篇。_
