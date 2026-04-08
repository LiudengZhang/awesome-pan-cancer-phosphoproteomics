# decoupleR

**Verdict:** The Swiss army knife of activity inference -- not the best at any single method, but the unified API that makes method comparison practical.

**Citation:** Badia-i-Mompel P, Velez Santiago J, Braunger J, et al. "decoupleR: ensemble of computational methods to infer biological activities from omics data." *Bioinformatics Advances* 2(1):vbac016 (2022). [DOI: 10.1093/bioadv/vbac016](https://doi.org/10.1093/bioadv/vbac016)

## Problem Setup

Kinase activity, transcription factor activity, and pathway scores all require inferring regulator activity from target measurements. Dozens of methods exist (VIPER, GSVA, ULM, WMEAN, etc.), each with different implementations, input formats, and assumptions. Comparing them requires writing glue code for every method. decoupleR asks: can a unified framework wrap these methods behind a single API?

## Approach

decoupleR provides a consistent R and Python interface for multiple activity inference methods. Users supply a matrix of measurements (e.g., phosphosite intensities) and a prior knowledge network (e.g., kinase-substrate relationships from OmniPath). The package runs any combination of methods -- univariate linear model (ULM), multivariate linear model (MLM), weighted mean (WMEAN), VIPER, GSVA, and others -- and returns activity scores in a standardized output format. The key abstraction is separating the statistical method from the prior knowledge source.

## Key Findings

- ULM (univariate linear model) and MLM perform surprisingly well relative to more complex methods like VIPER for kinase activity inference.
- Method agreement varies substantially across regulators -- some kinases get consistent scores regardless of method, others do not.
- Prior knowledge quality matters more than method choice in most benchmarks.
- The package integrates natively with Scanpy/AnnData (Python) and Seurat (R) ecosystems.
- Consensus scoring across methods improves robustness compared to any single method.

## Evaluation

Benchmarked on perturbation datasets where the ground truth activity change is known (kinase inhibitor treatments, gene knockdowns). Methods ranked by ability to recover the perturbed regulator. Also tested on CPTAC tumor data for biological plausibility. The benchmarking framework itself is a contribution -- it standardizes how activity inference methods should be evaluated.

## Honest Assessment

**Strengths:**

- Unified API eliminates the practical barrier to method comparison -- this alone is a major contribution.
- Tight integration with scverse (AnnData) and Seurat ecosystems makes adoption seamless.
- Actively maintained by the Saez-Rodriguez lab with regular updates.
- The separation of method from prior knowledge is a clean design that enables systematic ablation studies.

**Limitations:**

- Wrapping existing methods does not fix their fundamental assumptions -- garbage prior knowledge in, garbage activity scores out.
- The package does not provide guidance on which method to use for a specific biological context; users must benchmark themselves.
- Some wrapped methods (e.g., VIPER) are simplified reimplementations, not exact ports, which can produce slightly different results than the original packages.
- Performance on phosphoproteomics specifically is less validated than on transcriptomics.

**Design Decision:** Build a meta-framework rather than a new method. This bets that the field's bottleneck is practical usability and method comparison, not algorithmic innovation. Given that benchmarKIN later showed no single method dominates, this bet paid off -- the ability to run and compare multiple methods matters more than picking the "right" one.
