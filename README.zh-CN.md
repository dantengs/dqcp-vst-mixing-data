# SO(5) DQCP VST mixing 数据归档

[English](README.md) | 简体中文

本仓库归档 2026 年 11 月 6 日的稿件数据、11 月 8 日用 EFM v3 提取的 $\Lambda=23$ 谱，以及下文列出的 11 月 9 日更新。稿件数据、修复后的盲分析复跑结果和原始计算文件分别存放。[数据指南](DATA_GUIDE.zh-CN.md) 给出稿件各表、各图对应的文件及列说明。部分路径超过 Windows 默认的 260 字符限制，在 Windows 上请用 `git clone -c core.longpaths=true …` 克隆。[文件清单](manifests/file_manifest.csv) 记录来源和 SHA-256，[数据摘要](manifests/dataset_summary.json) 记录各数据集的版本与范围。

| 目录 | 内容 |
| --- | --- |
| [bootstrap/](bootstrap/) | Λ = 23 的 Skydiving ver4 和 Navigator ver3 EFM v3 谱及完整矩阵。主 Skydiving Notebook 含 971 个通道谱根、985 条 OPE 向量记录，另有 1 条固定外场归一化记录。 |
| [fuzzy_sphere/spectra/](fuzzy_sphere/spectra/) | 按稿件和 v0.5.5 复跑分目录保存的 UTF-8 CSV，分别记录原始能级、投影模式、物理能级分类及跨尺寸轨迹。 |
| [fuzzy_sphere/ope/](fuzzy_sphere/ope/) | CSV 和 JSON。整数扇区精确收缩、Stage B 收缩和半整数生产路线分表，共 37,689 行。另有稿件 OPE 目录和 N = 12 current 结果。 |
| [fuzzy_sphere/raw/](fuzzy_sphere/raw/) | v0.5.5 复跑的 1,447 个输入、N = 12 独立分析的 458 个输入、307 个权威生产文件，以及 current 原始检查点包和扫描数据。 |
| [comparison/](comparison/) | 已核对的图 2、4–6 数据，各截断阶数的 bootstrap 候选坐标、OPE 分量和转换因子，以及调谐与固定耦合的 singlet 序列。 |
| [manifests/](manifests/) | 文件校验值、来源、复跑记录，以及外部检查点的存放位置和验证收据。 |

## 2026 年 11 月 9 日更新

| 项目 | 数值 | 文件 |
| --- | --- | --- |
| 固定 $\Lambda=23$ minS 点的孤立应力张量（作业 6878、6953） | $\|\lambda_{\phi\phi T}\|=0.349770$；$ss$、$tt$ 为 $1.287065$、$0.834350$ | [isolated_stress_20261109/](bootstrap/efm_v3/isolated_stress_20261109/) |
| 同一点原求解 $\Delta=3$ 根的完整总量 | $\sqrt{\Gamma_{\phi\phi,\phi\phi}}=0.349994$ | [stress_coefficients.csv](bootstrap/efm_v3/isolated_stress_20261109/stress_coefficients.csv) |
| 自由点归一化检验（作业 6909，$\Lambda=15$） | $s,t,J,T$ 的数值/自由理论值为 $0.998122$、$0.999326$、$0.999862$、$1.000323$ | [free_theory_reference.csv](bootstrap/efm_v3/isolated_stress_20261109/free_theory_reference.csv) |
| 完整根权重 $\Gamma_{AB,AB}$（稿件附录 EFM 表，141 项） | mixed crossing 约定 | [bootstrap_complete_root_weights.csv](comparison/bootstrap_complete_root_weights.csv) |
| 发表约定下的核心系数 | bootstrap $(s,t,J,T)=(0.320, 1.255, 0.768, 0.350)$；球面 $N=5$–12 | [core_ope_coefficients_published.csv](comparison/core_ope_coefficients_published.csv) |
| 表 III 的 $1/N$ 外推，$N=8$–12 拟合 $a+b/N$ | $\|\lambda_{\phi\phi J}\|=0.78$，$\|\lambda_{\phi\phi T}\|=0.36$；其他窗口为 $0.776$–$0.786$、$0.355$–$0.369$ | [table3_finite_size_extrapolation.csv](comparison/table3_finite_size_extrapolation.csv) |
| 严格 primary 计数 | 非真空、$\ell\le3$：$N=10$ 为 39（$\Delta\le5.5$，即 Zhou 等表 VI 的窗口）和 52（$\Delta\le6.25$）；$N=11$ 为 35 和 50；$N=12$ 为 33 和 44 | [primary_counts.csv](fuzzy_sphere/spectra/manuscript/primary_counts.csv) |

外推截距随拟合窗口移向大 $N$ 而上升，各窗口间的差别是拟合窗口依赖，不是统计误差。孤立应力求解固定外场坐标，其余自旋 2 单态连续谱从 $3+10^{-6}$ 开始。其 Ward 贡献加上近阈值连续谱可复现原 $\Delta=3$ 根矩阵，逐元相对误差最大 $3.7\times10^{-6}$。

## 数据约定

- **Bootstrap**。打开 Notebook 后先运行数据读取单元，再运行相应的 `Dataset` 单元。按 `channel_index` 和 `root_index` 聚合同一根的记录，`component_index` 区分同根分解中的向量。十进制值以字符串保存原有精度。每条记录给出外场对顺序，并标记施加的 gap 和暂定幅度。[Skydiving Notebook](bootstrap/DQCP_bootstrap_CFT_L23.nb)
- **球面谱**。`N` 是轨道数，`L` 是空间自旋。`C2` 是内部 Casimir，`P` 是物理宇称，`X` 是段交换宇称。`energy` 保存原始能量，`Delta` 保存按守恒流能隙定标的维数。原始能级、投影模式和跨尺寸轨迹使用不同的标识。`sigma_Delta` 表示能量基展宽。稿件 N = 12 目录含 264 个能级，其中 45 个严格 primary（真空及 44 个非真空 primary）、154 个 descendant、65 个未定。
- **球面 OPE**。各路线保留插入算符及其秩、端点态、归一化、可用性和相位字段。`lambda_iso` 表示等距 Clebsch–Gordan 约定，`lambda` 表示共同的混合 crossing 约定。后者给出的 N = 12 current 幅度为 0.8574003792250015。L = 2 补空间证书状态见对应数据文件。
- **版本和比较**。图表数据和 bootstrap OPE 分量 CSV 对应 11 月 6 日的稿件快照。稿件保留的 76 条 OPE 路线与 v0.5.5 的 699 条聚合序列分开保存。图 2 的五个虚线标记对应未定原始能级。

原始文件包括解析后的 `Spectrum`、带提谱缩放的 `EFM_SE` 向量及完整矩阵。计入固定归一化记录时，Skydiving 有 972 个根和 986 条向量记录，Navigator 有 960 个根和 972 条向量记录。Notebook 的 `matrix_index` 是原始矩阵块内从零开始的索引。每条矩阵记录包含平移后的根坐标、按列排列的上三角元、本征值及输出向量数。原始矩阵除以 prefactor 得到谱归一化下的矩阵，原始向量则除以其平方根。[Skydiving ver4](bootstrap/efm_v3/Skydiving_ver4/) · [Navigator ver3](bootstrap/efm_v3/Navigator_ver3/)

## OPE 转换因子

2026 年 11 月 8 日的转换表覆盖 15 个外部标量通道，交换自旋 $\ell=0$–$4$，其中 52 项允许，23 项由 Bose 对称性禁戒。CSV 中 `v` 表示 $\phi$。`tt->35` 对应 $\mathbf{35}'$，与 `vt->35` 的 $\mathbf{35}$ 是不同的表示。请在允许行读取 `total_STF_to_solver_exact` 或 `total_STF_to_solver_numeric`。[转换表](comparison/fs_to_bootstrap_conversion_factors.csv)

另有 $s,t,J,T_{\mu\nu}$ 的固定分量换算，以及单矢量 crossing 到 VST 的逐表示因子。[固定分量因子](comparison/conversion_factors_key.csv) · [单矢量到 VST 因子](comparison/vsinglet_vst_by_rep.csv)

与解析后的 $\Lambda=23$ Skydiving minS ver4 谱比较时，采用等距 Clebsch–Gordan 和单位空间对称无迹张量（STF）归一化的球面系数按下式转换。

$$
|b_{ABR}|=G_{AB\to R}\,|\lambda_{\mathrm{iso,STF}}(A\otimes B\to R)|,
\qquad G_{AB\to R}=\left(\frac{d_R}{d_A d_B}\right)^{1/4}.
$$

$d_A,d_B,d_R$ 为 SO(5) 表示维数。谱振幅 $b$ 对应论文采用的 mixed crossing 系数 $\lambda$。卷积后的共形块已经包含空间因子 $\ell!/(2\ell-1)!!$，因此额外的振幅因子为 1。`total_h_to_solver_*` 列的输入是 $h=\sqrt{\ell!/(2\ell-1)!!}\,\lambda_{\mathrm{iso,STF}}$。v0.5.5 因子表中的 $c_r$ 用于前一步从秩为 $r$ 的矩阵元提取球面系数。[矩阵元提取因子](fuzzy_sphere/ope/v055/convention_factors.csv)

当归档路线 $X\otimes Y\to Z$ 需要置换标量腿时，先取不变量振幅 $\sqrt{d_Z}|\lambda_{\mathrm{iso,STF}}(X\otimes Y\to Z)|$，再按 bootstrap 配对除以 $(d_A d_B d_R)^{1/4}$。各微观插入路线分别保留。带符号比较需要对齐算符相位、内部张量取向和插入点顺序。

$\phi\phi T_{\mu\nu}$ 的 singlet 群因子为 $1/\sqrt{5}$，转换后振幅为 $\sqrt{15/2}\,|M_{20}/M_{00}|$。$N=10,11,12$ 的有限尺寸结果分别是 $0.254$、$0.264$ 和 $0.273$。Skydiving v3 的 $\Delta=3$ 根总振幅为 $\sqrt{\Gamma_{\phi\phi,\phi\phi}}=0.349994$。在该矩阵上，单个应力张量耦合的 Ward 上限为 $0.349770$。孤立应力张量求解直接给出 $0.349770$，现行稿件显示 $0.350$。11 月 6 日稿件快照中的 $0.203064$ 只是第一个向量的 $\phi\phi$ 分量模长。[球面插入路线](fuzzy_sphere/ope/manuscript/) · [稿件快照的 bootstrap 分量](comparison/bootstrap_ab_ope_components.csv)

旧单矢量 $\phi\phi$ crossing 使用内部张量 $P_R/d_R$，mixed crossing 使用 $5P_R/\sqrt{d_R}$。两边采用相同的卷积块约定时，旧谱的振幅平方先除以 $5\sqrt{d_R}$，再开方。其中 $J$ 的平方除以 $5\sqrt{10}$，$T_{\mu\nu}$ 的平方除以 $5$。旧单矢量 $\Lambda=23$ Navigator 的 stress 值转到 mixed 约定后为 $0.349456$。

## 读取原始文件

[复跑输入](fuzzy_sphere/raw/replay_v055/) 和 [N = 12 独立分析输入](fuzzy_sphere/raw/n12_isolated/) 保留逐字节校验的原始输入。读取 `.f64` 时，请使用对应的 `meta.json` 或导出元数据，确认形状、布局、态顺序及二进制校验值。[文件清单](manifests/file_manifest.csv) 的 `archive_path`、`source_key` 和 `local_source` 记录归档文件与原位置的对应关系。

[N = 12 current 检查点包](fuzzy_sphere/raw/current_n12/n12phiJ.tar) 保存原始小型检查点文件。解包后可用包内 `SHA256SUMS` 核验 93 个成员。[补充目录](fuzzy_sphere/raw/current_n12/supplemental/) 含随后保存的生产文本，[解码复跑目录](fuzzy_sphere/raw/current_n12/decoded_replay/) 含读出的二进制数组及元数据。

## 外部检查点

[检查点索引](manifests/external_raw_checkpoints.csv) 记录 531 个 payload 的原路径、可用的归档包及成员名，以及 payload SHA-256。[NAS 归档凭据](manifests/external_archive_receipts.json) 列出八个 NAS 包的路径、大小、整体 SHA-256 和验证收据。三个用于 current 计算的大窗口在索引中指向集群上的原始路径。

在仓库根目录运行 `sha256sum -c SHA256SUMS` 可校验入库文件。
