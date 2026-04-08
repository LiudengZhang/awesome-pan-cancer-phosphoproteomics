# COSMOS

**Verdict:** The most ambitious multi-omics pathway reconstruction framework -- intellectually compelling but demanding enough that few labs can actually run it.

**Citation:** Dugourd A, Kuppe C, Sciacovelli M, et al. "Causal integration of multi-omics data with prior knowledge to generate mechanistic hypotheses." *Molecular Systems Biology* 17(1):e9730 (2021). [DOI: 10.15252/msb.20209730](https://doi.org/10.15252/msb.20209730)

## Problem Setup

Multi-omics datasets (phosphoproteomics, transcriptomics, metabolomics) each capture a different slice of cellular state. How can these layers be connected into coherent mechanistic models? Simply overlaying data on pathway diagrams is ad hoc. COSMOS asks: can integer linear programming (ILP) with causal prior knowledge reconstruct the signaling and metabolic paths connecting measured molecular changes?

## Approach

COSMOS (Causal Oriented Search of Multi-Omic Space) takes as input activity scores from each omics layer -- kinase activities from phosphoproteomics, TF activities from transcriptomics, metabolite changes from metabolomics. It queries the OmniPath database for a causal prior knowledge network connecting kinases, TFs, enzymes, and metabolites. An ILP optimization then finds the subnetwork that best explains the observed activity changes while respecting causal directionality (activation/inhibition). The solution is a mechanistic hypothesis connecting upstream signals to downstream effects through intermediate nodes.

## Key Findings

- Reconstructed signaling-to-metabolism paths in a renal cell carcinoma dataset that connected HIF pathway activation to specific metabolic rewiring.
- Identified non-obvious intermediate nodes (kinases, TFs) connecting measured upstream and downstream changes.
- Multi-omics integration outperformed single-omics pathway analysis at recovering known biology.
- The prior knowledge network is critical -- results depend heavily on OmniPath coverage.
- Generated testable hypotheses about signaling crosstalk that were partially validated experimentally.

## Evaluation

Applied to matched multi-omics from renal cell carcinoma (Sciacovelli et al.) and cardiac fibrosis (Kuppe et al.). Reconstructed pathways assessed for overlap with known biology and experimental validation of select predictions. No systematic benchmark against alternative integration methods due to the absence of comparable tools at the time of publication.

## Honest Assessment

**Strengths:**

- Uniquely integrates three omics layers through a mechanistic, causal framework rather than statistical correlation.
- The ILP formulation enforces biological plausibility by respecting causal sign consistency.
- Generates specific, testable mechanistic hypotheses rather than enrichment scores.
- Built on OmniPath, which is the most comprehensive signaling prior knowledge resource available.

**Limitations:**

- Extremely complex to run -- requires pre-computed activity scores from each omics layer, careful parameter tuning, and significant computational expertise.
- Results are highly sensitive to prior knowledge completeness; pathways absent from OmniPath cannot be recovered.
- The ILP optimization can produce multiple equally optimal solutions, and the framework provides limited guidance on choosing among them.
- Scalability to large pan-cancer datasets (thousands of samples) is untested; most applications involve single comparisons (e.g., tumor vs. normal).
- Validation remains limited to a few case studies.

**Design Decision:** Causal reconstruction via ILP rather than correlation-based network inference. This is the most intellectually honest approach to multi-omics integration -- it forces explicit mechanistic reasoning -- but the practical barrier is high. The bet is that mechanistic specificity is worth the complexity cost. Whether the field follows this path depends on whether the tools become more accessible.
