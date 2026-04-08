# Cantley KinaseLibrary

**Verdict:** The gold standard for kinase-substrate motif specificity -- nothing else comes close in coverage, but motifs alone cannot predict signaling in cells.

**Citation:** Johnson JL, Yaron TM, Huntsman EM, et al. "An atlas of substrate specificities for the human serine/threonine kinome." *Nature* 613:759-766 (2023). [DOI: 10.1038/s41586-022-05575-3](https://doi.org/10.1038/s41586-022-05575-3)

## Problem Setup

Which kinase phosphorylates which substrate? Answering this question is fundamental to interpreting phosphoproteomics data. Previous motif databases covered a fraction of the kinome. This study asks: can systematic in vitro profiling of 303 serine/threonine kinases produce a comprehensive specificity atlas?

## Approach

Positional scanning peptide library arrays (PSPL) measure the preference of each kinase for every amino acid at positions surrounding the phosphosite (-5 to +4). Each kinase is profiled against a degenerate peptide library where one position is fixed and all others randomized. The resulting position-specific scoring matrices (PSSMs) define the intrinsic substrate specificity of each kinase. These PSSMs are compiled into the KinaseLibrary, a searchable web tool for scoring any phosphosite against all profiled kinases.

## Key Findings

- 303 Ser/Thr kinases profiled, covering ~84% of the expressed human Ser/Thr kinome.
- Kinases cluster into specificity groups that largely (but not perfectly) track with phylogenetic families.
- Many kinases share highly similar motifs, making unambiguous assignment from motif alone impossible for large kinase families.
- The scoring matrices outperform previous motif databases (PhosphoSitePlus, NetPhorest) at predicting known kinase-substrate pairs.
- Proline-directed, basophilic, and acidophilic specificity classes dominate the kinome.

## Evaluation

Benchmarked against known kinase-substrate relationships from PhosphoSitePlus. Receiver operating characteristic (ROC) analysis across kinases. Validated select predictions by in vitro kinase assays. Performance degrades for kinases whose specificity depends heavily on distal docking interactions rather than local sequence.

## Honest Assessment

**Strengths:**

- Most comprehensive kinase motif resource available -- 303 kinases in a single consistent experimental framework.
- In vitro PSPL avoids biases inherent in database-curated substrate lists.
- Freely accessible web tool and downloadable PSSMs enable direct integration into phosphoproteomics pipelines.
- Quantitative scoring matrices, not binary motif logos, allow probabilistic kinase-substrate assignment.

**Limitations:**

- In vitro motifs do not capture cellular context: co-localization, scaffolding, activation state, and competing substrates all determine which sites get phosphorylated in vivo.
- Tyrosine kinases are excluded (a separate study covers them, but the combined resource is not yet unified).
- Degenerate peptide libraries miss specificity driven by structured substrates or distal docking motifs.
- Motif similarity between related kinases means the library cannot distinguish closely related family members from sequence alone.

**Design Decision:** Measure intrinsic specificity in vitro rather than infer motifs from observed substrates in databases. This avoids the circular logic of database-derived motifs (which are biased toward well-studied kinases) but sacrifices biological context. The right trade-off for building a reference -- cellular context must be layered on top by downstream methods.
