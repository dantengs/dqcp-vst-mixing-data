# SO(5) DQCP VST mixing 数据归档

这是作者组的私有归档，对应 2026-11-06 的 37 页稿件 `manuscript_skydive_efm_20261106`。稿件取值、修复后盲分析和原始计算文件分别存放。各文件的来源、完整性校验和版本见 [数据清单](manifests/file_manifest.csv) 与 [快照摘要](manifests/dataset_summary.json)。

| 路径 | 内容 |
| --- | --- |
| [bootstrap/](bootstrap/) | 自包含的 Wolfram Notebook。主 Λ=23 混合候选的 971 条通道谱记录、1 条固定外场归一化记录、1,834 个带符号 OPE 分量，以及外场维数和比值 |
| [fuzzy_sphere/spectra/](fuzzy_sphere/spectra/) | UTF-8 CSV。按稿件和 v0.5.5 复跑分目录，保留原始能级、投影模式、物理能级分类及跨尺寸续接 |
| [fuzzy_sphere/ope/](fuzzy_sphere/ope/) | UTF-8 CSV 和 JSON。整数精确收缩、StageB 收缩、半整数生产路线分表，共 37,689 行逐尺寸路线记录。另列稿件 OPE 目录与 N=12 current |
| [fuzzy_sphere/raw/](fuzzy_sphere/raw/) | v0.5.5 的 1,447 个原始输入、N=12 独立分析的 458 个输入、307 个权威生产文件，以及 current 原始检查点包和原始扫描数据 |
| [comparison/](comparison/) | 已核对的图 2、4–6 数据，bootstrap cutoff 候选坐标、OPE 分量、调谐及固定耦合 singlet 序列 |
| [manifests/](manifests/) | 文件 SHA-256、逐文件来源、复跑记录、重型检查点的外部存放位置和归档校验凭据 |

## 数据约定

- **Bootstrap**。打开 Notebook 后先运行数据读取单元，再运行相应的 `Dataset` 单元。十进制数以字符串保存完整位数。每条谱记录标明外场对顺序、施加的 gap 和暂定幅度。整根向量相位与分量间相对符号应分别处理。
- **球面谱**。`N` 是轨道数，`L` 是空间自旋。`C2` 是内部 Casimir，`P` 是物理宇称，`X` 是段交换量子数。`energy` 与 `Delta` 分别保留原始能量和按当前 gap 定标的维数。投影模式、原始能级与跨尺寸轨迹各有独立身份。`sigma_Delta` 表示能量基展宽。稿件 N=12 目录有 264 行，其中 45 个 strict P（含真空）、154 个 D、65 个未定。
- **球面 OPE**。各路线保留插入算符和秩、端点身份、归一化、可用性与相位字段。等距 CG 约定的 `lambda_iso` 和混合 crossing 的 `lambda` 分列使用。N=12 current 的共同约定幅度是 0.8574003792250015，L=2 补空间证书状态记录在数据文件中。
- **版本和比较**。稿件 76 条保留 OPE 路线和 v0.5.5 的 699 条聚合序列分别存储。图 2 的五条虚线对应未定原始能级。附表的最近根与距离已按 ver4 数据统一。

## 原始文件的读法

`raw/replay_v055/` 和 `raw/n12_isolated/` 保存按字节校验的输入。二进制 `.f64` 文件与同目录的 `meta.json` 或导出元数据配套，形状、布局、态顺序及二进制哈希以对应元数据为准。归档名与运行清单里原路径的对应关系见 `file_manifest.csv` 的 `archive_path`、`source_key` 和 `local_source`。

`raw/current_n12/n12phiJ.tar` 保存原始小型检查点包。解包后可用包内 `SHA256SUMS` 核验 93 个成员。`supplemental/` 是随后保存的生产文本，`decoded_replay/` 是对应检查点的二进制读出，附元数据以便跨工具使用。

## 外部重型检查点

[检查点位置索引](manifests/external_raw_checkpoints.csv) 给出 531 个 payload 的原路径、归档包及成员名、payload SHA-256。八个 NAS 归档包的路径、大小、整体 SHA-256 和既有验证收据见 [NAS 归档凭据](manifests/external_archive_receipts.json)。其中三个 current 相关大窗口的定位为集群上的原始检查点。

从仓库根目录可用 `sha256sum -c SHA256SUMS` 校验入库文件。
