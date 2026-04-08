# funscoR

**Verdict:** The first systematic attempt to separate functional phosphosites from noise -- reveals that most detected phosphosites likely have no regulatory role, which is an uncomfortable but important finding.

**Citation:** Ochoa D, Jonikas M, Lawrence RT, et al. "The functional landscape of the human phosphoproteome." *Nature Biotechnology* 38:365-373 (2020). [DOI: 10.1038/s41587-019-0344-3](https://doi.org/10.1038/s41587-019-0344-3); Ochoa D, Jarnuczak AF, Vieitez C, et al. "An atlas of human kinase regulation." *Molecular Systems Biology* 17(3):e10066 (2021). [DOI: 10.15252/msb.202010066](https://doi.org/10.15252/msb.202010066)

## Problem Setup

Mass spectrometry detects over 100,000 human phosphosites, but how many are functionally relevant? Many may be non-functional "noise" -- stochastic phosphorylation with no regulatory consequence. Distinguishing functional from non-functional sites is essential for interpreting phosphoproteomics data. funscoR asks: can machine learning predict which phosphosites are likely functional?

## Approach

A random forest classifier trained on features that distinguish known functional phosphosites from background. Features include evolutionary conservation (across vertebrates), structural context (surface accessibility, proximity to functional domains), stoichiometry estimates, co-regulation patterns, and overlap with known kinase motifs. Training positives are well-characterized regulatory sites from PhosphoSitePlus (sites with known biological function). Training negatives are randomly sampled detected phosphosites. The output is a continuous functional score (0 to 1) for every detected human phosphosite.

## Key Findings

- Only approximately 15% of detected phosphosites show strong evidence of function, based on the classifier's score distribution.
- Evolutionary conservation is the single most predictive feature -- functional sites are conserved across vertebrates, non-functional sites are not.
- High-stoichiometry sites are more likely to be functional than low-stoichiometry sites.
- The functional score correlates with sensitivity to kinase inhibitor perturbation -- high-scoring sites respond more to targeted inhibition.
- The score provides a principled way to filter phosphoproteomics datasets before downstream analysis.

## Evaluation

Benchmarked via cross-validation on known functional sites. Validated by testing whether high-scoring sites are enriched among sites that respond to kinase inhibitor treatment in independent perturbation datasets. Also assessed correlation with evolutionary conservation and structural features not used in training.

## Honest Assessment

**Strengths:**

- Addresses a fundamental question that most phosphoproteomics studies ignore: is this site actually doing anything?
- Provides a practical, downloadable score for every known human phosphosite.
- The finding that ~85% of phosphosites may be non-functional is sobering and important for the field.
- Feature importance analysis is transparent and biologically interpretable.

**Limitations:**

- Training labels are circular to some degree -- "known functional" sites are biased toward well-studied kinases and pathways, so the model may underestimate functionality of sites in understudied pathways.
- The binary functional/non-functional framing is a simplification; some sites may be conditionally functional (e.g., only in specific tissues or disease states).
- Conservation-based features dominate, which means the model is essentially a sophisticated conservation filter with extra features.
- Cancer-specific phosphorylation events (neomorphic sites created by mutations) are poorly served by a model trained on conserved biology.

**Design Decision:** Frame functionality as a classification problem using curated positive examples. This is pragmatic -- the alternative (requiring experimental validation for every site) is infeasible -- but it means the model reflects current knowledge biases. The 15% estimate should be treated as a lower bound on functionality, not ground truth.
