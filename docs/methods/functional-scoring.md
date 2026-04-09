# Functional Scoring Methods

**Functional scoring addresses a critical bottleneck in phosphoproteomics: fewer than 3% of the roughly 200,000 cataloged human phosphosites have a known biological function, making it essential to computationally prioritize sites likely to be functionally important.**

## Key Methods

### funscoR
- **Paper:** [Molecular Systems Biology, 2023](https://doi.org/10.15252/msb.202211321)
- **Code:** [github.com/evocellnet/funscoR](https://github.com/evocellnet/funscoR)
- **Approach:** Random forest classifier predicting functional phosphosites using 59 features spanning evolutionary conservation, structural context, regulatory annotations, and proteomics evidence. Trained on PhosphoSitePlus regulatory sites as positives.
- **Key innovation:** Largest feature set for functional scoring; systematic integration of orthogonal evidence types; provides continuous scores rather than binary classification.
- **Strengths:** Comprehensive feature integration; well-calibrated probability scores; open-source R package; covers both Ser/Thr and Tyr sites.
- **Limitations:** Training set biased toward well-studied sites and pathways; conservation features less informative for lineage-specific regulation; random forest offers limited mechanistic insight into why a site scores highly.

### MIMP
- **Paper:** [Nature Methods, 2015](https://doi.org/10.1038/nmeth.3396)
- **Code:** [github.com/MoHelmy/mimp](https://github.com/MoHelmy/mimp)
- **Approach:** Mutation Impact on Phosphorylation. Predicts whether somatic mutations near phosphosites create or destroy kinase recognition motifs, linking cancer mutations to altered phospho-signaling.
- **Key innovation:** Directly connects the cancer genomics layer (somatic mutations) to the phosphoproteomics layer (kinase-substrate rewiring) by modeling motif disruption.
- **Strengths:** Mechanistically interpretable; identifies gain-of-phosphorylation and loss-of-phosphorylation events; relevant for precision oncology.
- **Limitations:** Only considers mutations within the linear motif window; misses allosteric or structural effects of distant mutations; requires high-quality kinase motif models.

### DeepMVP
- **Paper:** [Bioinformatics, 2024](https://doi.org/10.1093/bioinformatics/btae413)
- **Code:** [github.com/bzhanglab/DeepMVP](https://github.com/bzhanglab/DeepMVP)
- **Approach:** Deep learning model predicting the functional impact of mutations on phosphosites using protein language model embeddings and structural features from AlphaFold2-predicted structures.
- **Key innovation:** Leverages protein language models (ESM-2) and AlphaFold2 structures to capture sequence and structural context beyond linear motifs; goes deeper than motif disruption alone.
- **Strengths:** Captures structural context that linear motif methods miss; benefits from recent advances in protein structure prediction; strong benchmark performance.
- **Limitations:** Computationally heavier than motif-based methods; AlphaFold2 structure quality varies for disordered regions where many phosphosites reside; deep learning model interpretability is limited.

### FuncPhos
- **Paper:** [Cell Reports, 2023](https://doi.org/10.1016/j.celrep.2023.113048)
- **Code:** [github.com/evocellnet/funscoR](https://github.com/evocellnet/funscoR)
- **Approach:** Curated database and scoring framework classifying phosphosites by functional evidence type: enzymatic activity regulation, protein interactions, localization, stability, and other regulatory mechanisms.
- **Key innovation:** Structured functional annotation taxonomy for phosphosites; distinguishes between different mechanisms of phospho-regulation rather than treating function as binary.
- **Strengths:** Rich functional categorization; manually curated high-confidence annotations; useful for interpreting why a site matters, not just whether it matters.
- **Limitations:** Limited coverage (curated databases are inherently small); labor-intensive to maintain and expand; primarily literature-derived with associated publication bias.

## The Functional Dark Matter Problem

The vast majority of detected phosphosites remain functionally uncharacterized. This "dark phosphoproteome" creates a fundamental challenge: phosphoproteomics experiments routinely quantify tens of thousands of sites, but interpretation frameworks built on known functions cover only a small fraction. Functional scoring methods attempt to triage this gap using predictive features.

## Predictive Feature Categories

Three categories of features consistently contribute to functional phosphosite prediction:

- **Evolutionary conservation:** Functionally important sites tend to be conserved across species. However, conservation alone has limited sensitivity because some regulatory phosphosites are lineage-specific adaptations.
- **Structural features:** Sites in structured regions, near protein-protein interfaces, or in activation loops are more likely to be regulatory. AlphaFold2 has expanded structural coverage, but many phosphosites reside in intrinsically disordered regions with limited structural context.
- **Regulatory evidence:** Stoichiometry (high occupancy suggests function), co-regulation with known functional sites, and responsiveness to perturbations all provide indirect evidence of functional importance.

## When to Use Functional Scoring Methods

**Best for:**

- Prioritizing phosphosites for experimental validation from large-scale datasets
- Filtering differentially phosphorylated sites to those most likely to be biologically meaningful
- Connecting somatic mutations to phospho-signaling consequences in cancer genomics
- Annotating phosphoproteomic atlases with functional confidence scores

**Not ideal for:**

- Definitively establishing biological function (experimental validation remains necessary)
- Sites in poorly conserved or taxonomically restricted proteins
- Replacing kinase-substrate inference (functional scoring asks "is this site important?" not "which kinase phosphorylates it?")
