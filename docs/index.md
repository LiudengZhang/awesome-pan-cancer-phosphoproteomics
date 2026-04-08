# Awesome Pan-Cancer Phosphoproteomics

> Pan-cancer phosphoproteomics can identify thousands of sites — but without knowing which kinase, which pathway, and which drug, a catalog is not a map.

Mass spectrometry can now quantify over 100,000 phosphorylation sites across tumor types. Yet fewer than 5% of these sites have a known upstream kinase, and fewer than 3% have established functional roles. The gap between measurement and understanding defines this field.

This site is the companion to the [awesome list](https://github.com/LiudengZhang/awesome-pan-cancer-phosphoproteomics). While the list provides a curated index of tools, databases, and studies, this site goes deeper — with concept explainers, method comparisons, paper analyses, and synthesis essays that connect the pieces.

## The Central Problem

| What we can measure | What we know |
|---|---|
| ~240,000 human phosphosites cataloged | <5% have a known upstream kinase |
| 110,274 sites quantified across 10 CPTAC cancers | <3% have established functional roles |
| 518 kinases in the human kinome | 130+ kinases have zero known substrates |

The annotation bottleneck is not just a data problem — it shapes which biological questions can be asked and which therapeutic strategies can be pursued.

## How This Site Is Organized

- **[Concepts](concepts/phosphorylation-essentials.md)** — Phosphorylation biology, the kinase-substrate inference problem, and how phosphoproteomics complements genomics.
- **[Methods](methods/phosphosite-identification.md)** — Detailed guides for each tool category: identification, kinase inference, pathway reconstruction, functional scoring, pan-cancer integration, and therapeutic response.
- **[Deep Reads](deep-reads/index.md)** — Honest analyses of landmark papers.
- **[Benchmarks](benchmarks/state-of-benchmarking.md)** — The state of evaluation and what metrics actually matter.
- **[Datasets](datasets/datasets.md)** — Key datasets organized by what analyses they support.
- **[Timeline](timeline/index.md)** — Interactive literature timeline showing how the field evolved.
- **[Explorer](explorer/index.md)** — Interactive maps: a method taxonomy and a kinase-substrate-pathway-drug biology network.
- **[Synthesis](synthesis/annotation-bottleneck.md)** — Cross-cutting essays on the annotation bottleneck and the path from phosphosites to signaling circuits.
- **[Glossary](glossary.md)** — Key terms and definitions.

## Key Numbers

| Statistic | Value | Source |
|---|---|---|
| Human phosphosites cataloged | ~240,000 | PhosphoSitePlus |
| Sites with known upstream kinase | <5% | Community estimate |
| Sites with known function | <3% | Ochoa et al. 2020 |
| Ser/Thr kinases with motif data | 303 | KinaseLibrary (2023) |
| CPTAC cancer types profiled | 10+ | Geffen et al. 2023 |
| Kinase inhibitors FDA-approved | 70+ | As of 2024 |
| Phosphosites per typical experiment | 10,000–40,000 | DIA-NN / MaxQuant |
