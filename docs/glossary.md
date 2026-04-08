# Glossary

Key terms in pan-cancer phosphoproteomics, organized alphabetically.

---

**Activity inference** — Estimating the activity level of a kinase from the phosphorylation states of its known substrates. Distinct from substrate prediction.

**Annotation bottleneck** — The gap between the number of observed phosphosites (~240K) and those with known kinase or function (<5%). The central limitation of computational phosphoproteomics.

**CPTAC** — Clinical Proteomic Tumor Analysis Consortium. NCI-funded program producing matched proteomics, phosphoproteomics, and genomics across cancer types.

**DDA (Data-Dependent Acquisition)** — MS acquisition mode selecting the top-N most abundant precursor ions per cycle for fragmentation. Deeper per-run but less reproducible across samples than DIA.

**DIA (Data-Independent Acquisition)** — MS acquisition mode fragmenting all precursors within defined m/z windows. Better quantitative reproducibility but computationally demanding.

**decoupleR** — Unified framework for inferring kinase, transcription factor, and pathway activities from omics data. Wraps multiple statistical methods (ULM, VIPER, GSVA) with a consistent API.

**Enrichment analysis** — Statistical test asking whether substrates of a kinase are over-represented among differentially phosphorylated sites. The basis of KSEAapp and KEA3.

**funscoR** — Random forest classifier predicting functional relevance of phosphosites from evolutionary, structural, and regulatory features.

**IMAC** — Immobilized Metal Affinity Chromatography. Phosphopeptide enrichment using Fe3+ or Ti4+ metal ions. The standard enrichment in CPTAC workflows.

**ILP (Integer Linear Programming)** — Optimization framework used by CARNIVAL and PHONEMeS to find the most parsimonious signaling network consistent with observed phosphosite changes.

**Kinase** — Enzyme that transfers a phosphate group from ATP to a substrate protein. The human genome encodes 518 kinases (the "kinome").

**Kinase-substrate relationship** — A validated connection between a kinase and a specific phosphosite it phosphorylates. Fewer than 10,000 such pairs are curated in PhosphoSitePlus.

**KinaseLibrary** — Positional scanning peptide array data for 303 Ser/Thr kinases. The most comprehensive motif reference for kinase specificity (Johnson et al., Nature 2023).

**Kinome** — The complete set of protein kinases encoded in a genome. The human kinome contains 518 kinases.

**Localization probability** — Confidence score for assigning a phospho group to a specific residue within a peptide. Sites with probability >0.75 are typically considered localized.

**Motif** — The amino acid sequence pattern surrounding a phosphorylation site that determines kinase specificity. Example: CDK substrates prefer [S/T]-P-x-[K/R].

**OmniPath** — Meta-resource integrating 100+ databases of signaling interactions. The prior knowledge backbone for pathway reconstruction tools.

**Phosphatase** — Enzyme that removes phosphate groups from proteins. The counterpart to kinases in reversible phosphorylation signaling.

**Phosphoproteomics** — Mass spectrometry-based measurement of phosphorylation states across thousands of proteins simultaneously.

**Phosphosite** — A specific amino acid residue (Ser, Thr, or Tyr) on a protein that is phosphorylated. Identified by protein name and residue number (e.g., AKT1-S473).

**PhosphoSitePlus** — The primary curated database of phosphorylation sites and kinase-substrate relationships. Contains ~240,000 human phosphosites.

**Prior knowledge network** — A graph of known protein-protein interactions and regulatory relationships used as input for pathway reconstruction. OmniPath is the standard source.

**Ratio compression** — Systematic underestimation of fold changes in TMT-based quantification due to co-isolation interference. Affects pan-cancer phosphoproteomics datasets.

**Stoichiometry** — The fraction of a protein population that is phosphorylated at a given site. Rarely measured in standard phosphoproteomics; confounds abundance-based analyses.

**Substrate** — A protein that is phosphorylated by a kinase. One kinase may have hundreds of substrates; one substrate may be phosphorylated by multiple kinases.

**TMT (Tandem Mass Tag)** — Isobaric labeling reagent enabling multiplexed quantification of 11-18 samples per MS run. The backbone of CPTAC datasets.

**TiO2** — Titanium dioxide. Used for phosphopeptide enrichment; favors peptides with acidic residues near the phosphosite.
