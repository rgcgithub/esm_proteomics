# Variant Classification Using Proteomics‐Informed Large Language Models Increases Power of Rare Variant Association Studies and Enhances Target Discovery

Paper: Gillies CE, Mbatchou J, Habegger L, et al. Variant Classification Using Proteomics-Informed Large Language Models Increases Power of Rare Variant Association Studies and Enhances Target Discovery. Genetic Epidemiology. Published 3 November 2025. https://doi.org/10.1002/gepi.70023

## Study Background

This work represents the development and application of protein language models for predicting the functional consequences of missense variants in human proteins. Our study leverages the ESM-1b and ESM-1v (Evolutionary Scale Modeling) protein language models, which were trained on millions of protein sequences to learn evolutionary patterns and structural constraints that govern protein function.

### Motivation

Traditional approaches for predicting missense variant pathogenicity often rely on evolutionary conservation scores, structural features, or combinations of multiple prediction algorithms. However, protein language models offer a fundamentally different approach by learning the "grammar" of protein sequences directly from large-scale evolutionary data, potentially capturing subtle functional constraints that may be missed by other methods.

## Overview

Missense variant classifications from protein language models (ESM-1b and ESM-1v), for all possible single-nucleotide missense variants on Ensembl 100 canonical transcripts. Each model is provided in two forms:
- **Standard** (`ESM1b_std`, `ESM1v_std`): direct application of the pretrained model.
- **Proteomics-informed** (`ESM1b_proteomics`, `ESM1v_proteomics`): the model trained with labels from large-scale protein quantitative trait loci (pQTL) studies.

## Classification

Variants are ranked from least to most deleterious across all possible missense variants, giving a rank score from 0 (least deleterious) to 1 (most deleterious). All four methods use the same thresholds:

| Classification | Score Range |
|----------------|-------------|
| **Likely_benign** | 0.00 - 0.34 |
| **Intermediate** | 0.34 - 0.68318 |
| **Likely_deleterious** | 0.68318 - 0.78 |
| **Likely_deleterious_strict** | 0.78 - 1.0 |

- Likely_deleterious_strict (top 22%) was used in the manuscript, where deleterious missense variants were the top 22% scoring variants. The 22% was chosen to match the proportion selected by the 5-method ensemble (SIFT, MutationTaster, LRT, PolyPhen-2 HVAR, PolyPhen-2 HDIV).
- Scores > 0.68318 (Likely_deleterious or Likely_deleterious_strict) match AlphaMissense in the percentage of predicted deleterious missense variants.

## Files

In `scores/`, one file per chromosome (bgzip-compressed, tabix-indexed by chromosome and position): `combined_scores_chr*.deduplicated.reranked.with_variant_classifications.tsv.gz`

### Columns
1. `#chrom`: Chromosome
2. `pos`: Position
3. `variant`: Variant identifier (chromosome:position:reference:alternative)
4. `Ensembl_geneid`: Gene ID (Ensembl 100)
5. `Ensembl_tsid`: Transcript ID (Ensembl 100)
6. `ESM1b_proteomics_variant_classification`: ESM-1b + proteomics
7. `ESM1b_std_variant_classification`: Standard ESM-1b
8. `ESM1v_proteomics_variant_classification`: ESM-1v + proteomics
9. `ESM1v_std_variant_classification`: Standard ESM-1v

A classification is empty when the variant has no score from that method.

## Classification Distribution of ESM-1b+proteomics and standard ESM-1b

|  | | | **Standard ESM-1b Classification** | |
|---------------------------|---------------|--------------|-------------------|---------------------------|
| **ESM-1b + Proteomics Classification**  | **Likely_benign** | **Intermediate** | **Likely_deleterious** | **Likely_deleterious_strict** |
| **Likely_benign** | 20,382,123 | 4,498,136 | 28,889 | 3,464 |
| **Intermediate** | 4,515,654 | 16,939,253 | 2,465,418 | 1,225,041 |
| **Likely_deleterious** | 12,380 | 2,659,745 | 2,138,250 | 2,283,849 |
| **Likely_deleterious_strict** | 2,497 | 1,048,187 | 2,461,667 | 12,606,980 |

## License

This work is licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/deed.en). **Commercial use is not permitted** without explicit permission.
