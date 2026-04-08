# What to Measure

## Two Different Questions

Phosphoproteomics benchmarking conflates two fundamentally different tasks:

| Task | Question | Ground Truth | Typical Methods |
|---|---|---|---|
| **Substrate prediction** | Which kinase phosphorylates this site? | Curated kinase-substrate databases | KinaseLibrary, GPS, NetworKIN |
| **Activity inference** | Which kinases are active in this sample? | Perturbation experiments | KSEAapp, decoupleR, INKA |

A method can excel at one and fail at the other. GPS 6.0 predicts kinase-substrate relationships well but does not score kinase activity from differential phosphoproteomics. Conversely, KSEAapp infers kinase activity effectively but relies entirely on pre-existing substrate annotations.

## Metrics by Task

### Substrate Prediction Metrics

- **Precision at k** — Among the top-k predicted substrates for a kinase, how many are true? More informative than AUROC when the positive-to-negative ratio is extreme (as it always is — each kinase has <100 known substrates among ~240K sites).
- **Kinase coverage** — How many kinases can the method make predictions for? Methods relying on known substrates are limited to well-studied kinases.
- **Cross-validated AUROC** — Standard but misleading if train and test sets share the same kinase annotations.

### Activity Inference Metrics

- **Perturbation recovery** — After kinase inhibitor treatment, does the inferred activity of the target kinase decrease? The gold standard for activity inference.
- **Specificity** — Among all scored kinases, is only the target kinase affected, or do many kinases show spurious activity changes?
- **Sensitivity to input size** — How many differential phosphosites are needed for reliable inference? Methods requiring >500 sites are impractical for small experiments.

## The Missing Benchmark

No current benchmark adequately tests **novel substrate prediction** — predicting kinase-substrate relationships not in any training database. This matters because:

- The annotation bottleneck means most real-world phosphosites have no known kinase
- Methods trained on known substrates may simply memorize patterns of well-studied kinases
- The field needs tools that generalize to the ~95% of phosphosites without annotations

A proper novel-substrate benchmark would require:

1. Holding out entire kinase families from training
2. Testing prediction on those held-out families
3. Validating predictions experimentally (not against other databases)

Until this benchmark exists, claims about kinase-substrate prediction accuracy should be interpreted cautiously.

## Practical Guidance

| Scenario | Recommended Evaluation | Watch Out For |
|---|---|---|
| Choosing a kinase inference tool for CPTAC data | perturbation recovery + coverage | Methods that only score 30-50 kinases |
| Predicting kinase for a novel phosphosite | Cross-validated substrate prediction + motif quality | Circularity with PhosphoSitePlus |
| Scoring functional importance of a site | funscoR benchmark + experimental validation rate | Bias toward well-studied proteins |
| Comparing tools in a paper | benchmarKIN framework with matched datasets | Cherry-picked evaluation datasets |
