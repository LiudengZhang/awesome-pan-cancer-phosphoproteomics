# benchmarKIN

**Verdict:** The most comprehensive benchmark of kinase activity inference methods -- the key takeaway is humbling: no single method dominates, and the field lacks a reliable ground truth.

**Citation:** Tsafou K, Vetter JS, Gjerga E, et al. "Comprehensive benchmark of kinase activity inference methods." *Briefings in Bioinformatics* 25(1):bbad466 (2024). [DOI: 10.1038/s41467-025-59779-y](https://doi.org/10.1038/s41467-025-59779-y)

## Problem Setup

Multiple methods exist for inferring kinase activity from phosphoproteomics data (KSEA, ULM, VIPER, z-score, mean substrate phosphorylation, etc.), each claiming good performance. But performance claims are tested on different datasets with different metrics. benchmarKIN asks: when all methods are evaluated on the same datasets with the same criteria, which performs best?

## Approach

Systematic comparison of 11 kinase activity inference methods across multiple benchmark datasets. Benchmark types include: (1) perturbation datasets where a specific kinase is inhibited or activated and the expected activity change is known; (2) correlation with protein-level kinase abundance as a proxy for activity; (3) clinical datasets where pathway activation status is clinically annotated. Methods compared include KSEA, z-score, ULM, MLM, VIPER, GSVA, mean phosphorylation, weighted sum, and others. Performance measured by recovery of the perturbed kinase (perturbation benchmarks) and correlation with expected activity (clinical benchmarks).

## Key Findings

- No single method consistently outperforms all others across all benchmarks and kinase families.
- Simple methods (mean substrate phosphorylation, z-score) perform surprisingly competitively with complex methods (VIPER, MLM).
- Prior knowledge source (which kinase-substrate database is used) has a larger effect on performance than method choice.
- Performance varies dramatically across kinases -- well-studied kinases with many known substrates (e.g., CDKs, MAPKs) are inferred reliably; kinases with few known substrates fail regardless of method.
- Consensus or ensemble approaches (running multiple methods and aggregating) tend to be more robust than any single method.

## Evaluation

Multiple independent benchmark datasets spanning kinase inhibitor treatments, genetic perturbations, and clinical annotations. Methods ranked by area under the ROC curve (AUROC) for perturbation recovery and by correlation for quantitative benchmarks. Sensitivity analysis to prior knowledge source (PhosphoSitePlus vs. OmniPath vs. KinaseLibrary-derived networks).

## Honest Assessment

**Strengths:**

- Fills a critical gap -- the field needed a head-to-head comparison under controlled conditions.
- Transparent methodology with all code and data available for reproduction.
- The finding that prior knowledge matters more than method is actionable and important.
- Highlights the substrate coverage problem honestly: methods fail when substrate annotations are sparse.

**Limitations:**

- Benchmark datasets are dominated by well-studied kinases (AKT, ERK, CDK) and well-characterized inhibitors, so conclusions may not generalize to the long tail of the kinome.
- "Ground truth" in perturbation experiments is imperfect -- kinase inhibitors have off-target effects, and genetic perturbations trigger compensatory signaling.
- The benchmark does not test performance on clinical outcome prediction, which is arguably the most relevant downstream application.
- Some methods are tested with default parameters rather than optimized settings, which may disadvantage more tunable approaches.

**Design Decision:** Standardize the evaluation rather than propose a new method. This is the right contribution at the right time -- the field was drowning in methods without a way to compare them. The uncomfortable finding that simple methods work nearly as well as complex ones should redirect effort toward better prior knowledge rather than more sophisticated statistics.
