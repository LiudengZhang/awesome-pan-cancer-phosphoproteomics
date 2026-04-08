# Therapeutic Response Methods

**Therapeutic response analysis uses phosphoproteomics to connect kinase inhibitor treatments to phosphosite-level drug effects, informing drug selection and predicting resistance mechanisms.**

## Key Methods

### KinasePA
- **Paper:** [Bioinformatics, 2015](https://doi.org/10.1093/bioinformatics/btv524)
- **Code:** [bioconductor.org/packages/KinasePA](https://bioconductor.org/packages/KinasePA/)
- **Approach:** Kinase Perturbation Analysis. Infers kinase activity changes between conditions using substrate set enrichment on phosphoproteomic data, specifically designed for drug perturbation experiments.
- **Key innovation:** Tailored for before/after treatment comparisons; directly outputs which kinases are inhibited or activated by a drug.
- **Strengths:** Purpose-built for drug response studies; straightforward interpretation; Bioconductor package with standard interfaces.
- **Limitations:** Requires matched pre/post treatment samples; dependent on kinase-substrate database coverage; does not model adaptive or feedback responses.

### DrugKiNET
- **Paper:** [Briefings in Bioinformatics, 2024](https://doi.org/10.1093/bib/bbae058)
- **Code:** [github.com/zhaoweiyu-github/DrugKiNET](https://github.com/zhaoweiyu-github/DrugKiNET)
- **Approach:** Network-based framework linking drugs to kinases to phosphosites to phenotypes. Integrates drug-target binding data, kinase-substrate relationships, and pathway annotations to predict drug effects on the phosphoproteome.
- **Key innovation:** End-to-end modeling from drug to phosphosite: predicts which phosphosites a given kinase inhibitor will affect and which phenotypic consequences follow.
- **Strengths:** Bridges pharmacology and phosphoproteomics; useful for drug repurposing; connects drug mechanisms to observable phospho-signatures.
- **Limitations:** Predictions constrained by known drug-kinase binding profiles; off-target effects not fully captured; network-based predictions require experimental validation.

### KSTAR
- **Paper:** [Nature Communications, 2022](https://doi.org/10.1038/s41467-022-32550-z)
- **Code:** [github.com/NaegleLab/KSTAR](https://github.com/NaegleLab/KSTAR)
- **Approach:** Kinase activity inference using random network subsampling (detailed in kinase-substrate inference). In the therapeutic context, applied to compare kinase activity profiles before and after drug treatment.
- **Key innovation:** Bias-corrected kinase activity estimates reveal drug-responsive and drug-resistant kinase programs; robust to the database biases that plague treatment-response analyses.
- **Strengths:** Addresses study bias in drug-kinase-substrate databases; statistical framework quantifies confidence; works with single-sample data.
- **Limitations:** Binary input (regulated/not) loses quantitative dose-response information; computationally intensive.

## Key Studies

### Cao et al. 2024 -- Phosphoproteomics-Guided Cancer Therapy
- **Paper:** [Cancer Discovery, 2024](https://doi.org/10.1158/2159-8290.CD-23-0936)
- **Approach:** Applied phosphoproteomic profiling to patient tumors to identify activated kinases and match patients to corresponding kinase inhibitors. Demonstrated that phospho-guided therapy selection improved response rates compared to genomics-only selection.
- **Key findings:** Phosphoproteomics identified actionable kinase targets in tumors lacking genomic drivers. Patients selected by phospho-signatures showed higher response rates to matched kinase inhibitors. Adaptive resistance mechanisms were visible as compensatory kinase activation in post-treatment biopsies.
- **Significance:** Among the first prospective demonstrations that phosphoproteomic profiling can directly guide clinical treatment decisions in oncology.

### Petralia et al. 2024 -- Pharmacoproteomics
- **Paper:** [Cell, 2024](https://doi.org/10.1016/j.cell.2024.05.013)
- **Approach:** Systematic integration of drug response data with proteomic and phosphoproteomic profiles across cancer cell lines. Built predictive models linking basal phosphoproteomic states to drug sensitivity.
- **Key findings:** Basal kinase activity profiles predict drug sensitivity better than genomic features alone for many kinase inhibitors. Phosphoproteomic features capture pathway activation states that explain variable drug responses among genomically similar tumors. Multi-omic models integrating phosphoproteomics outperform single-omic predictors.
- **Significance:** Establishes phosphoproteomics as a predictive layer for precision oncology drug response modeling at scale.

## The Kinase Inhibitor-Phosphosite Connection

The pharmacological logic connecting kinase inhibitors to phosphoproteomics is direct: kinase inhibitors reduce phosphorylation of substrates downstream of their target kinase. Monitoring these substrate phosphosites provides a functional readout of drug efficacy that is more proximal to drug action than transcriptomic or phenotypic endpoints. This connection enables both prospective drug selection (identifying active kinases to target) and retrospective pharmacodynamic monitoring (confirming on-target drug activity).

## Challenges

**Tumor heterogeneity.** Bulk phosphoproteomic measurements average across cell populations within a tumor. Resistant subclones with distinct kinase activity profiles may be masked in bulk data, only becoming apparent upon treatment failure. Single-cell phosphoproteomics remains technically limited.

**Adaptive resistance.** Kinase signaling networks rewire in response to inhibition. Compensatory kinase activation (e.g., MAPK pathway reactivation after PI3K inhibition) can restore proliferative signaling through alternative routes, requiring longitudinal phosphoproteomic monitoring.

**Phospho-guided clinical trials.** Translating phosphoproteomic findings into clinical trials faces practical barriers: sample processing time (hours to days), tissue requirements (sufficient material for deep phosphoproteomics), assay standardization across clinical sites, and regulatory acceptance of phospho-based biomarkers as companion diagnostics.

## When to Use Therapeutic Response Methods

**Best for:**

- Identifying kinase targets for precision oncology drug selection
- Monitoring pharmacodynamic response to kinase inhibitors
- Predicting drug sensitivity from basal phosphoproteomic profiles
- Understanding resistance mechanisms through longitudinal phospho-profiling

**Not ideal for:**

- Non-kinase-targeted therapies (immunotherapy, chemotherapy) where phospho-readouts are indirect
- Tumors with insufficient biopsy material for deep phosphoproteomics
- Real-time clinical decisions where turnaround time exceeds the treatment window
