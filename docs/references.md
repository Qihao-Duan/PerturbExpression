# CIS-Δ — References

Provenance tags: **[R]** retrieved and confirmed in this project's literature
searches / live database checks; **[V]** to verify against primary source before
final submission (cited from background knowledge).

## Datasets used (three, all live-verified this project)
1. **[R]** Gasperini M. et al. *A genome-wide framework for mapping gene
   regulation via cellular genetic screens.* **Cell** 176(1–2):377–390 (2019).
   GEO: **GSE120861** (verified live against NCBI: *Homo sapiens*, 53 samples,
   build hg19). — the CIS-Δ v1 anchor (K562 CRISPRi; deep single-cell axis).
1b. **[R]** Gschwind A.R., Mualim K.S., Karbalayghareh A., Sheth M.U. et al.
   *An encyclopedia of enhancer-gene regulatory interactions in the human genome.*
   **bioRxiv** 2023.11.09.563812 (ENCODE-rE2G). Curated CRISPR benchmark of 10,411
   element–gene pairs; the `EPCrisprBenchmark` held-out non-K562 subset (WTC11,
   HCT116, Jurkat, GM12878; GRCh38) is the CIS-Δ cross-cell-type replication set.
   Repo: github.com/EngreitzLab/CRISPR_comparison.
1c. **[R]** Chardon F.M., McDiarmid T.A. et al. *Multiplex, single-cell CRISPRa
   screening for cell type specific regulatory elements.* **Nat Commun** 15:8209
   (2024). DOI 10.1038/s41467-024-52490-4. SRA **PRJNA1157910**. K562 + iPSC-neuron
   CRISPR-activation; the CIS-Δ up-regulation (positive-Δ) dataset.

## Therapeutic motivation (Casgevy / BCL11A enhancer)
2. **[R]** Frangoul H. et al. *Exagamglogene autotemcel for severe sickle cell
   disease.* **NEJM** — DOI 10.1056/NEJMoa2309676.
3. **[R]** Frangoul H. et al. *CRISPR-Cas9 gene editing for sickle cell disease
   and β-thalassemia* (first-in-human). **NEJM** — DOI 10.1056/NEJMoa2031054.
4. **[R]** Casgevy / exa-cel FDA-approval review. PMC11305803.

## Sequence-to-expression oracles (benchmarked / discussed)
5. **[R]** Avsec Ž. et al. *Effective gene-expression prediction from sequence by
   integrating long-range interactions* (**Enformer**). Nat Methods 18:1196–1203
   (2021). Weights: `EleutherAI/enformer-official-rough` (enformer-pytorch 0.8.12).
6. **[R]** Linder J. et al. *Predicting RNA-seq coverage from DNA sequence at
   single-base resolution* (**Borzoi**). Nat Genet (2025). Weights:
   `johahi/borzoi-replicate-0` (borzoi-pytorch 0.5.1).
7. **[R]** scooby — single-cell-resolution profiles from sequence. PMC11429888 /
   PMC12615262.
8. **[V]** AlphaGenome — variant-effect prediction (DeepMind).

## Enhancer–gene link models (baselines)
9. **[V]** Fulco C. et al. *Activity-by-contact (ABC) model.* Nat Genet (2019).
10. **[V]** ENCODE-rE2G — supervised enhancer–gene link prediction.
11. **[V]** EPInformer — promoter–enhancer expression prediction. Nat Commun
    (exact citation to verify).

## Perturbation benchmark culture
12. **[R]** Arc Virtual Cell Challenge — trans-perturbation prediction benchmark.

## Generative cis-regulatory design (Track B corpora)
13. **[R]** DNA-Diffusion. Nat Genet s41588-025-02441-6.
14. **[R]** D3 (discrete diffusion for regulatory design). PMC13142467.
15. **[R]** SPICE (splicing-element design). PMC12637576.
16. **[R]** AAV / cell-type-specific promoter design. bioRxiv 2026.01.13.699371.
17. **[V]** Gosai S. / Sabeti P. — synthetic-enhancer lentiMPRA sets.

## CRISPRi validity / concordance
18. **[R]** CRISPRi vs. eQTL effect-size concordance. bioRxiv 2025.05.05.651929
    (r ≈ 0.88–0.92 for well-powered CREs).
19. **[R]** TAP-seq. Nat Methods s41592-020-0837-5 (accession GSE135497 — [V]).
20. **[R]** Genome-scale hPSC CRISPRi map. Cell Genomics S2666-979X(25)00332-5.

## Population single-cell eQTL (Track A natural variation, future work)
22. **[V]** OneK1K; Cuomo et al.; Jerber et al. — sc-eQTL cohorts.

## Reference cell atlases / pretraining contexts (future work)
23. **[V]** Arc Virtual Cell Atlas; scBaseCount; Tahoe-100M; X-Atlas/Orion.
