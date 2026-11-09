# 数据指南

[English](DATA_GUIDE.md) | 简体中文

2026 年 11 月 9 日的稿件 (i) 以 $\Lambda=23$ minS 点的孤立应力张量求解作为 bootstrap 参考，(ii) 全部 OPE 采用同一约定：推广到所有通道的 LiShen2026 表 II $v$ singlet 约定 $\lambda$。两者说明如下。

本指南把稿件的表和图对应到归档文件，并说明稿件直接使用的文件各列含义。仓库结构和归一化约定见 [README](README.zh-CN.md)。`fuzzy_sphere/raw/` 下的原始输入由所在目录的 `meta.json`、`*_meta.json` 和 `checkpoints.toml` 说明。

## 获取文件

部分文件名超过 150 个字符。在 Windows 上克隆前请启用长路径，或克隆到 `C:\d` 这样较短的目录；否则 Git 检出时会缺文件。

```bash
git clone -c core.longpaths=true https://github.com/dantengs/dqcp-vst-mixing-data.git
```

```bash
sha256sum -c SHA256SUMS
```

`manifests/file_manifest.csv` 给出归档文件的大小、SHA-256 和本地来源。以下文件不在其中：清单本身、两份 README、两份指南、`SHA256SUMS`、许可与引用文件（`LICENSE`、`LICENSE-DATA`、`CITATION.cff`、`.zenodo.json`）和 Git 配置文件。

## 稿件条目与文件对照

| 稿件条目 | 文件 | 选取方式 |
| --- | --- | --- |
| 表 I，bootstrap 列 | `bootstrap/efm_v3/Skydiving_ver4/Spectrum_*.m` | 通道内最低根；外场 $\phi,s,t$ 维数为文件名前三个数 |
| 表 I，$N=12$ 列 | `fuzzy_sphere/spectra/manuscript/n12_two_scheme_levels.csv` | `A_publication == "P"`，`(rep, L, P)` 内最低或次低 |
| 表 II（31 个新增 $N=10$ primary 及 2 个原 P 现为未定） | `fuzzy_sphere/spectra/manuscript/n10_table2_additional_primaries.csv`；背景见 `n10_zhou_tableVI_comparison.csv` | 全部 |
| 表 III（全部列） | `comparison/table3_ope_lambda.csv` | 全部；`displayed_*` 即表中显示值 |
| 表 III 的输入 | bootstrap：`comparison/bootstrap_cutoff_candidates.csv`（扫描比值）与 `bootstrap/efm_v3/isolated_stress_20261109/`（$J$、$T$）；球面：`fuzzy_sphere/ope/manuscript/scalar_insertion_routes.csv`、`comparison/table3_finite_size_series.csv` | 见约定一节 |
| 表 III，$1/N\to0$ 列 | `comparison/table3_finite_size_extrapolation.csv`，输入为 `comparison/table3_finite_size_series.csv` | `N_min = 8`、`N_max = 12` |
| 表 V、IX、X（候选坐标、截断依赖、gap 敏感性） | `comparison/bootstrap_cutoff_candidates.csv` | 按 `Lambda`、`next_tensor_gap` 取行 |
| 表 VI（调谐 singlet 序列） | `comparison/singlet_tuned.csv` | 全部 |
| 表 XI（144 个完整根权重） | `comparison/bootstrap_complete_root_weights.csv` | `Gamma_lambda` 列 |
| 表 XII（18 个新增 primary 族） | `fuzzy_sphere/spectra/manuscript/additional_primary_continuations.csv` | 全部 |
| 表 XIII（$N=12$ 完整目录，264 个能级） | `fuzzy_sphere/spectra/manuscript/n12_two_scheme_levels.csv` | 全部；标签为 `A_publication` |
| 表 XIV（逐通道的 $G$ 与 $\kappa$） | `comparison/ope_convention_by_channel.csv`；按自旋分列的因子见 `comparison/fs_to_bootstrap_conversion_factors.csv` | 全部 |
| 图 2 | `comparison/figure2_points.csv`；虚线标记见 `comparison/figure2_unresolved_weights_ver4.csv` | 全部 |
| 图 4（共形检验） | `comparison/figure4a_order_parameter_points.csv`、`figure4b_spacing.csv`、`figure4c_raising.csv` | 全部 |
| 图 5、图 6(b)（固定耦合 singlet） | `comparison/fixed_coupling_singlet.csv` | `panel` 为 a 或 b |
| 图 6(a) | `comparison/singlet_tuned.csv` | 全部 |
| 孤立应力张量（附录 A.3） | `bootstrap/efm_v3/isolated_stress_20261109/stress_coefficients.csv` | 按 `external_pair` |
| 正文中的 primary 计数 | `fuzzy_sphere/spectra/manuscript/primary_counts.csv` | 按 `N` 和 `window` |

表号和图号对应 2026 年 11 月 9 日的稿件，浮动体位置变化时可能改变。编号不一致时请按内容识别。

## 标识约定

**Bootstrap 通道。** 求解器文件使用 $SO(6)$ 式标签。`source_sector` 如 `S+, l=2`，由标签、自旋奇偶和自旋组成。

| 求解器标签 | `S` | `V` | `A` | `T` | `50` | `64` | `S84` | `S105` | `175` |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| $SO(5)$ 表示 | **1** | **5** | **10** | **14** | **30** | **35** | **35′** | **55** | **81** |

`+`、`-` 表示偶、奇自旋通道，不是宇称。**5**、**30**、**35**（来自 $s\phi$、$t\phi$）的物理宇称为 $-$，其余为 $+$。`V$theta` 保存固定外场归一化 $\beta_{\phi\phi t}=1.0858374$。`Spectrum` 中的 `{Delta, {b_1, b_2, ...}}` 按稿件通道表的外场对顺序给出振幅；保留多分量的根会以相同 `Delta` 出现多次。

**球面能级。** `phys_level_key = N<N>:C<C2>:L<L>:P<±1>:<E>` 依次表示尺寸、Casimir、空间自旋、物理宇称和原始能量。末尾为维数的键（如 `N12:C3:L3:P-1:4.426230`）表示投影模式。`C2` 采用 $C_2(\mathbf 5)=2$ 的归一化，**1、5、10、14、35、35′、30、81、105、55** 依次为 0、2、3、5、6、8、9、10、12、14。`rep = 35p` 与 `35'` 均表示 **35′**。`C2=15{84|154}` 这类标签表示 Casimir 不能唯一确定表示。`block = s<a>_s<b>_L<L>` 给出两个内部自旋和 $L$。`X` 是段交换宇称；没有该对称性的块记为 `0`。

**分类。** 严格 primary 须在 $\kappa_c/3$、$\kappa_c$、$3\kappa_c$ 下均满足 $w_P\ge0.90$，且对称副本一致、保留窗口稳定。

## OPE 约定

文中涉及三种归一化。$\lambda_{\rm iso}(A\otimes B\to R)$ 是等距 CG（$\mathcal C\mathcal C^\dagger=1_R$）前的系数，即球面提取直接给出的量。求解器幅度为 $\beta=G\,\lambda_{\rm iso}$，$G=(d_R/d_Ad_B)^{1/4}$。稿件中所有系数均为 $\lambda=\kappa\beta$：

| 规则 | 情形 | $\lambda$ |
| --- | --- | --- |
| (a) | $A$、$B$ 或 $R$ 为单态 | $\beta$ |
| (b) | $R=\mathbf{10}$（与 current 相同的定分量归一化） | $\lambda_{\rm iso}/\sqrt2=(d_Ad_B/40)^{1/4}\beta$ |
| (c) | 其余 | $\lambda_{\rm iso}=(d_Ad_B/d_R)^{1/4}\beta$ |

外场耦合按 $\phi\phi\to s$、$\phi\phi\to t$、$ss\to s$、$st\to t$、$tt\to t$ 定义，于是 $\lambda_{\phi\phi s}=\beta_{\phi\phi s}$、$\lambda_{\phi\phi t}=(25/14)^{1/4}\beta_{\phi\phi t}$、$\lambda_{\phi\phi J}=(5/8)^{1/4}\beta_{\phi\phi J}$、$\lambda_{\phi\phi T}=\beta_{\phi\phi T}$（即 LiShen2026 表 II），$\lambda_{sss}=\beta_{sss}$、$\lambda_{stt}=\beta_{stt}$，$\lambda_{ttt}=14^{1/4}\beta_{ttt}$（三阶不变量取等距归一化；若取迹归一化需再乘 $\sqrt{20/27}$）。`bootstrap_cutoff_candidates.csv` 中的扫描比值 $r_{XYZ}=\beta_{XYZ}/\beta_{\phi\phi t}$ 是求解器量。选择性范数 $B$ 一律用 $\beta$ 计算。[逐通道因子](comparison/ope_convention_by_channel.csv)

## 列说明

### `comparison/`

| 文件 | 列 |
| --- | --- |
| `bootstrap_complete_root_weights.csv` | 孤立应力求解：`AB` 外场对；`rep`、`spin`、`Delta` 交换根；`source_sector`、`source_root_index` 在 Spectrum 中的位置；`Gamma_beta` $=\sum_a\beta_{AB,a}^2$；`kappa`；`Gamma_lambda` $=\kappa^2\Gamma_\beta$（表 XI 所印）；`multi_component`；`imposed_gap_or_threshold`（gap 或 $\ell+1+10^{-6}$ 连续谱阈值）；`isolated_stress` 标出 $\Delta=3$ 的 Ward 块 |
| `bootstrap_ab_ope_components.csv` | 11 月 6 日快照，只含首分量（`amplitude`、`amplitude_squared`）。当前附录表请用 `bootstrap_complete_root_weights.csv`。 |
| `bootstrap_cutoff_candidates.csv` | `Lambda`；`next_tensor_gap` 即 $g_t$；优化后的 `Delta_phi`、`Delta_s`、`Delta_t`；扫描比值 $\beta_{\phi\phi s}/\beta_{\phi\phi t}$、$\beta_{ttt}/\beta_{\phi\phi t}$、$\beta_{stt}/\beta_{\phi\phi t}$、$\beta_{sss}/\beta_{\phi\phi t}$ |
| `core_ope_coefficients_published.csv` | `source`（bootstrap 行为 `mixed_L23_Skydiving_ver4`，$\phi\phi T$ 为 `mixed_L23_isolated_stress_6953`）；球面行的 `N`、`insertion`；`quantity`（$\phi\phi s$、$\phi\phi t$、$\phi\phi J$、$\phi\phi T$）；`beta_vst` 求解器值；`vst_to_published_factor` $=\kappa$；`lambda_published` $=\lambda$；`kind` |
| `table3_ope_lambda.csv` | 表 III 各行：`convention_factor_from_beta_ratio` 乘在 $\beta$ 比值上；全精度 `bootstrap`、`N12`、`N11`、`N10` 及 $1/N$ 截距；`fs_insertion` 插入路线；`displayed_*` 为表中显示值 |
| `ope_convention_by_channel.csv` | `AB`、`R`、各维数、`rule`（a/b/c）、精确式与数值的 `G` 和 `kappa`，以及 $\lambda/\lambda_{\rm iso}$ |
| `table3_finite_size_extrapolation.csv` | `quantity`；拟合窗口 `N_min`–`N_max`；$a+b/N$ 的 `intercept_a`、`slope_b`；`max_abs_residual`；作对照的 $a+b/N+c/N^2$ 截距 `quadratic_fit_intercept`；`displayed_in_table3` |
| `table3_finite_size_series.csv` | `N`；$\phi$ 插入、发表约定下的 `phiphi_J`、`phiphi_T` |
| `figure2_points.csv` | `method`；`N`；`rep`；`L`；`P`；`Delta`；`B` 为 $\beta$ 下的 bootstrap 振幅范数（孤立应力求解；应力点取完整 Ward 向量，$B=1.573$）；`kind`（`strong` $B\ge0.10$、`weak` $0.01\le B<0.10$、`external`、`primary`、`unresolved`）；`source_id` 为 bootstrap 的 `sector:root` 或球面键；`track_id`；`x` 作图横坐标 |
| `figure2_unresolved_weights_ver4.csv` | 5 个虚线能级：$\kappa_c$ 下的 `w_primary`、`w_descendant`；$\kappa_c/3$、$3\kappa_c$ 下的 `w_primary_thr_lo/hi`；`window_status`；`nearest_bootstrap_Delta`、`absolute_distance`、`relative_distance_percent` |
| `figure4a_order_parameter_points.csv` | `N`、`g`、`sqrt_N_m2` $=N^{1/2}\langle m_i^2\rangle$ |
| `figure4b_spacing.csv` | `branch`（`dphi`、`dt`、`curlJ`、`dJ`）、`N`、`value` $=\epsilon_{\mathcal O,1}$ |
| `figure4c_raising.csv` | `branch`（`phi`、`t`、`stress`）、`N`、`value` $=\mathcal C_{\mathcal O}$ |
| `fixed_coupling_singlet.csv` | `panel`（`a` 为 $g$ 扫描，`b` 为 $N$ 序列）；`N`；`g`；`x` 作图横坐标；`value` $=\Delta_s^{\rm eff}$；`evidence`：`A` 为在 $g_*$ 锚定且同基主导重叠，`L` 为经相邻重叠链锚定 |
| `singlet_tuned.csv` | `N`；`g` $=g_*(N)$；原始能量 `E0`、`E_S`、`E_J`、`E_stress`；`alpha` $=2/(E_J-E_0)$；`Delta_S`；`Delta_stress_check` |
| `n10_unresolved_bootstrap_candidates.csv` | 两个未定 $N=10$ 行的候选根，按 `distance_rank` 排序；`selected` 标出稿件显示的根 |
| `conversion_factors_key.csv`、`vsinglet_vst_by_rep.csv`、`fs_to_bootstrap_conversion_factors.csv` | 换算因子，含精确式（`*_exact`）和数值（`*_numeric`），见 README |

### `fuzzy_sphere/spectra/manuscript/`

| 文件 | 列 |
| --- | --- |
| `n12_two_scheme_levels.csv` | `phys_level_key`、`block`、`raw_index`、`rep`、`L`、`P`、`C2`、`X`、`Delta`。`A_*` 为稿件分类：`A_publication`（`P`、`D`、`-`）；`A_detail`（`P` primary、`D` descendant、`M` 混合、`W` 窗口敏感、`R` 由分散模式解析出的 primary、`F` 家族覆盖不全）；`A_reviewed_class`、`A_window_status`；权重 `A_wP`、`A_wD`、`A_parent_weight`。`B_*` 为独立的有界切换交叉检验：`B`（`P`、`D`、`M`、`U` 未覆盖、`S` 依赖方法、`V` 真空、`X` 方案 B 无记录）、`B_status`、`B_Psupport`、`B_mode_Delta`、`B_mode_sigma_Delta` 及各切换标签 |
| `n12_two_scheme_transitions.csv` | `A_publication`（行）与 `B`（列）的计数 |
| `n12_two_scheme_distributed_modes.csv` | 分布在多个原始能级上的 13 个 primary 方向：`mode_delta`、能量基展宽 `sigma_delta`、`components`（`#索引:Delta:权重`） |
| `n12_reviewed_raw_levels.csv` | $N=12$ 各阶段标签（`classes_v035`、`revised_class`、`reviewed_class`） |
| `n10_n11_formal_low_spin_spectrum.csv` | $N=10,11$ 的同类字段；`derived_reviewed_class_N12_priority` 按 $N=12$ 规则给出稿件计数；`w_primary_thr_lo/hi` 对应 $\kappa_c/3$、$3\kappa_c$；`parent_*`、`primary_*` 把 descendant 和模式联到轨迹 |
| `n10_zhou_tableVI_comparison.csv` | Zhou 等表 VI 的 129 行：原文值（`paper_*`，未归类时 `paper_PD` 为空）与本文标签（`current_label` 为 `P`/`D`/`M`，`current_window`），并给出 0.90、0.85 两个门限的结果 |
| `additional_primary_continuations.csv` | 18 个新增族：`Delta_N10`、`Delta_N11`、`Delta_N12`（无通过的延续时为空）、`wP_N10`、`wD_N10`、`paper_class`（空表示 Zhou 等未归类） |
| `n10_table2_additional_primaries.csv` | 表 II 的 33 行：`assignment`（`U->P`、`D->P`、`above window` 表示 $5.5<\Delta\le6.25$、`P->U`）、`Delta_FS_N10`、`phys_level_key`、`class`、`w_primary`、`in_mixed_channels`、最近 bootstrap 根 `Delta_bootstrap_nearest` 及其 `B_bootstrap_beta`、`bootstrap_sector` |
| `primary_counts.csv` | 按 `N` 和维数 `window` 统计的严格 primary 数 |

### `fuzzy_sphere/ope/manuscript/`

| 文件 | 列 |
| --- | --- |
| `scalar_insertion_routes.csv` | 各路线的 mixed crossing $\beta$：`vvt_t` 为 $t$ 插入的 $\phi\phi t$，`vvt_v` 为 $\phi$ 插入；另有 `vvs_s`、`vvs_v`、`sss_s`、`stt_s`、`stt_t`、`ttt_t`；`*_over_vvt` 为除以 `vvt_t` 的比值；`*_alt` 为另一种插入 |
| `representative_ope_routes.csv`、`retained_n5_n11_ope_routes.csv` | `route` 插入算符（`S` singlet、`T` tensor、`phi` vector）；`X`、`Z` 端点轨迹；`rank`；`lambda_iso_N5` … `lambda_iso_N12`；`display_*` 为稿件中的名称。`kind`、`copy_check` 为中文，见下方术语表。 |
| `n12_reviewed_integer_ope.csv` | 每行一个 $N=12$ 收缩：`insertion`、`rank`、端点 `X_*` 与 `Z_*`、矩阵元 `me_*`、`cg_iso`、`normalization_Z_used`、`lambda_iso_signed`、`lambda_3j_blind`；`publishable`、`eligible_strict` 标出可用于比较的行 |
| `n12_ope_route_identity.csv` | 各保留路线的 $N=12$ 值及其匹配方式 |

### `bootstrap/efm_v3/isolated_stress_20261109/`

| 文件 | 列 |
| --- | --- |
| `stress_coefficients.csv` | `isolated_coefficient` 为 Ward 块值 $c\,w$；`original_root_total` 为原 $\Delta=3$ 根的 $\sqrt{\Gamma}$；`continuum_root_total` 为近阈值剩余部分 |
| `low_spectrum_comparison.csv`、`figure2_comparison.csv` | 原求解与孤立求解对比：`old_*`/`new_*` 的通道、根、`Delta`、`B`；`abs_delta`；`relative_B` 为比值（不是百分数）；`same_3dp` |
| `free_theory_reference.csv` | 四个核心系数的近自由点检验：精确值、数值及其比值 |

### 术语表

| 列 | 取值 | 含义 |
| --- | --- | --- |
| `kind` | `有符号 λ_iso` | 带符号的 $\lambda_{\rm iso}$ |
| `kind` | `\|λ_iso\|，相位未定` | 只有模长，相位未定 |
| `copy_check` | `核心窗口逐N有副本` | 核心窗口内每个尺寸都有独立对称副本 |
| `copy_check` | `仅部分N有副本` | 只有部分尺寸有副本 |
| `copy_check` | `核心窗口无独立副本` | 核心窗口内没有独立副本 |

## 已被取代和分版本的文件

| 文件 | 状态 |
| --- | --- |
| `comparison/bootstrap_ab_ope_components.csv` | 11 月 6 日的首分量；附录表使用 `bootstrap_complete_root_weights.csv` |
| 旧说明中的 0.203064 与 0.349994 | 未孤立应力张量时的首分量与完整根 $\phi\phi$ 应力幅度；稿件采用孤立值 0.349770 |
| ver4 完整根权重（141 项，$\beta$） | 11 月 9 日起由孤立应力求解的权重取代；ver4 的 Spectrum 与矩阵仍在 `bootstrap/efm_v3/Skydiving_ver4/` |
| `fuzzy_sphere/spectra/v055/`、`fuzzy_sphere/ope/v055/` | 修复盲分析代码后的复跑，与稿件目录分开保存 |
