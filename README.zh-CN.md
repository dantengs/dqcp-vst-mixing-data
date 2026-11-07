# SO(5) DQCP VST mixing 数据归档

[English](README.md) | 简体中文

本仓库归档 2026 年 11 月 6 日的 37 页稿件快照 `manuscript_skydive_efm_20261106` 所用数据。稿件数据、修复后的盲分析复跑结果和原始计算文件分别存放。[文件清单](manifests/file_manifest.csv) 记录来源和 SHA-256，[数据摘要](manifests/dataset_summary.json) 记录各数据集的版本与范围。

| 目录 | 内容 |
| --- | --- |
| [bootstrap/](bootstrap/) | 主 Λ = 23 混合相关函数候选点的自包含 Wolfram Notebook。含 971 条谱记录、1 条固定外场归一化记录、1,834 个带符号 OPE 分量，以及外场维数和 OPE 比值。 |
| [fuzzy_sphere/spectra/](fuzzy_sphere/spectra/) | 按稿件和 v0.5.5 复跑分目录保存的 UTF-8 CSV，分别记录原始能级、投影模式、物理能级分类及跨尺寸轨迹。 |
| [fuzzy_sphere/ope/](fuzzy_sphere/ope/) | CSV 和 JSON。整数扇区精确收缩、Stage B 收缩和半整数生产路线分表，共 37,689 行。另有稿件 OPE 目录和 N = 12 current 结果。 |
| [fuzzy_sphere/raw/](fuzzy_sphere/raw/) | v0.5.5 复跑的 1,447 个输入、N = 12 独立分析的 458 个输入、307 个权威生产文件，以及 current 原始检查点包和扫描数据。 |
| [comparison/](comparison/) | 已核对的图 2、4–6 数据，各截断阶数的 bootstrap 候选坐标、OPE 分量，以及调谐与固定耦合的 singlet 序列。 |
| [manifests/](manifests/) | 文件校验值、来源、复跑记录，以及外部检查点的存放位置和验证收据。 |

## 数据约定

- **Bootstrap**。打开 Notebook 后先运行数据读取单元，再运行相应的 `Dataset` 单元。十进制值以字符串保存完整精度。每条谱记录给出外场对顺序，并标记施加的 gap 和暂定幅度。整根 OPE 向量整体变号时，各分量的相对符号保持一致。
- **球面谱**。`N` 是轨道数，`L` 是空间自旋。`C2` 是内部 Casimir，`P` 是物理宇称，`X` 是段交换宇称。`energy` 保存原始能量，`Delta` 保存按守恒流能隙定标的维数。原始能级、投影模式和跨尺寸轨迹使用不同的标识。`sigma_Delta` 表示能量基展宽。稿件 N = 12 目录含 264 个能级，其中 45 个严格 primary（含真空）、154 个 descendant、65 个未定。
- **球面 OPE**。各路线保留插入算符及其秩、端点态、归一化、可用性和相位字段。`lambda_iso` 表示等距 Clebsch–Gordan 约定，`lambda` 表示共同的混合 crossing 约定。后者给出的 N = 12 current 幅度为 0.8574003792250015。L = 2 补空间证书状态见对应数据文件。
- **版本和比较**。稿件保留的 76 条 OPE 路线与 v0.5.5 的 699 条聚合序列分开保存。图 2 的五个虚线标记对应未定原始能级，附表中的最近 bootstrap 根与距离采用 ver4。

## 读取原始文件

[复跑输入](fuzzy_sphere/raw/replay_v055/) 和 [N = 12 独立分析输入](fuzzy_sphere/raw/n12_isolated/) 保留逐字节校验的原始输入。读取 `.f64` 时，请使用对应的 `meta.json` 或导出元数据，确认形状、布局、态顺序及二进制校验值。[文件清单](manifests/file_manifest.csv) 的 `archive_path`、`source_key` 和 `local_source` 记录归档文件与原位置的对应关系。

[N = 12 current 检查点包](fuzzy_sphere/raw/current_n12/n12phiJ.tar) 保存原始小型检查点文件。解包后可用包内 `SHA256SUMS` 核验 93 个成员。[补充目录](fuzzy_sphere/raw/current_n12/supplemental/) 含随后保存的生产文本，[解码复跑目录](fuzzy_sphere/raw/current_n12/decoded_replay/) 含读出的二进制数组及元数据。

## 外部检查点

[检查点索引](manifests/external_raw_checkpoints.csv) 记录 531 个 payload 的原路径、可用的归档包及成员名，以及 payload SHA-256。[NAS 归档凭据](manifests/external_archive_receipts.json) 列出八个 NAS 包的路径、大小、整体 SHA-256 和验证收据。三个用于 current 计算的大窗口在索引中指向集群上的原始路径。

在仓库根目录运行 `sha256sum -c SHA256SUMS` 可校验入库文件。
