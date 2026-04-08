# From Sites to Circuits

## The Gap

A phosphosite is a coordinate — a specific serine, threonine, or tyrosine on a specific protein. A signaling circuit is a causal chain — kinase A activates kinase B, which phosphorylates transcription factor C, which drives gene expression program D. The gap between these two levels of description is where the field's most important unsolved problems live.

## Level 1: Sites

Mass spectrometry produces a list of phosphosites with quantitative values. This is the raw material. A typical experiment yields 10,000–40,000 quantified sites. Pan-cancer atlases reach 100,000+.

At this level, the data is rich but uninterpretable. A phosphosite that increases 3-fold in tumors could be a driver event, a passenger modification, or an artifact of changed protein abundance. Without context, sites are just coordinates.

**Tools at this level:** MaxQuant, FragPipe, DIA-NN, Spectronaut

## Level 2: Kinase Activities

Kinase-substrate inference methods aggregate phosphosite changes into kinase activity scores. If many known AKT substrates increase in a sample, AKT is inferred to be active.

This step transforms thousands of sites into scores for tens to hundreds of kinases — a massive dimensionality reduction that enables biological interpretation. But it depends entirely on the quality and completeness of kinase-substrate annotations (see [The Annotation Bottleneck](annotation-bottleneck.md)).

**Tools at this level:** KSEAapp, decoupleR, PhosX, INKA, KSTAR

## Level 3: Pathways

Pathway reconstruction methods connect individual kinase activities into causal signaling networks. Given that AKT is active and mTOR substrates are phosphorylated, these tools infer the AKT → mTOR signaling axis.

This requires prior knowledge about which proteins can interact and which kinases can phosphorylate which targets. Tools like CARNIVAL and COSMOS use integer linear programming to find the most parsimonious signaling topology consistent with the data.

**Tools at this level:** PHONEMeS, CARNIVAL, COSMOS, CausalPath

## Level 4: Circuits and Therapeutic Targets

The ultimate goal: a wiring diagram of active signaling in a tumor, with nodes that can be targeted by drugs. If the reconstructed circuit shows that bypass signaling through MET compensates for EGFR inhibition, this suggests adding a MET inhibitor.

Few tools operate at this level, and none do so reliably. The challenge is compounding uncertainty — errors at each level propagate upward. An incorrect kinase-substrate annotation at Level 2 produces a wrong pathway at Level 3 and a misleading therapeutic prediction at Level 4.

**Tools at this level:** COSMOS (multi-omic), Cao et al. 2024 (phospho-to-drug)

## The Compounding Uncertainty Problem

Each transition between levels introduces error:

| Transition | Source of Error | Magnitude |
|---|---|---|
| Sites → Kinases | Incomplete annotations, motif degeneracy | High — <5% of sites have kinase |
| Kinases → Pathways | Prior knowledge gaps, context dependence | Medium — well-studied pathways work |
| Pathways → Targets | Pharmacology complexity, resistance | High — biology defeats simple models |

This compounding means that a signaling circuit reconstructed from phosphoproteomics data alone should be treated as a hypothesis generator, not a validated wiring diagram.

## What Would Close the Gap

1. **Systematic kinase-substrate mapping** at the scale of the KinaseLibrary but in cellular context (not just in vitro motifs)
2. **Temporal phosphoproteomics** capturing signaling dynamics after perturbation, not just steady-state snapshots
3. **Single-cell phosphoproteomics** resolving tumor heterogeneity (current methods average across millions of cells)
4. **Closed-loop validation** where computational predictions are systematically tested experimentally and fed back into models

The field is moving from Level 1 (sites) toward Level 4 (circuits), but the journey is not linear. Each level has its own bottlenecks, and progress at one level does not automatically translate to progress at the next.
