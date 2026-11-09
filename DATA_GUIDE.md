# Data guide

English | [简体中文](DATA_GUIDE.zh-CN.md)

This guide maps the manuscript's tables and figures to the archived files and defines the columns of the files used directly in the manuscript. The [README](README.md) describes the archive layout and normalization conventions. Raw inputs under `fuzzy_sphere/raw/` are described by the `meta.json`, `*_meta.json` and `checkpoints.toml` files in their directories.

## Getting the files

Some file names exceed 150 characters. On Windows, enable long paths before cloning, or clone into a short directory such as `C:\d`. Otherwise Git can stop the checkout with missing files.

```bash
git clone -c core.longpaths=true https://github.com/dantengs/dqcp-vst-mixing-data.git
```

```bash
sha256sum -c SHA256SUMS
```

`manifests/file_manifest.csv` gives the size, SHA-256 and local origin of every archived file except itself, the two READMEs, the two guides, `SHA256SUMS` and the Git configuration files.

## Manuscript items

| Manuscript item | File | Selection |
| --- | --- | --- |
| Table I, bootstrap column | `bootstrap/efm_v3/Skydiving_ver4/Spectrum_*.m` | lowest root in the channel; the external $\phi,s,t$ dimensions are the first three numbers in the file name |
| Table I, $N=12$ column | `fuzzy_sphere/spectra/manuscript/n12_two_scheme_levels.csv` | `A_publication == "P"`, lowest or second-lowest in `(rep, L, P)` |
| Table II (revised $N=10$ assignments) | `fuzzy_sphere/spectra/manuscript/additional_primary_continuations.csv`, `n10_zhou_tableVI_comparison.csv`, `comparison/n10_unresolved_bootstrap_candidates.csv` | `Delta_N10`; bootstrap: nearest nonboundary root with $B\ge0.01$ |
| Table III (OPE), bootstrap | `comparison/core_ope_coefficients_published.csv`; ratios from `comparison/bootstrap_cutoff_candidates.csv` | `source == mixed_L23_Skydiving_ver4` |
| Table III, fuzzy sphere | `fuzzy_sphere/ope/manuscript/scalar_insertion_routes.csv` (ratios); `comparison/core_ope_coefficients_published.csv` (J, T) | `N = 10, 11, 12`; $N=12$ current from `fuzzy_sphere/ope/current_n12/manuscript_value.json` |
| Table III, $1/N\to0$ column | `comparison/table3_finite_size_extrapolation.csv`, input `comparison/table3_finite_size_series.csv` | `N_min = 8`, `N_max = 12` |
| Tables V, IX, X (candidate coordinates, cutoff dependence, gap sensitivity) | `comparison/bootstrap_cutoff_candidates.csv` | rows by `Lambda`, `next_tensor_gap` |
| Table VI (tuned singlet sequence) | `comparison/singlet_tuned.csv` | all rows |
| Table XI (141 complete root weights) | `comparison/bootstrap_complete_root_weights.csv` | all rows |
| Table XII (18 additional primary families) | `fuzzy_sphere/spectra/manuscript/additional_primary_continuations.csv` | all rows |
| Table XIII (complete $N=12$ catalogue, 264 levels) | `fuzzy_sphere/spectra/manuscript/n12_two_scheme_levels.csv` | all rows; label `A_publication` |
| Table XIV (OPE conversion factors) | `comparison/fs_to_bootstrap_conversion_factors.csv` | `allowed == True` |
| Fig. 2 | `comparison/figure2_points.csv`; dashed markers `comparison/figure2_unresolved_weights_ver4.csv` | all rows |
| Fig. 4 (conformal checks) | `comparison/figure4a_order_parameter_points.csv`, `figure4b_spacing.csv`, `figure4c_raising.csv` | all rows |
| Figs. 5 and 6(b) (fixed-coupling singlet) | `comparison/fixed_coupling_singlet.csv` | `panel` a or b |
| Fig. 6(a) | `comparison/singlet_tuned.csv` | all rows |
| Isolated stress tensor (Appendix A.3) | `bootstrap/efm_v3/isolated_stress_20261109/stress_coefficients.csv` | `external_pair` |
| Primary counts in the text | `fuzzy_sphere/spectra/manuscript/primary_counts.csv` | by `N` and `window` |

Table and figure numbers refer to the manuscript of 9 November 2026 and can change with float placement. Identify an item by its content if the numbers differ.

## Identifiers

**Bootstrap channels.** The solver files use $SO(6)$-style labels. The `source_sector` strings such as `S+, l=2` combine the label, the spin class and the spin.

| Solver label | `S` | `V` | `A` | `T` | `50` | `64` | `S84` | `S105` | `175` |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| $SO(5)$ representation | **1** | **5** | **10** | **14** | **30** | **35** | **35′** | **55** | **81** |

`+` and `-` denote even- and odd-spin channels, not parity. The physical parity is $-$ for **5**, **30** and **35** (the $s\phi$ and $t\phi$ channels) and $+$ otherwise. `V$theta` holds the fixed external normalization $\beta_{\phi\phi t}=1.0858374$. A `Spectrum` entry `{Delta, {b_1, b_2, ...}}` lists amplitudes in the external-pair order of the manuscript's channel table. A root with several retained components appears as several entries with the same `Delta`.

**Fuzzy-sphere levels.** `phys_level_key = N<N>:C<C2>:L<L>:P<±1>:<E>` identifies a raw level by size, Casimir, spatial spin, physical parity and raw energy. A key ending in a dimension, such as `N12:C3:L3:P-1:4.426230`, identifies a projected mode. `C2` uses the normalization $C_2(\mathbf 5)=2$. It gives 0, 2, 3, 5, 6, 8, 9, 10, 12, 14 for **1, 5, 10, 14, 35, 35′, 30, 81, 105, 55**. `rep = 35p` and `35'` denote **35′**. A label such as `C2=15{84|154}` means the Casimir does not fix the representation. `block = s<a>_s<b>_L<L>` gives the two internal spins and $L$. `X` is the segment-exchange parity, with `0` for blocks without that symmetry.

**Classification.** Strict primaries satisfy $w_P\ge0.90$ for $\kappa_c/3$, $\kappa_c$ and $3\kappa_c$, with consistent symmetry copies and stable retained windows.

## Column definitions

### `comparison/`

| File | Columns |
| --- | --- |
| `bootstrap_complete_root_weights.csv` | `AB` external pair; `representation_tex`, `spin`, `Delta` exchanged root; `source_sector`, `source_root_index` position in the Spectrum file; `amplitude_squared` $=\Gamma_{AB,AB}=\sum_a\beta_{AB,a}^2$ in the mixed-crossing convention; `imposed_gap` root fixed by a gap or unitarity bound; `provisional` stress root; `display` value printed in the appendix; `kept_components` number of retained components |
| `bootstrap_ab_ope_components.csv` | 6 November snapshot: the leading component only (`amplitude`, `amplitude_squared`). Use `bootstrap_complete_root_weights.csv` for the current appendix table. |
| `bootstrap_cutoff_candidates.csv` | `Lambda`; `next_tensor_gap` $g_t$; optimized `Delta_phi`, `Delta_s`, `Delta_t`; scan ratios $\beta_{\phi\phi s}/\beta_{\phi\phi t}$, $\beta_{ttt}/\beta_{\phi\phi t}$, $\beta_{stt}/\beta_{\phi\phi t}$, $\beta_{sss}/\beta_{\phi\phi t}$ |
| `core_ope_coefficients_published.csv` | `source`; `N` and `insertion` for fuzzy-sphere rows; `quantity` ($\phi\phi s$, $\phi\phi t$, $\phi\phi J$, $\phi\phi T$); `beta_vst` mixed-crossing value; `vst_to_published_factor`; `lambda_published` in the convention of LiShen2026 Table II; `kind` (`coefficient`, `complete_root_total`, `finite_size_coefficient`) |
| `table3_finite_size_extrapolation.csv` | `quantity`; fit window `N_min`–`N_max`; `intercept_a`, `slope_b` of $a+b/N$; `max_abs_residual`; `quadratic_fit_intercept` of $a+b/N+c/N^2$ for comparison; `displayed_in_table3` |
| `table3_finite_size_series.csv` | `N`; `phiphi_J`, `phiphi_T` in the published convention from $\phi$ insertion |
| `figure2_points.csv` | `method`; `N`; `rep`; `L`; `P`; `Delta`; `B` bootstrap amplitude norm; `kind` (`strong` $B\ge0.10$, `weak` $0.01\le B<0.10$, `external`, `primary`, `unresolved`); `source_id` bootstrap `sector:root` or fuzzy-sphere key; `track_id`; `x` plotted abscissa. The stress point uses the norm of its leading component (2.477; complete root 2.576), which does not change its marker. |
| `figure2_unresolved_weights_ver4.csv` | the five dashed levels: `w_primary`, `w_descendant` at $\kappa_c$, `w_primary_thr_lo/hi` at $\kappa_c/3$ and $3\kappa_c$; `window_status`; `nearest_bootstrap_Delta`, `absolute_distance`, `relative_distance_percent` |
| `figure4a_order_parameter_points.csv` | `N`, `g`, `sqrt_N_m2` $=N^{1/2}\langle m_i^2\rangle$ |
| `figure4b_spacing.csv` | `branch` (`dphi`, `dt`, `curlJ`, `dJ`), `N`, `value` $=\epsilon_{\mathcal O,1}$ |
| `figure4c_raising.csv` | `branch` (`phi`, `t`, `stress`), `N`, `value` $=\mathcal C_{\mathcal O}$ |
| `fixed_coupling_singlet.csv` | `panel` (`a` scan in $g$, `b` sequence in $N$); `N`; `g`; `x` plotted abscissa; `value` $=\Delta_s^{\rm eff}$; `evidence`: `A` anchored at $g_*$ with a dominant same-basis overlap, `L` anchored through an accepted chain of adjacent overlaps |
| `singlet_tuned.csv` | `N`; `g` $=g_*(N)$; raw energies `E0`, `E_S`, `E_J`, `E_stress`; `alpha` $=2/(E_J-E_0)$; `Delta_S`; `Delta_stress_check` |
| `n10_unresolved_bootstrap_candidates.csv` | candidate roots for the two unresolved $N=10$ rows, ordered by `distance_rank`; `selected` marks the printed root |
| `conversion_factors_key.csv`, `vsinglet_vst_by_rep.csv`, `fs_to_bootstrap_conversion_factors.csv` | conversion factors with exact (`*_exact`) and numerical (`*_numeric`) forms. See the README. |

### `fuzzy_sphere/spectra/manuscript/`

| File | Columns |
| --- | --- |
| `n12_two_scheme_levels.csv` | `phys_level_key`, `block`, `raw_index`, `rep`, `L`, `P`, `C2`, `X`, `Delta`. `A_*` is the manuscript classification: `A_publication` (`P`, `D`, `-`), `A_detail` (`P` primary, `D` descendant, `M` mixed, `W` window-sensitive, `R` primary resolved from a distributed mode, `F` incomplete family coverage), `A_reviewed_class`, `A_window_status`, weights `A_wP`, `A_wD`, `A_parent_weight`. `B_*` is the independent bounded-switch cross-check: `B` (`P`, `D`, `M`, `U` uncovered, `S` method-dependent, `V` vacuum, `X` no scheme-B record), `B_status`, `B_Psupport`, `B_mode_Delta`, `B_mode_sigma_Delta` and the switch labels. |
| `n12_two_scheme_transitions.csv` | counts of `A_publication` (rows) against `B` (columns) |
| `n12_two_scheme_distributed_modes.csv` | the 13 primary directions spread over several raw levels: `mode_delta`, energy-basis width `sigma_delta`, `components` (`#index:Delta:weight`) |
| `n12_reviewed_raw_levels.csv` | the manuscript $N=12$ labels by stage (`classes_v035`, `revised_class`, `reviewed_class`) |
| `n10_n11_formal_low_spin_spectrum.csv` | the same level fields for $N=10,11$; `derived_reviewed_class_N12_priority` applies the $N=12$ rules and gives the published counts; `w_primary_thr_lo/hi` at $\kappa_c/3$ and $3\kappa_c$; `parent_*` and `primary_*` link descendants and modes to tracks |
| `n10_zhou_tableVI_comparison.csv` | the 129 rows of Zhou et al. Table VI: printed values (`paper_*`, `paper_PD` blank where unassigned) and the present labels (`current_label` `P`/`D`/`M`, `current_window`) at the 0.90 and 0.85 gates |
| `additional_primary_continuations.csv` | the 18 additional families: `Delta_N10`, `Delta_N11`, `Delta_N12` (empty when no continuation passes), `wP_N10`, `wD_N10`, `paper_class` (blank = unassigned in Zhou et al.) |
| `primary_counts.csv` | strict-primary counts by `N` and dimension `window` |

### `fuzzy_sphere/ope/manuscript/`

| File | Columns |
| --- | --- |
| `scalar_insertion_routes.csv` | mixed-crossing $\beta$ by route: `vvt_t` $\phi\phi t$ with $t$ insertion, `vvt_v` with $\phi$ insertion, `vvs_s`, `vvs_v`, `sss_s`, `stt_s`, `stt_t`, `ttt_t`; ratios `*_over_vvt` divide by `vvt_t`; `*_alt` use the other insertion |
| `representative_ope_routes.csv`, `retained_n5_n11_ope_routes.csv` | `route` insertion (`S` singlet, `T` tensor, `phi` vector); `X`, `Z` endpoint tracks; `rank`; `lambda_iso_N5` … `lambda_iso_N12`; `display_*` names used in the manuscript. `kind` and `copy_check` are in Chinese. See the glossary below. |
| `n12_reviewed_integer_ope.csv` | one row per $N=12$ contraction: `insertion`, `rank`, endpoints `X_*` and `Z_*`, matrix elements `me_*`, `cg_iso`, `normalization_Z_used`, `lambda_iso_signed`, `lambda_3j_blind`; `publishable` and `eligible_strict` select rows usable for comparison |
| `n12_ope_route_identity.csv` | $N=12$ value of each retained route and how it was matched |

### `bootstrap/efm_v3/isolated_stress_20261109/`

| File | Columns |
| --- | --- |
| `stress_coefficients.csv` | `isolated_coefficient` Ward-block value $c\,w$; `original_root_total` $\sqrt{\Gamma}$ of the original $\Delta=3$ root; `continuum_root_total` near-threshold remainder |
| `low_spectrum_comparison.csv`, `figure2_comparison.csv` | original against isolated solve: `old_*`/`new_*` channel, root, `Delta`, `B`; `abs_delta`; `relative_B` as a fraction (not a percentage); `same_3dp` |
| `free_theory_reference.csv` | near-free checks of the four core coefficients: exact values, numerical values and ratios |

### Glossary

| Column | Value | Meaning |
| --- | --- | --- |
| `kind` | `有符号 λ_iso` | signed $\lambda_{\rm iso}$ |
| `kind` | `\|λ_iso\|，相位未定` | modulus only; phase not fixed |
| `copy_check` | `核心窗口逐N有副本` | independent symmetry copy at every size in the core window |
| `copy_check` | `仅部分N有副本` | copies at some sizes only |
| `copy_check` | `核心窗口无独立副本` | no independent copy in the core window |

## Superseded and versioned files

| File | Status |
| --- | --- |
| `comparison/bootstrap_ab_ope_components.csv` | 6 November leading components; the appendix uses `bootstrap_complete_root_weights.csv` |
| The value 0.203064 in older notes | leading-component $\phi\phi$ stress amplitude; the manuscript uses 0.350 |
| `fuzzy_sphere/spectra/v055/`, `fuzzy_sphere/ope/v055/` | rerun with corrected blind-analysis code, kept separate from the manuscript catalogue |
