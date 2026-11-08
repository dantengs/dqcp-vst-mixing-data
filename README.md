# SO(5) DQCP VST mixing data archive

English | [简体中文](README.zh-CN.md)

This repository archives the data for the 37-page manuscript snapshot `manuscript_skydive_efm_20261106`, dated 6 November 2026. The manuscript data, the rerun with corrected blind-analysis code, and the original calculation files have separate directories. The [file manifest](manifests/file_manifest.csv) records sources and SHA-256 checksums. The [dataset summary](manifests/dataset_summary.json) identifies each dataset's version and scope.

| Directory | Contents |
| --- | --- |
| [bootstrap/](bootstrap/) | Self-contained Wolfram Notebook for the main mixed-correlator candidate at Λ = 23. It contains 971 spectrum records, one fixed external-normalization record, 1,834 signed OPE components, and the external scaling dimensions and OPE ratios. |
| [fuzzy_sphere/spectra/](fuzzy_sphere/spectra/) | UTF-8 CSV files for the manuscript and v0.5.5 rerun, with separate records for raw levels, projected modes, physical-level classifications, and tracks across sizes. |
| [fuzzy_sphere/ope/](fuzzy_sphere/ope/) | CSV and JSON files. Separate tables hold exact integer-sector contractions, Stage B contractions, and half-integer production routes, with 37,689 rows in total. The manuscript OPE catalogue and the N = 12 current result have their own directories. |
| [fuzzy_sphere/raw/](fuzzy_sphere/raw/) | The 1,447 input files for the v0.5.5 rerun, 458 inputs for the separate N = 12 analysis, 307 authoritative production files, the original current checkpoint bundle, and scan data. |
| [comparison/](comparison/) | Verified data for Figures 2 and 4–6, bootstrap candidate coordinates at different cutoffs, OPE components and conversion factors, and tuned and fixed-coupling singlet sequences. |
| [manifests/](manifests/) | File checksums, provenance, rerun records, and storage locations and verification records for external checkpoints. |

## Data conventions

- **Bootstrap.** Evaluate the data-loading cell in the Notebook first, then the relevant `Dataset` cell. Decimal strings preserve the full precision. Each spectrum record gives the external-pair order and flags imposed gaps and provisional amplitudes. A common sign change of the entire OPE vector preserves its relative component signs.
- **Fuzzy-sphere spectra.** `N` is the orbital count, `L` is spatial spin, `C2` is the internal Casimir, `P` is physical parity, and `X` is segment-exchange parity. `energy` stores the raw energy, while `Delta` is the dimension calibrated by the gap of the conserved current. Raw levels, projected modes, and tracks across sizes have separate identifiers. `sigma_Delta` is the energy-basis spread. The manuscript N = 12 catalogue contains 264 levels, with 45 strict primaries (including the vacuum), 154 descendants, and 65 unresolved levels.
- **Fuzzy-sphere OPE.** Each route retains the insertion and its rank, endpoint states, normalization, availability flag, and phase convention. We use `lambda_iso` for the isometric Clebsch–Gordan convention and `lambda` for the common mixed-crossing convention. The N = 12 current amplitude in the latter convention is 0.8574003792250015. Its data file records the status of the L = 2 complement-space certificate.
- **Versioned comparisons.** The 76 retained manuscript OPE routes and the 699 aggregated v0.5.5 series are stored separately. The five dashed markers in Figure 2 denote unresolved raw levels. Their nearest bootstrap roots and distances in the archived companion table use ver4.

## OPE conversion factors

The 8 November 2026 conversion table covers 15 external-scalar channels at exchange spin $\ell=0$–$4$, with 52 allowed and 23 Bose-forbidden rows. The CSV uses `v` for $\phi$. Its `tt->35` denotes $\mathbf{35}'$, which is distinct from the $\mathbf{35}$ in `vt->35`. Use `total_STF_to_solver_exact` or `total_STF_to_solver_numeric` on the allowed rows. [Conversion table](comparison/fs_to_bootstrap_conversion_factors.csv)

The compact tables give factors into the fixed-component convention for $s,t,J,T_{\mu\nu}$ and factors from the single-vector crossing to VST by exchanged representation. [Fixed-component factors](comparison/conversion_factors_key.csv) · [Single-vector to VST factors](comparison/vsinglet_vst_by_rep.csv)

For the parsed $\Lambda=23$ Skydiving minS ver4 spectrum, an OPE amplitude in the isometric Clebsch–Gordan convention with a unit spatial symmetric traceless (STF) tensor converts as

$$
|b_{ABR}|=G_{AB\to R}\,|\lambda_{\mathrm{iso,STF}}(A\otimes B\to R)|,
\qquad G_{AB\to R}=\left(\frac{d_R}{d_A d_B}\right)^{1/4}.
$$

Here $d_A,d_B,d_R$ are SO(5) representation dimensions. The spectrum amplitude $b$ is the manuscript's mixed-crossing coefficient $\lambda$. The convolved blocks already include the spatial factor $\ell!/(2\ell-1)!!$, so the additional amplitude factor is 1. The `total_h_to_solver_*` columns take $h=\sqrt{\ell!/(2\ell-1)!!}\,\lambda_{\mathrm{iso,STF}}$ as their input. The rank-$r$ factors $c_r$ in the v0.5.5 table belong to the earlier matrix-element extraction step. [Matrix-element extraction factors](fuzzy_sphere/ope/v055/convention_factors.csv)

For a compatible scalar-leg permutation of a stored route $X\otimes Y\to Z$, carry the invariant amplitude $\sqrt{d_Z}|\lambda_{\mathrm{iso,STF}}(X\otimes Y\to Z)|$ into the bootstrap pairing and divide by $(d_A d_B d_R)^{1/4}$. Keep microscopic insertions separate. Signed comparisons require matched operator phases, internal tensor orientation, and point ordering.

For $\phi\phi T_{\mu\nu}$ the singlet factor is $1/\sqrt{5}$ and the resulting mixed amplitude is $\sqrt{15/2}\,|M_{20}/M_{00}|$. The finite-size values at $N=10,11,12$ are $0.254$, $0.264$, and $0.273$. The parsed ver4 bootstrap amplitude has magnitude $0.203064$ and is provisional. The bootstrap components CSV stores `amplitude` and `amplitude_squared` separately. Optimized external-scalar ratios retain their own denominators. [Fuzzy-sphere routes](fuzzy_sphere/ope/manuscript/) · [Parsed bootstrap components](comparison/bootstrap_ab_ope_components.csv)

For the older single-vector $\phi\phi$ crossing, the internal tensor is $P_R/d_R$, while the mixed convention uses $5P_R/\sqrt{d_R}$. With the same convolved block convention, divide the old squared spectrum amplitudes by $5\sqrt{d_R}$ before taking square roots. This gives divisors $5\sqrt{10}$ for $J$ and $5$ for $T_{\mu\nu}$. The older $\Lambda=23$ Navigator stress value converts to $0.349456$ in the mixed convention. The ver4 pre-projection diagonal estimate near $0.350$ is a separate diagnostic from that job's parsed rank-one amplitude.

## Reading the original files

[Replay inputs](fuzzy_sphere/raw/replay_v055/) and [separate N = 12 inputs](fuzzy_sphere/raw/n12_isolated/) preserve the checked input bytes. Use each `.f64` file with its `meta.json` or export metadata for the shape, layout, state order, and binary checksum. The [file manifest](manifests/file_manifest.csv) maps the archived files to their original locations through `archive_path`, `source_key`, and `local_source`.

The [N = 12 current bundle](fuzzy_sphere/raw/current_n12/n12phiJ.tar) preserves the original small checkpoint files. After extraction, use the bundle's `SHA256SUMS` to verify its 93 members. The [supplemental directory](fuzzy_sphere/raw/current_n12/supplemental/) contains production text files saved later. The [decoded replay directory](fuzzy_sphere/raw/current_n12/decoded_replay/) contains the extracted binary arrays and their metadata.

## External checkpoints

The [checkpoint index](manifests/external_raw_checkpoints.csv) lists 531 payloads with their original paths, archive and member names where available, and payload SHA-256 checksums. The [NAS archive receipts](manifests/external_archive_receipts.json) give the paths, sizes, archive SHA-256 checksums, and verification records for eight NAS archives. The index locates three large windows for the current calculation at their original cluster paths.

Run `sha256sum -c SHA256SUMS` from the repository root to verify the files in this repository.
