# MIMP

**Verdict:** A pioneering method that connects the dots between cancer mutations and phosphorylation changes -- conceptually important but limited by sparse training data and the complexity of real signaling networks.

**Citation:** Wagih O, Reimand J, Bader GD. "MIMP: predicting the impact of mutations on kinase-substrate phosphorylation." *Nature Methods* 12:531-533 (2015). [DOI: 10.1038/nmeth.3396](https://doi.org/10.1038/nmeth.3396)

## Problem Setup

Cancer genomes harbor thousands of somatic mutations, but which mutations affect phosphorylation-based signaling? A mutation near a phosphosite could destroy the site itself, alter the flanking sequence to disrupt kinase recognition, or create a new motif recognized by a different kinase. MIMP asks: can computational analysis predict which mutations rewire kinase-substrate relationships?

## Approach

MIMP (Mutation Impact on Phosphorylation) analyzes mutations within a window around known phosphosites (+/- 7 residues from the phosphorylated position). For each mutation, it scores the wild-type and mutant sequence against position weight matrices (PWMs) for kinase substrate specificity. If a mutation significantly reduces the score for one kinase and/or increases it for another, MIMP predicts a kinase switch -- a rewiring event. The method also detects direct phosphosite destruction (mutation of the phosphorylated residue itself) and creation of new Ser/Thr/Tyr residues by mutation.

## Key Findings

- Applied to TCGA pan-cancer somatic mutations, MIMP identifies thousands of predicted kinase rewiring events across cancer types.
- Some predicted rewiring events affect known cancer-relevant kinase-substrate pairs (e.g., mutations disrupting AKT substrate recognition).
- Direct phosphosite destruction (mutating S/T/Y to another residue) is enriched above background in several cancer types.
- Recurrent mutations at phosphosite-flanking positions suggest selection for signaling rewiring in some tumors.
- The method is fast and scales to whole-genome/exome mutation datasets.

## Evaluation

Validated on a curated set of known mutation-phosphorylation relationships from the literature. Enrichment analysis tested whether cancer mutations are more likely to affect phosphosites than expected by chance. Compared against random expectation and simple proximity-based approaches. No large-scale experimental validation of predicted rewiring events.

## Honest Assessment

**Strengths:**

- Addresses a genuinely important and underexplored question: how do mutations mechanistically alter phospho-signaling?
- Computationally efficient -- can process entire TCGA mutation datasets.
- Conceptually bridges two fields (cancer genomics and phosphoproteomics) that often operate in isolation.
- Open-source tool with a web interface for accessibility.

**Limitations:**

- Relies entirely on linear motif recognition (PWMs), which captures only part of kinase-substrate specificity; docking interactions, localization, and scaffolding are ignored.
- The kinase motif library used (circa 2015) covers far fewer kinases than the current KinaseLibrary; predictions are limited to well-characterized kinases.
- No way to distinguish a predicted rewiring event that actually matters for cell biology from one that is biochemically real but phenotypically irrelevant.
- Most predicted rewiring events lack experimental validation, so the false positive rate is unknown.
- Does not account for the stoichiometry or abundance of the affected substrate.

**Design Decision:** Use linear motif scoring as a fast, scalable proxy for kinase-substrate compatibility. This is a pragmatic simplification that enables genome-wide analysis but limits predictive accuracy. The approach was ahead of its time in 2015 -- with better kinase motif data (KinaseLibrary 2023) and larger phosphoproteomics datasets (CPTAC), the core idea deserves revisiting with updated resources.
