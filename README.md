
# Variant Classification Using Proteomics‐Informed Large Language Models Increases Power of Rare VariantAssociation Studies and Enhances Target Discovery

## Study Background

This work represents the development and application of protein language models for predicting the functional consequences of missense variants in human proteins. Our study leverages the ESM-1b (Evolutionary Scale Modeling 1b) protein language model, which was trained on millions of protein sequences to learn evolutionary patterns and structural constraints that govern protein function.

### Motivation

Traditional approaches for predicting missense variant pathogenicity often rely on evolutionary conservation scores, structural features, or combinations of multiple prediction algorithms. However, protein language models offer a fundamentally different approach by learning the "grammar" of protein sequences directly from large-scale evolutionary data, potentially capturing subtle functional constraints that may be missed by other methods.

### Study Design

We computed two complementary scoring approaches using the ESM1b model:
1. **Standard ESM-1b scoring** (`ESM1b_std_variant_classification`): Direct application of ESM1b likelihood scores
2. **Proteomics-informed ESM-1b scoring** (`ESM1b_proteomics_variant_classification`): ESM1b scores enhanced with proteomics training

The proteomics-informed approach incorporates additional biological context from large-scale protein quantitative trait loci (pQTL) studies, allowing the model to learn patterns that are specifically relevant to protein function as measured through proteomic assays.

### Classification Framework

Both scoring methods classify missense variants into four categories based on predicted functional impact:
- **Likely_benign**: Variants predicted to have minimal functional impact
- **Intermediate**: Variants with uncertain or moderate predicted impact  
- **Likely_deleterious**: Variants predicted to have significant functional impact
- **Likely_deleterious_strict**: Variants predicted to have severe functional impact


#### Classification Thresholds
The script applies the following thresholds to both ESM1b scoring methods:

| Classification | Score Range |
|----------------|-------------|
| **Likely_benign** | 0.00 - 0.34 |
| **Intermediate** | 0.34 - 0.68318 |
| **Likely_deleterious** | 0.68318 - 0.78 |
| **Likely_deleterious_strict** | 0.78 - 1.0 |


### Clinical and Research Applications

These classifications can be used for:
- Prioritizing variants in genetic studies and clinical sequencing
- Understanding the functional spectrum of human genetic variation
- Informing burden testing strategies in association studies
- Guiding experimental validation efforts

### Output Files
- **Path**: `scores/combined_scores_chr*.deduplicated.reranked.with_variant_classifications.tsv`
- **Format**: Compressed TSV with tabix index
- **Compression**: bgzip
- **Index**: tabix (chromosome, position-based)

### Output Columns
1. `#chrom`: Chromosome
2. `pos`: Position
3. `variant`: Variant identifier
4. `Ensembl_geneid`: Gene ID (Ensembl 100)
5. `Ensembl_tsid`: Transcript ID (Ensembl 100)
6. `ESM1b_proteomics_variant_classification`: ESM-1b Proteomics-based missense variant classification
7. `ESM1b_std_variant_classification`: Standard ESM-1b missense variant classification

## Classification Distribution of ESM-1b+proteomics and standard ESM-1b

|  | | | **Standard ESM-1b Classification** | |
|---------------------------|---------------|--------------|-------------------|---------------------------|
| **ESM-1b + Proteomics Classification**  | **Likely_benign** | **Intermediate** | **Likely_deleterious** | **Likely_deleterious_strict** |
| **Likely_benign** | 20,382,123 | 4,498,136 | 28,889 | 3,464 |
| **Intermediate** | 4,515,654 | 16,939,253 | 2,465,418 | 1,225,041 |
| **Likely_deleterious** | 12,380 | 2,659,745 | 2,138,250 | 2,283,849 |
| **Likely_deleterious_strict** | 2,497 | 1,048,187 | 2,461,667 | 12,606,980 |

## License

This work is licensed under the Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0). This license allows for sharing and adaptation of the material for non-commercial purposes with appropriate attribution. Commercial use is not permitted without explicit permission.

**License Details:**
- **Share**: Copy and redistribute the material in any medium or format
- **Adapt**: Remix, transform, and build upon the material
- **Attribution**: You must give appropriate credit and indicate if changes were made
- **NonCommercial**: You may not use the material for commercial purposes

For the full license text, visit: https://creativecommons.org/licenses/by-nc/4.0/deed.en