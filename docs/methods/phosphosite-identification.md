# Phosphosite Identification Methods

**Phosphosite identification is the foundational step in phosphoproteomics, converting raw mass spectra into confident phosphopeptide assignments with localized modification sites.**

## Key Methods

### MaxQuant
- **Paper:** [Nature Biotechnology, 2008](https://doi.org/10.1038/nbt.1511)
- **Web:** [maxquant.org](https://www.maxquant.org/)
- **Approach:** Andromeda search engine with probabilistic phosphosite localization via the PTM score. Processes DDA data with label-free or SILAC quantification.
- **Key innovation:** Integrated phosphosite localization scoring within a complete proteomics pipeline; match-between-runs reduces missing values.
- **Strengths:** Gold standard for DDA phosphoproteomics; large user community; extensive documentation; well-validated localization probabilities.
- **Limitations:** Windows-only; slow on large cohorts; DDA acquisition inherently limits depth and reproducibility across samples.

### FragPipe / MSFragger
- **Paper:** [Nature Methods, 2017](https://doi.org/10.1038/nmeth.4256)
- **Code:** [github.com/Nesvilab/FragPipe](https://github.com/Nesvilab/FragPipe)
- **Approach:** Ultrafast fragment-ion indexing for database search. PTMProphet or PTM-Shepherd handle site localization. Supports open search for unbiased PTM discovery.
- **Key innovation:** Orders of magnitude faster than conventional search engines; open search mode can discover unexpected modifications without specifying them in advance.
- **Strengths:** Speed enables searching large pan-cancer cohorts in hours rather than days; open search uncovers unexpected phospho-events.
- **Limitations:** Localization accuracy depends on downstream tools (PTM-Shepherd); less mature phospho-specific workflows compared to MaxQuant.

### DIA-NN
- **Paper:** [Nature Methods, 2020](https://doi.org/10.1038/s41592-019-0638-x)
- **Code:** [github.com/vdemichev/DiaNN](https://github.com/vdemichev/DiaNN)
- **Approach:** Deep neural network-based analysis of data-independent acquisition (DIA) spectra. Library-free mode generates in silico spectral libraries; site localization uses fragment-level evidence.
- **Key innovation:** Neural network scoring for DIA data enables library-free phosphoproteomics with high sensitivity and fewer missing values than DDA.
- **Strengths:** Excellent quantitative reproducibility; fewer missing values than DDA; library-free mode eliminates need for fractionated library runs.
- **Limitations:** Phosphosite localization in DIA is inherently harder due to chimeric spectra; newer tool with less community validation for phospho-specific analyses.

### Spectronaut
- **Paper:** [Molecular & Cellular Proteomics, 2015](https://doi.org/10.1074/mcp.M114.044305)
- **Code:** Commercial software by Biognosys
- **Approach:** DIA data analysis with proprietary algorithms for peak extraction and site localization. directDIA mode supports library-free analysis.
- **Key innovation:** Sophisticated interference correction and site-level confidence scoring for DIA phosphoproteomics.
- **Strengths:** Mature DIA platform; strong phosphosite localization; widely used in CPTAC studies.
- **Limitations:** Commercial (not open-source); reproducibility concerns when exact algorithms are proprietary.

### AlphaPept
- **Paper:** [Nature Communications, 2024](https://doi.org/10.1038/s41467-024-46485-4)
- **Code:** [github.com/MannLabs/alphapept](https://github.com/MannLabs/alphapept)
- **Approach:** Python-based, open-source proteomics pipeline from the Mann lab. GPU-accelerated processing with modular architecture.
- **Key innovation:** Fully open-source reimagining of the MaxQuant philosophy; Python-native enables integration with ML workflows.
- **Strengths:** Open-source; GPU acceleration; Python ecosystem compatibility; actively developed.
- **Limitations:** Younger tool with smaller user base; phospho-specific benchmarks still limited compared to MaxQuant.

## Complementary: Sequence-Based Predictors

Computational predictors complement MS-based identification by predicting phosphosites from protein sequence alone:

- **DeepPhos** ([Bioinformatics, 2019](https://doi.org/10.1093/bioinformatics/bty1051)) -- deep learning on sequence context windows; captures hierarchical features.
- **MusiteDeep** ([Bioinformatics, 2020](https://doi.org/10.1093/bioinformatics/btx496)) -- attention-based deep learning for general PTM prediction; transfer learning across modification types.
- **NetPhos 3.1** ([Nucleic Acids Research, 2004](https://doi.org/10.1002/pmic.200300771)) -- classic neural network predictor; remains a useful baseline despite its age.

These tools help prioritize candidate sites for experimental validation and fill gaps where MS coverage is incomplete.

## DDA vs. DIA: The Core Tradeoff

DDA (data-dependent acquisition) selects the most abundant precursors for fragmentation, yielding high-confidence identifications but stochastic sampling and missing values across runs. DIA (data-independent acquisition) fragments all precursors in defined windows, providing more complete and reproducible quantification at the cost of more complex data analysis and harder site localization due to chimeric spectra. Pan-cancer studies increasingly favor DIA for its quantitative consistency across large cohorts.

## When to Use Phosphosite Identification Methods

**Best for:**

- Initial processing of raw mass spectrometry data
- Building phosphosite-level quantitative matrices for downstream kinase inference
- Comparing DDA vs. DIA strategies for study design
- Sequence-based predictors for expanding coverage beyond MS detection limits

**Not ideal for:**

- Functional interpretation of identified sites (see functional scoring methods)
- Inferring upstream kinase activity (see kinase-substrate inference methods)
- Understanding pathway-level signaling (see pathway reconstruction methods)
