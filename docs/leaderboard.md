# CIS-Δ Leaderboard

> **LEGACY / PROVISIONAL.** This generator renders pre-revision artifacts. Its datasets are not V4-admitted, and the output is not a current scientific conclusion.

**CIS-Δ** is a virtual-cell benchmark for the *cis*-regulatory expression response: it scores a method's predicted change in expression (**Δ**) for a *(cell context, cis-sequence intervention)* pair against endogenous single-cell, eQTL, and CRISPR ground truth. The central finding is that sequence oracles show a calibration/coverage gap that holds across architectures — most real regulatory links fall outside their receptive field, and where visible they rarely out-rank a distance-to-TSS prior; on eQTLs they are out-ranked by fine-mapping PIP. This leaderboard ranks every benchmarked model against those baselines, per axis.

*Auto-generated from `results_committed/*.json` on 2026-07-14 00:35 UTC. Do not edit by hand — run `code/gen_leaderboard.py`.*

Baseline rows (distance-to-TSS, fine-mapping PIP, ABC, ENCODE-rE2G) are marked **(baseline)** and ranked inline with the models so oracle-vs-baseline is visible at a glance.


## eQTL — GEUVADIS LCL (QTD000110)

Magnitude-discrimination AUROC on the common in-window set (identical n = 1681; bootstrap 95% CI). Higher = better at ranking large-|effect| eQTLs.

| Rank | Model | AUROC (magnitude) | 95% CI | Sign-agree | Spearman ρ |
|---|---|---|---|---|---|
| 1 | fine-mapping PIP *(baseline)* | 0.688 |  | — | — |
| 2 | AlphaGenome | 0.624 | [0.587, 0.657] | 0.678 | 0.488 |
| 3 | Borzoi | 0.600 | [0.562, 0.630] | 0.585 | 0.269 |
| 4 | distance-to-TSS *(baseline)* | 0.573 |  | — | — |
| 5 | Evo2 | 0.516 | [0.485, 0.552] | 0.474 | -0.065 |

## eQTL — GTEx whole blood (QTD000356)

Cross-cohort replication of the GEUVADIS pattern. The ranked table uses the FAIR COMMON SET (n = 1707) where AlphaGenome and Borzoi score the same pairs: AlphaGenome 0.617 vs Borzoi 0.606, DeLong p = 0.40 (not significant). AlphaGenome's full 1 Mb-eligible AUROC (n = 1772: 0.600, gene-clustered CI shown) is listed in its row label. PIP is an outcome-informed reference, not a sequence-only baseline.

| Rank | Model | AUROC (magnitude) | 95% CI | Sign-agree | Spearman ρ |
|---|---|---|---|---|---|
| 1 | fine-mapping PIP (reference) *(baseline)* | 0.664 | [0.633, 0.696] | — | — |
| 2 | AlphaGenome (official; full-eligible n=1772: 0.600) | 0.617 | [0.565, 0.634] | 0.682 | 0.500 |
| 3 | Borzoi | 0.606 | [0.572, 0.636] | 0.577 | 0.209 |
| 4 | distance-to-TSS *(baseline)* | 0.540 | [0.504, 0.573] | — | — |

## Gasperini K562 CRISPRi — full test set (all element types)

Direction AUROC ranking screen hits vs non-hits by |predicted Δ| over all n = 3789 test pairs (51 hits). The distance ruler and the ABC / rE2G maps out-rank the sequence oracles here.

| Rank | Model | AUROC (hit direction) | 95% CI |
|---|---|---|---|
| 1 | distance-to-TSS *(baseline)* | 0.868 |  |
| 2 | ENCODE-rE2G *(baseline)* | 0.817 |  |
| 3 | ABC score *(baseline)* | 0.806 |  |
| 4 | Borzoi | 0.493 |  |
| 5 | Enformer | 0.368 |  |

## Gasperini K562 CRISPRi — distal-DHS stratum

Direction AUROC on distal DHS enhancers, the stratum where sequence oracles are expected to add value over distance. Per-model n differs with receptive field (shown); values as committed.

| Rank | Model | AUROC (DHS hit direction) | 95% CI | n |
|---|---|---|---|---|
| 1 | Borzoi | 0.873 |  | — |
| 2 | AlphaGenome | 0.845 | [0.733, 0.936] | 1928 |
| 3 | distance-to-TSS *(baseline)* | 0.804 |  | — |
| 4 | Enformer | 0.724 |  | — |
| 5 | Evo2 | 0.513 |  | 2420 |

> Identical-set head-to-head (n = 1109, 43 hits): Borzoi 0.692 [0.615, 0.767] vs AlphaGenome 0.619 [0.519, 0.713]. AlphaGenome's 1 Mb context covers 56.7% of pairs vs Borzoi 524 kb's 30.4%.


## Multi-tissue eQTL — cell-context axis

Does a cell-type-matched track set discriminate that tissue's eQTLs better than a mismatched one? n = 5619 variants, 4 tissues (blood / brain / muscle / skin). Reported for both Borzoi (track-reads) and the official AlphaGenome (native per-tissue heads).

| Quantity | Value |
|---|---|
| Borzoi: matched − mismatched AUROC | 0.595 − 0.592 = 0.0029 |
| Borzoi: per-pair top-1 tissue accuracy | 0.457 (chance 0.441) |
| AlphaGenome: matched − mismatched AUROC | 0.0079 (gene-clustered 95% CI [-0.0013, 0.0175], p = 0.11) |
| AlphaGenome: per-pair top-1 tissue accuracy | 0.484 (chance 0.442; gene-clustered excess +0.042, 95% CI [0.006, 0.077], p = 0.024; 707 rows span 642 genes) |
| Cross-track-set pred. corr (median off-diag) | Borzoi 0.820 / AlphaGenome 0.662 |
| Measured β cross-tissue Pearson (ground-truth ceiling) | 0.925–0.959 |

**Verdict.** Benchmark-axis identifiability failure, not a demonstrated architectural limit: the matched-head advantage is small and uncertain (AlphaGenome +0.008, gene-clustered CI crosses 0; per-pair top-1 gene-clustered excess +0.042, 95% CI [0.006, 0.077], p=0.024 — modestly above chance), and the ground truth itself carries almost no tissue-specific signal (cross-tissue β correlated 0.93–0.96).


## Promoter CRISPRa activation (Chardon 2024)

Locus-level agreement between promoter-ablation direction and CRISPRa responsiveness. n = 626 guide pairs over 18 loci (K562 + neuron).

| Quantity | Value |
|---|---|
| Ablation-direction agreement, pooled activatable loci | 0.400 |
|   — K562 | 0.000 |
|   — neuron | 0.800 |
| CRISPRi in-window reference (context) | 0.790 |

**Verdict.** Direction agreement is cell-type-dependent (neuron 0.80, K562 0.00) and below the CRISPRi in-window reference (0.79): promoter-activation direction is only partially captured.


## Reporter variant-effect (bidirectional single-base MPRA) — Kircher/Ahituv 2019

Sign agreement on significant single-base edits (the one BIDIRECTIONAL axis: 2948 activating / 4376 repressing of 7324 significant, 31287 scored, 21 elements). Episomal MPRA reporter (not genomic editing); effects RECONSTRUCTED from GEO raw counts w/ authors' model — exploratory tier, not V4-admitted.

| Quantity | Value |
|---|---|
| Sign agreement, significant edits (random baseline) | 0.495 |
|   chance reference (bidirectional) | 0.500 |
| Magnitude AUROC: |pred| separates significant edits (random baseline) | 0.505 |
| Majority-class-sign baseline | 0.597 |

**Verdict.** Harness live; the seeded RANDOM baseline sits at chance (0.50) as it must, confirming the axis discriminates direction. A real oracle must beat 0.50 here — the direction test the CRISPRi axes are degenerate for. CAVEAT: the independent unit is the element (~21), not the significant-variant count — variant-level CIs are optimistically narrow, so the scorer now reports element-clustered CIs; the binding limit is the element count (~21). Model scoring gated on the signed SAP.


## GWAS-variant single-cell CRISPRi — STING-seq (Morris 2023, K562)

Direction recovery on the published significant-links subset (168 links / 123 genes; 158 repressive / 10 activating). Exploratory tier (cross-screen concordance, not independent validation), not V4-admitted.

| Quantity | Value |
|---|---|
| Sign agreement (distance-prior baseline) | 0.940 |
| Majority-class-sign baseline (predict-all-repressive) | 0.940 |

**Verdict.** The truth is ~94% repressive, so the distance prior EXACTLY equals the majority-class baseline (both 0.940): it adds nothing. A submission is only meaningful if it beats the majority-class-sign baseline. Model scoring gated on the signed SAP.


## Historical fixture contract

1. Produce one submission file per axis — a table keyed by that axis's `pair_id` with your predicted `pred_delta` (four `pred_delta_<tissue>` columns for the multi-tissue axis). See the submission format spec (published with the dataset release) for the full contract, dtypes, sign conventions, and worked examples.
2. Score it with the official harness:

   ```bash
   python code/score_submission.py \
       --submission my_preds.csv --axis eqtl_geuvadis \
       --model-name MyModel --out my_scored.json
   ```

3. `python code/score_submission.py --selftest` round-trips the committed legacy fixtures under the explicit portable numerical contract.
4. Do not submit results for a public leaderboard until Gate C authorizes an admitted release.

