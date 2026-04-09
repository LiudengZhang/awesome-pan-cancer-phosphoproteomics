# Awesome Pan-Cancer Phosphoproteomics [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Pan-cancer phosphoproteomics can identify thousands of sites — but without knowing which kinase, which pathway, and which drug, a catalog is not a map. This list connects the tools that turn phosphosites into actionable biology.

Mass spectrometry can now quantify over 100,000 phosphorylation sites across tumor types. Yet fewer than 5% of these sites have a known upstream kinase, and fewer than 3% have established functional roles. The gap between measurement and understanding defines this field. This list organizes the computational tools, databases, experimental methods, and pan-cancer studies that bridge phosphosite catalogs to mechanistic insight and therapeutic targets.

**Companion site:** [liudengzhang.github.io/awesome-pan-cancer-phosphoproteomics](https://liudengzhang.github.io/awesome-pan-cancer-phosphoproteomics/)

## Contents

- [Surveys and Reviews](#surveys-and-reviews)
- [Phosphosite Identification](#phosphosite-identification)
- [Kinase-Substrate Inference](#kinase-substrate-inference)
- [Pathway Reconstruction](#pathway-reconstruction)
- [Functional Scoring and Annotation](#functional-scoring-and-annotation)
- [Pan-Cancer Integration Studies](#pan-cancer-integration-studies)
- [Therapeutic Response and Drug Sensitivity](#therapeutic-response-and-drug-sensitivity)
- [Databases and Resources](#databases-and-resources)
- [Experimental Methods](#experimental-methods)
- [Tools and Infrastructure](#tools-and-infrastructure)
- [Companion Site](#companion-site)

## Surveys and Reviews

- [Phosphoproteomics for cancer research](https://doi.org/10.1186/s12014-024-09455-4) - Comprehensive overview of phosphoproteomics workflows from sample preparation through data analysis, with emphasis on clinical translation (Clinical Proteomics, 2024).
- [The expanding landscape of cancer phosphoproteomics](https://doi.org/10.1038/s41568-023-00604-3) - Perspective on how CPTAC-scale phosphoproteomics reshapes understanding of cancer signaling beyond genomics (Nature Reviews Cancer, 2023).
- [Computational approaches for kinase-substrate prediction](https://doi.org/10.1016/j.coisb.2020.08.008) - Systematic comparison of motif-based versus network-based kinase-substrate inference strategies (Current Opinion in Systems Biology, 2020).
- [Mass spectrometry-based phosphoproteomics](https://doi.org/10.1002/mas.21887) - Technical review covering enrichment strategies, fragmentation methods, and quantification approaches for phosphopeptides (Mass Spectrometry Reviews, 2023).
- [Spatial phosphoproteomics in tissue biology](https://doi.org/10.1016/j.mcpro.2023.100568) - Review connecting phosphoproteomics with spatial resolution for understanding tumor microenvironment signaling (Molecular and Cellular Proteomics, 2023).
- [sc-best-practices: phosphoproteomics analysis](https://www.sc-best-practices.org/) - Community-maintained best practices for single-cell and proteomics data analysis workflows.

## Phosphosite Identification

Tools for detecting and quantifying phosphorylation sites from mass spectrometry data.

- [MaxQuant](https://www.maxquant.org/) - The most widely used search engine for phosphoproteomics; Andromeda search engine with phospho(STY) localization scoring. Gold standard but computationally heavy (Nature Biotechnology, 2008).
- [FragPipe](https://github.com/Nesvilab/FragPipe) - MSFragger-based pipeline with PTMProphet for phosphosite localization; significantly faster than MaxQuant with comparable sensitivity (Nature Methods, 2017).
- [DIA-NN](https://github.com/vdemichev/DiaNN) - Neural network-based DIA analysis with library-free search capability; enables deep phosphoproteome coverage without spectral libraries (Nature Methods, 2020).
- [Spectronaut](https://biognosys.com/software/spectronaut/) - Commercial DIA analysis platform with directDIA mode for phosphoproteomics; strong phosphosite localization in DIA data (Molecular and Cellular Proteomics, 2015).
- [AlphaPept](https://github.com/MannLabs/alphapept) - Python-based open-source pipeline from the Mann lab; modular design allows custom phospho workflows (Nature Communications, 2024).
- [DeepPhos](https://github.com/USTC-HIlab/DeepPhos) - Deep learning predictor of general phosphorylation sites from protein sequence; supplements MS-based identification (Bioinformatics, 2019).
- [MusiteDeep](https://github.com/duolinwang/MusiteDeep) - Deep learning framework for predicting phosphorylation and other PTM sites from sequence; transfer learning across modification types (Nucleic Acids Research, 2020).
- [NetPhos 3.1](https://services.healthtech.dtu.dk/services/NetPhos-3.1/) - Sequence-based neural network predictor for Ser/Thr/Tyr phosphorylation; one of the earliest and most cited predictors (Proteomics, 2004).

## Kinase-Substrate Inference

Methods for predicting which kinase phosphorylates which site — the central bottleneck of the field.

- [KinaseLibrary](https://kinase-library.phosphosite.org/) - Positional scanning peptide array data for 303 Ser/Thr kinases; the most comprehensive motif reference, but motifs alone explain only part of kinase specificity (Nature, 2023).
- [KSEAapp](https://github.com/casecpb/KSEAapp) - Kinase-substrate enrichment analysis using PhosphoSitePlus annotations; simple and widely used, but limited by known substrate annotations (Bioinformatics, 2017).
- [KEA3](https://maayanlab.cloud/kea3/) - Kinase enrichment analysis integrating multiple libraries; broader coverage than KSEAapp through aggregation, but inherits biases from each source (Nucleic Acids Research, 2021).
- [RoKAI](https://github.com/serhan-yilmaz/RoKAI) - Network-propagation approach that improves kinase activity inference by incorporating functional relationships between phosphosites (Nucleic Acids Research, 2021).
- [PhosX](https://github.com/alussana/PhosX) - Kinase activity inference using substrate sequence specificity from KinaseLibrary motifs; fast and annotation-free (Bioinformatics, 2024).
- [GPS 6.0](https://gps.biocuckoo.cn/) - Group-based prediction system for kinase-specific phosphorylation sites; covers 617 human kinases with hierarchical predictions (Nucleic Acids Research, 2023).
- [iGPS](https://igps.biocuckoo.org/) - Integrates GPS motif predictions with PPI network context to improve kinase-substrate prediction accuracy (Molecular Cell, 2020).
- [NetworKIN](http://networkin.info/) - Combines linear motif scoring with network context (STRING interactions) for kinase-substrate prediction; pioneered the motif+network paradigm (Science Signaling, 2007).
- [decoupleR](https://github.com/saezlab/decoupleR) - Unified framework for inferring kinase and TF activities from omics data; wraps multiple methods (ULM, VIPER, GSVA) with consistent API (Bioinformatics, 2022).
- [INKA](https://inkascore.org/) - Integrative inferred kinase activity scoring combining kinase-centric and substrate-centric evidence (Molecular Systems Biology, 2019).
- [benchmarKIN](https://github.com/saezlab/benchmarKIN) - Benchmark framework comparing 11 kinase activity inference methods; reveals that no single method dominates across all scenarios (Briefings in Bioinformatics, 2024).
- [PTMsigDB](https://github.com/broadinstitute/ssGSEA2.0) - Curated phosphosite signature database organized by kinase, pathway, and perturbation; enables set-based enrichment analysis (Molecular and Cellular Proteomics, 2019).

## Pathway Reconstruction

Tools for connecting phosphorylation events into signaling cascades and causal networks.

- [PHONEMeS](https://github.com/saezlab/PHONEMeS) - Integer linear programming approach to reconstruct signaling pathways from phosphoproteomics and prior knowledge networks; identifies the most parsimonious pathway explanations (PLOS Computational Biology, 2015).
- [CARNIVAL](https://github.com/saezlab/CARNIVAL) - Causal network optimization from perturbation data; uses ILP to find signaling topologies consistent with observed phosphosite changes (npj Systems Biology and Applications, 2019).
- [COSMOS](https://github.com/saezlab/cosmosR) - Integrates phosphoproteomics, transcriptomics, and metabolomics into unified causal signaling models; the most ambitious multi-omics integration in this space (Molecular Systems Biology, 2021).
- [CausalPath](https://github.com/PathwayAndDataAnalysis/causalpath) - Discovers causal signaling relationships from proteomic/phosphoproteomic data using pathway databases; outputs directed networks (PLOS Computational Biology, 2018).
- [PhosR](https://github.com/PYangLab/PhosR) - R package for comprehensive phosphoproteomics analysis including kinase-substrate scoring, pathway analysis, and temporal dynamics (Nucleic Acids Research, 2021).
- [OmniPath](https://github.com/saezlab/OmnipathR) - Meta-resource integrating 100+ databases of signaling, regulatory, and kinase-substrate interactions; the prior knowledge backbone for pathway tools (Nature Methods, 2016).

## Functional Scoring and Annotation

Methods for determining whether a phosphosite matters — the function prediction problem.

- [funscoR](https://github.com/evocellnet/funscoR) - Random forest classifier predicting functional relevance of phosphosites from evolutionary, structural, and regulatory features; assigns probability scores to each site (Molecular Systems Biology, 2021).
- [MIMP](https://github.com/omarwagih/rmimp) - Predicts impact of mutations on phosphorylation by comparing kinase motif scores of wildtype and mutant sequences; connects genomics to phosphoproteomics (Nature Methods, 2015).
- [DeepMVP](https://github.com/bzhanglab/DeepMVP) - Deep learning model predicting pathogenicity of missense variants at phosphorylation sites; integrates sequence, structure, and functional data (Bioinformatics, 2023).
- [FuncPhos](https://funcphos.mbc.nctu.edu.tw/) - Database and predictor of functional phosphosites using structural and sequence features; classifies sites by regulatory mechanism (Nucleic Acids Research, 2020).

## Pan-Cancer Integration Studies

Large-scale phosphoproteomics studies across cancer types — where the data comes from.

- [CPTAC pan-cancer phosphoproteome atlas](https://doi.org/10.1016/j.cell.2023.07.013) - 110,274 phosphosites across 10 cancer types; defines shared and cancer-type-specific signaling programs (Geffen et al., Cell, 2023).
- [CPTAC proteogenomic data ecosystem](https://doi.org/10.1016/j.ccell.2023.06.009) - Standardized processing of 1,524 tumors across 14 cancer types with matched proteomics, phosphoproteomics, and genomics (Vasaikar et al., Cancer Cell, 2023).
- [Pan-cancer kinase activity landscape](https://doi.org/10.1016/j.cell.2023.07.014) - Kinase activity inference across CPTAC cancers revealing convergent and divergent kinase programs (Li et al., Cell, 2023).
- [Breast cancer phosphoproteomics (CPTAC)](https://doi.org/10.1016/j.cell.2020.10.036) - Foundational CPTAC phosphoproteomics study revealing PAM50 subtype-specific kinase activities (Krug et al., Cell, 2020).
- [Pan-cancer phospho-signaling and drug response](https://doi.org/10.1158/2159-8290.CD-23-1038) - Links CPTAC phosphoproteomic profiles to drug sensitivity predictions across cancer types (Cao et al., Cancer Discovery, 2024).
- [Multi-omic integration for therapeutic vulnerabilities](https://doi.org/10.1016/j.cell.2024.01.027) - Integrates phosphoproteomics with genomics and transcriptomics to identify druggable nodes in treatment-resistant tumors (Petralia et al., Cell, 2024).

## Therapeutic Response and Drug Sensitivity

Connecting phosphoproteomics to treatment decisions.

- [Phosphoproteomics-guided kinase inhibitor selection](https://doi.org/10.1158/2159-8290.CD-23-1038) - Uses patient-derived phosphoproteomics to predict sensitivity to targeted kinase inhibitors (Cancer Discovery, 2024).
- KinasePA - Predicts kinase inhibitor sensitivity from phosphoproteomic profiles; maps phosphosite changes to drug targets (Bioinformatics, 2019).
- [DrugKiNET](https://drugkinet.ca/) - Kinase-drug interaction predictor integrating binding affinity and phosphoproteomic data (Briefings in Bioinformatics, 2023).
- [KSTAR](https://github.com/NaegleLab/KSTAR) - Kinase-substrate activity relationship tool that maps differential phosphorylation to kinase activity changes for therapeutic target nomination (Molecular Systems Biology, 2022).
- [Phosphosite-based patient stratification](https://doi.org/10.1038/s41586-024-07586-6) - Shows phosphoproteomic subtypes predict clinical outcomes independently of genomic subtypes (Nature, 2024).
- [CancerPhospho](https://cancerphospho.org/) - Database linking cancer phosphosite alterations to drug responses and clinical outcomes across tumor types.

## Databases and Resources

- [PhosphoSitePlus](https://www.phosphosite.org/) - The primary curated database for phosphorylation sites with ~240,000 human phosphosites; includes kinase-substrate annotations and upstream regulatory relationships.
- [dbPTM](https://awi.cuhk.edu.cn/dbPTM/) - Comprehensive PTM database covering phosphorylation across species with 3D structure mappings and functional annotations (Nucleic Acids Research, 2024).
- [Phospho.ELM](http://phospho.elm.eu.org/) - Experimentally verified phosphorylation sites with kinase annotations; smaller but highly curated.
- [UniProt PTM annotations](https://www.uniprot.org/) - Swiss-Prot manually curated phosphorylation annotations embedded in protein records; conservative but reliable.
- [CPTAC Data Portal](https://proteomic.datacommons.cancer.gov/pdc/) - Proteomic Data Commons hosting all CPTAC cancer phosphoproteomics datasets with standardized processing.
- [LinkedOmicsKB](https://www.linkedomics.org/) - Web platform linking CPTAC phosphoproteomics to genomics and clinical data with interactive query tools.
- [TCPA/TCGA phospho-RPPA](https://tcpaportal.org/) - Reverse-phase protein array data including ~50 phosphoproteins across TCGA cohorts; low-dimensional but clinically validated.
- [OmniPath](https://omnipathdb.org/) - Integrated signaling resource combining PhosphoSitePlus, Signor, HPRD, and 100+ databases into a unified prior knowledge network.
- [EPSD](https://epsd.biocuckoo.cn/) - Eukaryotic Phosphorylation Site Database with >500,000 sites across 68 species including regulatory information.
- [PTMsigDB](https://github.com/broadinstitute/ssGSEA2.0) - Curated phosphosite signature database from the Broad Institute; enables ssGSEA-based pathway and kinase activity scoring.

## Experimental Methods

Key experimental approaches for phosphoproteomics — understanding what the data can and cannot tell you.

- **TiO2 / IMAC enrichment** - Metal oxide and immobilized metal affinity chromatography for phosphopeptide enrichment; TiO2 favors acidic contexts while IMAC is more permissive. Most pan-cancer datasets use IMAC (Fe-NTA).
- **DDA (Data-Dependent Acquisition)** - Traditional shotgun approach selecting top-N precursors per cycle; deeper per-run phosphoproteome but lower reproducibility across samples. Used in early CPTAC studies.
- **DIA (Data-Independent Acquisition)** - Acquires all precursors in defined windows; better quantitative reproducibility at the cost of computational complexity. Increasingly adopted for clinical phosphoproteomics.
- **TMT multiplexing** - Isobaric labeling enabling 11-18 samples per run with reduced missing values; the backbone of CPTAC pan-cancer datasets. Ratio compression is the main limitation.
- **Label-free quantification (LFQ)** - No chemical labeling; flexible sample numbers but requires careful normalization. Preferred for smaller studies and DIA workflows.
- **Phospho-enriched interactomics (KAYAK)** - Kinase activity assay using peptide substrates incubated with cell lysate; orthogonal validation of computationally inferred kinase activities.

## Tools and Infrastructure

Computational infrastructure supporting phosphoproteomics workflows.

- [Bioconductor phosphoproteomics](https://www.bioconductor.org/) - R/Bioconductor ecosystem with PhosphoR, limma-phospho, and other dedicated packages for phosphoproteomics statistical analysis.
- [Perseus](https://maxquant.net/perseus/) - MaxQuant companion for statistical analysis of proteomics data; widely used for phosphoproteomics downstream analysis (Nature Methods, 2016).
- [MSstats](https://github.com/Vitek-Lab/MSstats) - Statistical framework for quantitative proteomics with dedicated modules for PTM analysis (MSstatsPTM) and group comparisons (Bioinformatics, 2014).
- [Proteomics Identifications (PRIDE)](https://www.ebi.ac.uk/pride/) - European repository for proteomics data; the primary archive for phosphoproteomics raw data and processed results.
- [pySCENIC+](https://github.com/aertslab/scenicplus) - Multi-omic regulatory network inference that can integrate phosphoproteomic kinase activities with transcriptomic readouts.
- [Cytoscape](https://cytoscape.org/) - Network visualization platform essential for interpreting phospho-signaling networks from pathway reconstruction tools.
- [ProteomeScout](https://proteomescout.wustl.edu/) - Web resource for exploring protein modifications including phosphorylation in the context of protein domains and interactions.
- [Kinase.com](http://kinase.com/) - Manning kinome classification and phylogenetic tree; the standard reference for organizing kinase families.

## Companion Site

The [companion site](https://liudengzhang.github.io/awesome-pan-cancer-phosphoproteomics/) provides deeper content:

- **Concepts:** Phosphorylation essentials, the kinase-substrate inference problem, and how phosphoproteomics differs from genomics.
- **Methods:** Detailed method pages covering each category with strengths, limitations, and decision guides.
- **Deep Reads:** Paper analyses for landmark studies with honest assessments.
- **Timeline:** Interactive literature timeline showing the evolution of the field.
- **Explorer:** Interactive method and biology maps for navigating the tool landscape and kinase-substrate-pathway-drug relationships.
- **Synthesis:** Essays on the annotation bottleneck and the path from phosphosites to signaling circuits.

## Contributing

Contributions are welcome. Please read the [contribution guidelines](contributing.md) before submitting a pull request.
