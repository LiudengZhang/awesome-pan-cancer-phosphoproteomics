# Key Datasets

Datasets organized by what analyses they support. Each entry notes the phosphoproteomics platform, sample count, and what makes it uniquely useful.

## Pan-Cancer Atlases

### CPTAC Pan-Cancer Phosphoproteome (Geffen et al., 2023)

- **Cancer types:** 10 (breast, ovarian, endometrial, colon, lung adenocarcinoma, lung squamous, head and neck, glioblastoma, renal clear cell, pancreatic)
- **Samples:** ~1,100 tumors with matched normal
- **Phosphosites:** 110,274 quantified
- **Platform:** TMT-based DDA (Orbitrap)
- **Access:** [CPTAC Data Portal](https://proteomic.datacommons.cancer.gov/pdc/)
- **Best for:** Pan-cancer kinase activity analysis, phospho-subtype discovery, cross-cancer convergence studies
- **Caveat:** TMT ratio compression affects quantitative accuracy for small fold changes

### CPTAC Proteogenomic Ecosystem (Vasaikar et al., 2023)

- **Cancer types:** 14 (extends Geffen with additional tumor types)
- **Samples:** 1,524 tumors
- **Data layers:** Proteomics, phosphoproteomics, genomics, transcriptomics, clinical
- **Access:** [LinkedOmicsKB](https://www.linkedomics.org/)
- **Best for:** Multi-omic integration, proteogenomic driver discovery

## Single-Cancer Datasets

### Breast Cancer CPTAC (Krug et al., 2020)

- **Samples:** 122 treatment-naive breast tumors
- **Phosphosites:** ~40,000 quantified
- **Key value:** PAM50 subtype-specific kinase activities; foundational for phospho-subtype concept
- **Best for:** Subtype-specific kinase activity, benchmark dataset for method development

### Ovarian Cancer CPTAC (McDermott et al., 2020)

- **Samples:** 169 high-grade serous ovarian tumors
- **Key value:** Links phospho-signaling to platinum sensitivity
- **Best for:** Therapeutic response prediction, platinum resistance mechanisms

### Lung Adenocarcinoma CPTAC (Gillette et al., 2020)

- **Samples:** 110 tumors
- **Key value:** Connects driver mutations to phospho-signaling consequences
- **Best for:** Mutation-to-phospho linking, EGFR/ALK/KRAS signaling studies

## Kinase Reference Datasets

### KinaseLibrary Positional Scanning Data (Johnson et al., 2023)

- **Kinases:** 303 Ser/Thr kinases
- **Method:** Positional scanning peptide arrays
- **Access:** [kinase-library.phosphosite.org](https://kinase-library.phosphosite.org/)
- **Best for:** Motif-based kinase-substrate prediction, motif comparison

### PhosphoSitePlus Curated Annotations

- **Phosphosites:** ~240,000 human sites
- **Kinase-substrate pairs:** ~10,000 curated
- **Access:** [phosphosite.org](https://www.phosphosite.org/)
- **Best for:** Training and evaluating kinase-substrate inference tools
- **Caveat:** Heavy bias toward well-studied kinases (AKT, ERK, CDK families); ~130 kinases have zero annotated substrates

## Perturbation Datasets (for Benchmarking)

### Kinase Inhibitor Panels

Multiple studies have profiled phosphoproteome changes after kinase inhibitor treatment:

| Study | Inhibitors Tested | Cell Lines | Value |
|---|---|---|---|
| Wilkes et al. 2015 | 28 kinase inhibitors | Jurkat, A549 | benchmarKIN evaluation dataset |
| Klaeger et al. 2017 | 243 clinical kinase inhibitors | Cell-free kinobeads | Drug-kinase binding ground truth |
| Hijazi et al. 2020 | EGF/HGF time courses | HeLa | Temporal dynamics benchmark |

**Best for:** Evaluating kinase activity inference methods; the controlled perturbation provides ground truth for which kinases should change.

## Dataset Selection Guide

| Analysis Goal | Recommended Dataset | Why |
|---|---|---|
| Pan-cancer kinase landscape | CPTAC Geffen 2023 | Largest standardized phospho dataset |
| Method benchmarking (kinase inference) | Kinase inhibitor panels | Controlled perturbation = ground truth |
| Motif-based prediction | KinaseLibrary | Most comprehensive motif data |
| Subtype-specific analysis | Krug 2020 (breast) | Best-characterized phospho subtypes |
| Multi-omic integration | Vasaikar 2023 ecosystem | Matched multi-omic layers |
| Training ML models | PhosphoSitePlus + dbPTM | Largest labeled datasets |
