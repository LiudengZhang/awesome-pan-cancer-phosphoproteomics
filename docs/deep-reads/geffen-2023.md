# Geffen 2023

**Verdict:** The definitive CPTAC phosphoproteomics atlas -- sets the standard for pan-cancer phospho analysis but inherits all the limitations of bulk tumor profiling.

**Citation:** Geffen Y, Anber M, Batlle E, et al. "Pan-cancer proteogenomics connects oncogenic drivers to functional states." *Cell* 186(17):3502-3521.e25 (2023). [DOI: 10.1016/j.cell.2023.07.014](https://doi.org/10.1016/j.cell.2023.07.014)

## Problem Setup

How do oncogenic mutations translate into functional cellular states across cancer types? Genomics catalogs driver mutations, but the phosphoproteome captures what those mutations actually do to signaling. This study asks whether pan-cancer phosphoproteomic data can reveal convergent kinase programs and druggable dependencies that genomics alone misses.

## Approach

The study profiles 110,274 phosphosites across 1,110 tumors spanning 10 CPTAC cancer types (breast, ovarian, endometrial, colon, lung adenocarcinoma, lung squamous, head and neck, glioblastoma, renal clear cell, pancreatic ductal adenocarcinoma). Kinase activity inference uses substrate-based scoring. Tumors are stratified into phospho-based subtypes via consensus clustering on kinase activity scores. Integration with matched genomic, transcriptomic, and proteomic data connects driver mutations to downstream phospho-signaling states.

## Key Findings

- Convergent kinase activity programs emerge across cancer types -- tumors with different driver mutations can activate the same kinase modules.
- Phospho-based subtypes capture clinically relevant biology not visible in genomic or transcriptomic subtypes alone.
- Specific kinase dependencies (CDK, MAPK, PI3K/AKT/mTOR axes) are druggable and stratify patients beyond standard molecular classifications.
- Driver mutations show variable penetrance at the phospho level -- the same mutation does not always produce the same signaling outcome.
- Immune and stromal microenvironment features correlate with distinct kinase activity patterns.

## Evaluation

Validated across all 10 CPTAC cohorts with matched multi-omics. Phospho subtypes assessed for survival associations and pathway enrichment. Kinase activity scores benchmarked against known biology (e.g., EGFR mutations driving EGFR kinase activity). No independent external validation cohort outside CPTAC.

## Honest Assessment

**Strengths:**

- Largest pan-cancer phosphoproteomics dataset to date with rigorous multi-omics integration.
- Demonstrates that phospho data adds non-redundant clinical information beyond genomics.
- Publicly available data enables downstream reanalysis.
- Systematic kinase activity inference across cancer types in a unified framework.

**Limitations:**

- Bulk tumor profiling obscures cell-type-specific signaling -- stromal and immune phospho signals are confounded with tumor-intrinsic signals.
- Missing data is substantial; phosphosite quantification across 10 cancer types requires aggressive imputation.
- Phospho subtypes lack prospective clinical validation.
- TMT-based quantification has known ratio compression issues that may attenuate real biological differences.

**Design Decision:** Breadth over depth. By spanning 10 cancer types, the study gains power for cross-cancer comparisons but sacrifices per-tumor resolution. This is the right bet for an atlas paper -- the field needed a comprehensive map before it could ask targeted questions.
