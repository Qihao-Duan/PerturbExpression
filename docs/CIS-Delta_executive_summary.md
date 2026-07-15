# CIS-Δ — Executive summary & reading guide

**CIS-Δ** is a perturbation-grounded *cis*-regulatory response benchmark prototype: it scores a model's predicted change in expression (**Δ**) from a defined *cis*-intervention against experimental ground truth, across several assay types. It gives the sequence-oracle and generative-DNA communities a shared, non-circular target and a naive-baseline floor to beat. (Scope note: not every axis is single-cell — eQTLs are bulk — and not every axis is native chromatin — satMPRA is an episomal reporter; claims are made per axis.)

> **Status (read this first):** This is a **provisional prototype**. Of the seven scoring axes, **five are established/reference tracks and two are exploratory breadth extensions** (`satmpra`, `sting_seq`); **zero are formally V4-admitted**. satMPRA fails the power gate (~21 elements) and STING-seq fails the overlap gate for independent validation (115/124 genes overlap the anchor), so both are exploratory tiers, not benchmark axes. Model scoring on the frozen truth unlocks only after the scoring analysis plan (SAP) is signed. "Hackathon-ready" here does **not** mean "paper-ready" — the paper path is enumerated at the end.

---

## The finding in one paragraph

Across every model architecture tested — Borzoi, Enformer, AlphaGenome (2026 state of the art), Evo2, scooby — sequence oracles show a **calibration/coverage gap**. On distal enhancers a model can see, it recovers perturbation *direction*; but (i) most real regulatory links fall outside the receptive field (**71%** out for Borzoi, **88%** for Enformer), (ii) aggregate performance collapses to chance once promoter-proximal controls are included, and (iii) **on the pooled K562 CRISPRi set a naive distance-to-TSS baseline out-ranks Borzoi and Enformer** (AUROC **0.868** vs pooled oracle at/near chance). The gap **recurs in four non-K562 cell types**, and on natural variation the oracle is out-ranked by **fine-mapping PIP** (0.688 vs 0.624) — though PIP is an *outcome-informed reference*, not a sequence-only baseline (it sees the same genotype–expression association we score against). Cell-type-matched readout tracks recover direction (sign agreement 0.58 → 0.79) but leave receptive-field and distance-dominance untouched — isolating what is *fixable* (readout) from what is *architectural* (context length, effective range).

## The perturbation-response angle

CIS-Δ is organized along the **perturbation-response** dimension — the signed, quantitative Δ from a defined intervention. Its breadth is **axis diversity** (CRISPRi repression, CRISPRa activation, reporter-MPRA variant effects, natural variation, cross-screen concordance) under one Δ metric — not dataset count.

## The seven scoring axes

| Axis | Assay | Modality | Independent unit | Status |
|---|---|---|---|---|
| `gasperini_dhs` | Gasperini 2019 K562 CRISPRi | repression | ~30 distal-DHS loci | established |
| `eqtl_geuvadis` | GEUVADIS LCL eQTL | natural variation | 1,826 variants | established |
| `eqtl_gtex` | GTEx whole-blood eQTL | natural variation | 1,800 variants | established |
| `multitissue` | GTEx 4-tissue eQTL | natural variation | 5,619 pairs | established |
| `promoter_crispra` | Chardon 2024 CRISPRa | activation | 18 loci (10 resp.) | established |
| `satmpra` | Kircher/Ahituv sat-mut MPRA | reporter variant effect | 21 elements | **exploratory** |
| `sting_seq` | STING-seq GWAS sc-CRISPRi | repression (GWAS cCRE) | 124 genes / 30 concordant | **exploratory** |

All seven round-trip in `code/score_submission.py --selftest` to <1e-6 from committed fixtures.

## Reading guide to the manuscript (`CIS-Delta_paper.pdf`)

- **§1–3** — motivation, the benchmark definition, and Table 1 (the seven axes). *Start here.*
- **§4** — the Gasperini anchor, verified from the file (90,955 pairs).
- **§5.1–5.3** — the reference result and the central finding (**the core**).
- **§5.6–5.8** — cross-cell-type replication + the fixable/architectural separation.
- **§5.9, §5.11** — up-regulation (CRISPRa) and natural variation (eQTL) breadth.
- **§5.16–5.17** — AlphaGenome and Evo2 (the gap survives the state of the art).
- **§5.21–5.22** — the two exploratory breadth axes, with their statistical caveats stated in-line.
- **§6–7** — discussion, honest limitations, and the two-timescale conclusion.

## Load-bearing claims (and the ones we deliberately do *not* make)

- **We claim:** oracle > distance on the visible DHS stratum; distance > oracle pooled; fine-mapping PIP > oracle on eQTLs (p=5.2e-4); the gap replicates and survives AlphaGenome.
- **We do NOT claim:** that AlphaGenome beats Borzoi (edge is n.s. on both eQTL cohorts — DeLong p≈0.08 GEUVADIS, p=0.40 GTEx); that the two exploratory axes are validated; that the leaderboard is a secure/hidden-holdout benchmark (public truth, fittable — governance-gated).

## Paper path (post-hackathon)

1. Element-cluster-aware inference for `satmpra`; gene-cluster-aware inference for `sting_seq`.
2. Fix `satmpra` magnitude-AUROC treatment of non-significant rows (currently unknown-as-negative).
3. Model-exposure audit; lock environment + data versions.
4. Living-leaderboard auto-ingest; a hidden evaluation holdout.
5. Independent statistician + biologist review; **sign the scoring SAP only after** the estimands, labels, independent units, and inference procedures above are corrected.

---

*Deliverables: manuscript `CIS-Delta_paper.{md,html}` · slide deck `CIS-Delta_hackathon_deck.html` · speaker notes `CIS-Delta_hackathon_speaker_notes.md` · scorer `code/score_submission.py` · leaderboard `docs/leaderboard.{md,html}`. Repo: github.com/Qihao-Duan/PerturbExpression (latest commit on main).*
