# Pathway Reconstruction Methods

**Pathway reconstruction connects individual phosphosite and kinase observations into coherent signaling network models that explain how upstream perturbations propagate to downstream cellular responses.**

## Key Methods

### OmniPath
- **Paper:** [Nature Methods, 2016](https://doi.org/10.1038/nmeth.4077)
- **Code:** [github.com/saezlab/OmnipathR](https://github.com/saezlab/OmnipathR)
- **Approach:** Comprehensive prior knowledge database integrating signaling pathways, enzyme-substrate relationships, protein complexes, and gene regulatory interactions from over 100 resources.
- **Key innovation:** Unified access to fragmented pathway databases through a single harmonized API; serves as the prior knowledge backbone for downstream reconstruction tools.
- **Strengths:** Largest integrated signaling resource; actively maintained; accessible via R, Python, and web API; quality-scored interactions.
- **Limitations:** Prior knowledge inherits biases of source databases (well-studied pathways overrepresented); interaction directionality not always reliable.

### PHONEMeS
- **Paper:** [Molecular Systems Biology, 2018](https://doi.org/10.15252/msb.20188046)
- **Code:** [github.com/saezlab/PHONEMeS](https://github.com/saezlab/PHONEMeS)
- **Approach:** PHOsphorylation NEtworks for Mass Spectrometry. Uses integer linear programming (ILP) to find the most parsimonious signaling network connecting drug targets to observed phosphorylation changes, constrained by a prior knowledge network.
- **Key innovation:** Directly designed for phosphoproteomics data; ILP formulation finds globally optimal sparse networks rather than local solutions.
- **Strengths:** Purpose-built for phospho data; produces mechanistically interpretable network models; ILP guarantees optimality.
- **Limitations:** Requires well-defined perturbation targets as input; scalability limited for very large networks; depends heavily on prior knowledge completeness.

### CARNIVAL
- **Paper:** [npj Systems Biology and Applications, 2019](https://doi.org/10.1038/s41540-019-0118-z)
- **Code:** [github.com/saezlab/CARNIVAL](https://github.com/saezlab/CARNIVAL)
- **Approach:** CAusal Reasoning for Network Identification using Integer VALue programming. Contextualizes signaling networks by finding causal paths consistent with transcription factor activities and perturbation data using ILP optimization.
- **Key innovation:** Integrates transcription factor activity estimates (from gene expression) with signaling network topology to infer causal signaling paths.
- **Strengths:** Bridges phosphoproteomics and transcriptomics; causal reasoning produces directed, interpretable networks; flexible input types.
- **Limitations:** Primarily transcription factor-centric; phospho integration requires coupling with upstream kinase inference tools; ILP solver dependency.

### COSMOS
- **Paper:** [Molecular Systems Biology, 2021](https://doi.org/10.15252/msb.20209730)
- **Code:** [github.com/saezlab/cosmosR](https://github.com/saezlab/cosmosR)
- **Approach:** Causal Oriented Search of Multi-Omic Space. Extends CARNIVAL to integrate signaling, transcriptional regulation, and metabolism into unified network models spanning from receptor activation through metabolic output.
- **Key innovation:** Multi-omic integration across signaling layers; connects phosphoproteomics to metabolomics through a coherent causal framework.
- **Strengths:** Most comprehensive pathway reconstruction tool; truly multi-omic; mechanistically connects kinase activity to metabolic consequences.
- **Limitations:** Computationally demanding; requires multi-omic data for full utility; complex setup and parameter tuning.

### CausalPath
- **Paper:** [npj Genomic Medicine, 2018](https://doi.org/10.1038/s41525-018-0064-8)
- **Code:** [github.com/PathwayAndDataAnalysis/causalpath](https://github.com/PathwayAndDataAnalysis/causalpath)
- **Approach:** Identifies causal relationships between measured phosphoproteomic and proteomic changes using Pathway Commons prior knowledge. Tests whether observed correlations between protein expression and phosphorylation are consistent with known causal mechanisms.
- **Key innovation:** Correlation-based approach that statistically tests causal hypotheses rather than optimizing network topology; directly interpretable as "protein X causally explains phosphorylation of site Y."
- **Strengths:** Statistically grounded; does not require perturbation data; works with observational cohort data (ideal for CPTAC studies); interpretable output.
- **Limitations:** Correlation-based inference is weaker than perturbation-based; limited to relationships present in Pathway Commons.

### PhosR
- **Paper:** [Cell Reports, 2021](https://doi.org/10.1016/j.celrep.2021.108771)
- **Code:** [github.com/PYangLab/PhosR](https://github.com/PYangLab/PhosR)
- **Approach:** R package providing an integrated pipeline for phosphoproteomics including imputation, normalization, kinase activity scoring, and signaling pathway analysis using kinase-substrate and PPI networks.
- **Key innovation:** End-to-end phosphoproteomics analysis pipeline combining data processing with pathway-level interpretation in a single framework.
- **Strengths:** Complete workflow from raw phosphosite matrix to pathway output; well-documented; handles common data quality issues (missing values, batch effects).
- **Limitations:** Less flexible than modular approaches; pathway analysis component is simpler than dedicated ILP-based methods.

## The Saez-Rodriguez Lab Ecosystem

A coherent pipeline connects several tools from the Saez-Rodriguez lab: **OmniPath** provides the prior knowledge network, **decoupleR** infers kinase and transcription factor activities, **PHONEMeS** reconstructs phospho-specific signaling subnetworks, **CARNIVAL** extends to causal transcriptional regulation, and **COSMOS** unifies signaling with metabolism. This modular ecosystem allows users to combine tools based on available data and biological questions.

## ILP-Based vs. Correlation-Based Approaches

ILP-based methods (PHONEMeS, CARNIVAL, COSMOS) optimize network topology to explain observed data, producing mechanistic models but requiring perturbation context and solver infrastructure. Correlation-based methods (CausalPath) test statistical associations against known causal mechanisms, requiring less computational setup and working with observational data but offering weaker causal claims. Pan-cancer studies benefit from both: ILP methods for drug perturbation experiments, correlation methods for tumor cohort analyses.

## When to Use Pathway Reconstruction Methods

**Best for:**

- Building mechanistic models connecting kinase activity to downstream cellular outcomes
- Integrating phosphoproteomics with transcriptomics or metabolomics
- Identifying druggable nodes in signaling networks
- Generating testable hypotheses about signaling cascade architecture

**Not ideal for:**

- Initial exploratory analysis of phosphoproteomics data (start with kinase inference)
- Situations lacking prior knowledge for the pathway of interest
- High-throughput screening where simpler enrichment methods suffice
