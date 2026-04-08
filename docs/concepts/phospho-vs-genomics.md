# Phosphoproteomics vs Genomics

## The Short Answer

Genomics tells you what mutations exist in a tumor. Phosphoproteomics tells you what signaling is actually active. They answer different questions: genomics identifies the potential for pathway activation; phosphoproteomics measures whether that activation is occurring. Neither alone provides a complete picture of cancer biology, but phosphoproteomics captures functional states that are invisible to DNA sequencing.

## Why They Are Complementary

Mutations are binary -- a driver mutation is either present or absent. Phosphorylation is quantitative and dynamic, changing in magnitude over seconds to minutes in response to stimuli, drug treatment, or microenvironmental cues. A tumor with a KRAS G12D mutation has that mutation in every sequencing read from the mutant clone. But the downstream phosphorylation of ERK, AKT, and S6K varies across time, across cells, and across the tumor microenvironment. Genomics provides the wiring diagram; phosphoproteomics provides the current flowing through the wires.

## What Phosphoproteomics Reveals That Genomics Misses

- **Kinase activity without mutation** -- Wild-type EGFR can be constitutively activated by autocrine ligand loops or loss of negative regulators, producing the same downstream phosphorylation as an EGFR-mutant tumor. Genomics sees no actionable alteration; phosphoproteomics detects the active signaling.
- **Pathway crosstalk** -- Phosphorylation events integrate signals from multiple upstream inputs. A phosphosite on AKT S473 may reflect combined input from PI3K, mTORC2, and integrin signaling. No single genomic alteration captures this convergence.
- **Feedback loops** -- Negative feedback loops (e.g., S6K phosphorylating IRS-1 to dampen insulin signaling) are invisible to genomics but directly measurable by phosphoproteomics.
- **Drug-adaptive rewiring** -- When a kinase inhibitor blocks its target, compensatory kinases activate within hours. This bypass signaling -- a major cause of therapeutic resistance -- is detectable by phosphoproteomics before any genomic change occurs.
- **Stromal and immune signaling** -- Bulk phosphoproteomics captures signaling from all cell types in the tumor microenvironment, including immune checkpoint signaling and CAF-derived growth factor signaling that have no genomic representation in tumor DNA.

## What Genomics Reveals That Phosphoproteomics Misses

- **Passenger vs driver distinction** -- Large-scale sequencing studies with statistical frameworks (MutSig, dNdScv) can distinguish recurrently mutated driver genes from passenger noise. Phosphoproteomics has no equivalent statistical framework for separating functional from non-functional phosphosites.
- **Clonal architecture** -- Variant allele frequencies and multi-region sequencing reveal tumor heterogeneity and clonal evolution. Bulk phosphoproteomics averages across all clones.
- **Non-signaling mechanisms** -- Epigenetic silencing, alternative splicing, and copy number alterations affect cancer biology through mechanisms that do not directly involve phosphorylation.
- **Germline predisposition** -- BRCA1/2 mutations, Lynch syndrome genes, and other hereditary cancer predisposition factors are genomic findings with no phosphoproteomic correlate.

## The CPTAC Lesson

The Clinical Proteomic Tumor Analysis Consortium (CPTAC) has generated matched genomic, transcriptomic, proteomic, and phosphoproteomic data for over 10 cancer types. Key findings demonstrate the added value of phosphoproteomics:

- **Phosphoproteomic subtypes are not redundant with genomic subtypes.** In CPTAC endometrial cancer (Dou et al., Cell 2020), phosphoproteomic clustering identified patient groups with distinct kinase activity profiles that cut across genomic subtypes and predicted clinical outcomes independently.
- **Kinase activity scores outperform mutation status for drug response prediction.** In CPTAC lung adenocarcinoma (Gillette et al., Cell 2020), CDK4 activity inferred from substrate phosphorylation correlated with palbociclib sensitivity better than CDKN2A deletion status alone.
- **Trans-effects dominate.** Most genomic alterations affect phosphorylation on proteins other than the mutated gene product, through indirect signaling effects that are only visible at the phosphoproteomic level.

## When to Use Each Approach

| Question | Genomics | Phosphoproteomics | Both |
|----------|----------|-------------------|------|
| Identify actionable driver mutations | Yes | No | -- |
| Determine which signaling pathways are active | No | Yes | -- |
| Predict kinase inhibitor sensitivity | Limited | Yes | Preferred |
| Detect drug resistance mechanisms | Late (months) | Early (hours-days) | Preferred |
| Classify tumor subtypes | Yes | Yes | Most informative |
| Identify clonal structure | Yes | No | -- |
| Measure dynamic treatment response | No | Yes | -- |
| Assess immunotherapy biomarkers | PD-L1 amplification, TMB | Immune signaling phosphosites | Preferred |
| Screen for hereditary cancer risk | Yes | No | -- |
| Discover novel therapeutic targets | Recurrence-based | Activity-based | Complementary |
