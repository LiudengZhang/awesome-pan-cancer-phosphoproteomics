# Pan-Cancer Integration Studies

**Pan-cancer phosphoproteomic integration reveals signaling programs that transcend tissue of origin, identifying convergent kinase dependencies and phosphorylation-defined subtypes invisible to genomics alone.**

## Key Studies

### Geffen et al. 2023 -- Pan-Cancer Phospho-Signaling Atlas
- **Paper:** [Cell, 2023](https://doi.org/10.1016/j.cell.2023.07.013)
- **Data:** CPTAC pan-cancer cohort (11 cancer types, ~1,100 tumors)
- **Approach:** Systematic kinase activity inference across cancer types using phosphoproteomic profiling. Identified recurrent kinase activity patterns and phosphorylation-based tumor subtypes through unsupervised clustering of inferred kinase activities.
- **Key findings:** Convergent kinase programs operate across histologically distinct cancers. CDK-RB and MAPK signaling axes define pan-cancer phospho-subtypes that cut across tissue of origin. Phospho-subtypes capture therapeutic vulnerabilities not apparent from genomic or transcriptomic classification.
- **Significance:** The most comprehensive pan-cancer phosphoproteomic analysis to date; establishes that kinase activity landscapes provide a complementary axis of tumor classification.

### Vasaikar et al. 2023 -- CPTAC Pan-Cancer Proteogenomics
- **Paper:** [Cancer Cell, 2023](https://doi.org/10.1016/j.ccell.2023.06.009)
- **Data:** CPTAC ecosystem across 10 cancer types with matched genomic, transcriptomic, proteomic, and phosphoproteomic data
- **Approach:** Multi-omic integration linking somatic alterations to proteomic and phosphoproteomic consequences. Quantified cis and trans effects of copy number alterations and mutations on protein phosphorylation.
- **Key findings:** Many driver mutations exert their effects primarily at the phosphoproteomic level, invisible to transcriptomics. Trans-effects of copy number alterations on phosphorylation reveal signaling network dependencies. The phosphoproteome captures drug-targetable pathway activation missed by other omic layers.
- **Significance:** Demonstrates that proteogenomic integration with phosphoproteomics is necessary for complete functional interpretation of cancer genomes.

### Li et al. 2023 -- Kinase Activity Landscape
- **Paper:** [Cell, 2023](https://doi.org/10.1016/j.cell.2023.07.014)
- **Data:** Large-scale kinase activity profiling across cancer types
- **Approach:** Inferred kinase activities from phosphoproteomic data and mapped the kinase activity landscape across tumors, identifying kinase co-activation modules and their associations with clinical features.
- **Key findings:** Kinase activities cluster into co-regulated modules reflecting shared upstream regulation or pathway membership. Cancer-type-specific kinase activation patterns distinguish tumor lineages, while a subset of kinase modules are recurrently active across cancers. Kinase activity scores correlate with drug sensitivity in cell line panels.
- **Significance:** Provides a kinase-centric view of cancer signaling that directly connects to therapeutic targeting with kinase inhibitors.

### Krug et al. 2020 -- Breast Cancer CPTAC Proteogenomics
- **Paper:** [Cell, 2020](https://doi.org/10.1016/j.cell.2020.10.036)
- **Data:** 122 treatment-naive breast tumors with matched multi-omic profiling
- **Approach:** Deep proteogenomic characterization of breast cancer subtypes including phosphoproteomic profiling. Identified phosphorylation-based subtypes and kinase activity signatures within and across genomic subtypes.
- **Key findings:** Phosphoproteomic subtypes provide finer stratification than genomic subtypes alone. Within basal-like breast cancers, distinct kinase activity patterns (e.g., high CDK vs. high immune kinase signatures) define subgroups with different biology. Phosphoproteomic data identifies actionable kinase targets in tumors lacking genomic drivers.
- **Significance:** Foundational single-cancer-type study demonstrating that phosphoproteomics adds clinical value beyond genomics; established analytical paradigms adopted by subsequent pan-cancer efforts.

## Cross-Cutting Themes

**Convergent kinase programs across cancers.** Multiple studies independently identify a core set of kinase signaling modules (CDK-RB cell cycle, MAPK proliferation, PI3K-AKT-mTOR growth, DNA damage response) that are recurrently activated across cancer types, suggesting shared therapeutic vulnerabilities regardless of tissue of origin.

**Cancer-type-specific phospho-signatures.** Despite convergent programs, each cancer type maintains a distinctive phosphoproteomic fingerprint reflecting lineage-specific signaling wiring. These signatures aid in tumor classification and may explain differential drug responses across cancer types.

**Phospho-subtypes beyond genomic subtypes.** A recurring finding is that phosphoproteomic subtypes provide clinically relevant stratification not captured by DNA or RNA-based classification. Tumors with identical driver mutations can have distinct kinase activity profiles and different therapeutic vulnerabilities.

## When to Use Pan-Cancer Integration Approaches

**Best for:**

- Identifying shared therapeutic targets across cancer types
- Discovering phosphorylation-based tumor subtypes for patient stratification
- Connecting genomic alterations to functional signaling consequences
- Generating hypotheses for kinase inhibitor repurposing across indications

**Not ideal for:**

- Single-sample clinical interpretation (cohort-level studies)
- Rare cancer types with insufficient phosphoproteomic cohort data
- Real-time clinical decision-making (current studies are retrospective)
