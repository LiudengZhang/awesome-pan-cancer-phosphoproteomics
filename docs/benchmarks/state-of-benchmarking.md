# State of Benchmarking

## The Problem

Benchmarking kinase-substrate inference and phosphosite analysis tools is fundamentally harder than benchmarking most bioinformatics methods. The ground truth is sparse, biased toward well-studied kinases, and the definition of "correct" depends on the application.

## Major Benchmarks

### benchmarKIN (Briefings in Bioinformatics, 2024)

The most comprehensive kinase activity inference benchmark to date. Compares 11 methods across multiple perturbation datasets.

**Key findings:**

- No single method dominates across all evaluation scenarios
- Enrichment-based methods (KSEAapp, decoupleR/ULM) perform well on known kinase-inhibitor perturbation data
- Motif-based methods (PhosX, KinaseLibrary-based) excel at predicting kinases for individual sites but not at activity scoring
- Network-augmented methods (RoKAI) improve performance when high-quality interaction data is available
- Ensemble approaches combining motif + enrichment consistently outperform individual methods

### Evaluation Datasets Used

| Dataset | Design | Strengths | Weaknesses |
|---|---|---|---|
| Kinase inhibitor perturbations | Treat cells with specific inhibitor, measure phospho changes | Clear ground truth (inhibited kinase should show reduced activity) | Tests only inhibition, not activation; limited to druggable kinases |
| CPTAC tumor data | Compare kinase activity across cancer subtypes | Clinically relevant; large sample sizes | No controlled perturbation; ground truth is indirect |
| Synthetic benchmarks | Simulate phosphosite changes with known kinase activities | Full control over ground truth | May not capture biological complexity |

## What Metrics Matter

### For Kinase Activity Inference

- **AUROC for known perturbations** — Can the method identify which kinase was inhibited? This is the most direct test but only covers druggable kinases.
- **Recall of known kinase-substrate pairs** — Does the method recover PhosphoSitePlus annotations? Circular if the method uses these annotations as input.
- **Consistency across replicates** — Does the method give the same answer with biological replicates?
- **Coverage** — How many kinases can the method score? Methods limited to well-annotated kinases miss the long tail.

### For Phosphosite Identification

- **Localization accuracy** — Phospho(STY) probability scores from MaxQuant/Spectronaut. Sites with probability >0.75 are standard cutoff.
- **Quantitative reproducibility** — CV across replicates. DIA methods typically show lower CVs than DDA.
- **Depth** — Number of quantified phosphosites per sample. Current state-of-the-art: 15,000-40,000 sites per sample.

## The Circularity Problem

Most kinase-substrate inference methods are evaluated against PhosphoSitePlus annotations. Many of these same methods use PhosphoSitePlus as training data or prior knowledge. This creates an evaluation circularity:

1. Method is trained/configured using known kinase-substrate pairs from PhosphoSitePlus
2. Method is evaluated on its ability to recover kinase-substrate pairs from PhosphoSitePlus
3. Performance on truly novel kinase-substrate relationships remains unknown

The benchmarKIN study partially addresses this by using kinase inhibitor perturbation data as an orthogonal evaluation, but even this tests activity inference rather than substrate prediction directly.

## Recommendations

- Use multiple evaluation frameworks (perturbation data + known substrates + cross-validation)
- Report coverage alongside accuracy — a method scoring 300 kinases at 60% accuracy may be more useful than one scoring 30 kinases at 90%
- Distinguish between activity inference (which kinase is active?) and substrate prediction (which sites does a kinase phosphorylate?) — these are different tasks requiring different benchmarks
