# Literature Timeline

Interactive timeline of key publications in pan-cancer phosphoproteomics. Hover over items for details. Filter by category using the buttons below.

<div id="timeline-controls" style="margin-bottom: 1rem; display: flex; gap: 0.5rem; flex-wrap: wrap;">
  <button class="tl-btn active" data-group="all" style="padding: 0.3rem 0.8rem; border-radius: 4px; border: 1px solid #009688; background: #009688; color: white; cursor: pointer; font-size: 0.85rem;">All</button>
  <button class="tl-btn" data-group="Identification" style="padding: 0.3rem 0.8rem; border-radius: 4px; border: 1px solid #1976D2; background: white; color: #1976D2; cursor: pointer; font-size: 0.85rem;">Identification</button>
  <button class="tl-btn" data-group="Kinase Inference" style="padding: 0.3rem 0.8rem; border-radius: 4px; border: 1px solid #E64A19; background: white; color: #E64A19; cursor: pointer; font-size: 0.85rem;">Kinase Inference</button>
  <button class="tl-btn" data-group="Pathway" style="padding: 0.3rem 0.8rem; border-radius: 4px; border: 1px solid #7B1FA2; background: white; color: #7B1FA2; cursor: pointer; font-size: 0.85rem;">Pathway</button>
  <button class="tl-btn" data-group="Pan-Cancer" style="padding: 0.3rem 0.8rem; border-radius: 4px; border: 1px solid #2E7D32; background: white; color: #2E7D32; cursor: pointer; font-size: 0.85rem;">Pan-Cancer</button>
  <button class="tl-btn" data-group="Database" style="padding: 0.3rem 0.8rem; border-radius: 4px; border: 1px solid #F57F17; background: white; color: #F57F17; cursor: pointer; font-size: 0.85rem;">Database</button>
  <button class="tl-btn" data-group="Benchmark" style="padding: 0.3rem 0.8rem; border-radius: 4px; border: 1px solid #455A64; background: white; color: #455A64; cursor: pointer; font-size: 0.85rem;">Benchmark</button>
</div>

<div id="timeline" style="width: 100%; height: 500px; border: 1px solid #e0e0e0; border-radius: 8px;"></div>

<link href="https://unpkg.com/vis-timeline@7.7.3/styles/vis-timeline-graph2d.min.css" rel="stylesheet" />
<script src="https://unpkg.com/vis-timeline@7.7.3/standalone/umd/vis-timeline-graph2d.min.js"></script>

<script>
var groups = new vis.DataSet([
  {id: 'Identification', content: 'Identification', style: 'color: #1976D2;'},
  {id: 'Kinase Inference', content: 'Kinase Inference', style: 'color: #E64A19;'},
  {id: 'Pathway', content: 'Pathway', style: 'color: #7B1FA2;'},
  {id: 'Pan-Cancer', content: 'Pan-Cancer', style: 'color: #2E7D32;'},
  {id: 'Database', content: 'Database', style: 'color: #F57F17;'},
  {id: 'Benchmark', content: 'Benchmark', style: 'color: #455A64;'}
]);

var items = new vis.DataSet([
  {id: 1, content: 'NetPhos', start: '2004-01-01', group: 'Identification', title: 'NetPhos 3.1 — Neural network Ser/Thr/Tyr predictor (Proteomics, 2004)', style: 'background-color: #BBDEFB;'},
  {id: 2, content: 'PhosphoSitePlus', start: '2004-01-01', group: 'Database', title: 'PhosphoSitePlus — Primary curated phosphosite database', style: 'background-color: #FFF9C4;'},
  {id: 3, content: 'Phospho.ELM', start: '2004-01-01', group: 'Database', title: 'Phospho.ELM — Experimentally verified phosphosites', style: 'background-color: #FFF9C4;'},
  {id: 4, content: 'NetworKIN', start: '2007-09-01', group: 'Kinase Inference', title: 'NetworKIN — Motif + network context for kinase prediction (Sci Signal, 2007)', style: 'background-color: #FFCCBC;'},
  {id: 5, content: 'MaxQuant', start: '2008-01-01', group: 'Identification', title: 'MaxQuant — Gold standard search engine for phosphoproteomics (Nat Biotech, 2008)', style: 'background-color: #BBDEFB;'},
  {id: 6, content: 'MIMP', start: '2015-06-01', group: 'Kinase Inference', title: 'MIMP — Mutation impact on phosphorylation (Nat Methods, 2015)', style: 'background-color: #FFCCBC;'},
  {id: 7, content: 'PHONEMeS', start: '2015-01-01', group: 'Pathway', title: 'PHONEMeS — ILP pathway reconstruction from phospho data (PLOS Comp Bio, 2015)', style: 'background-color: #E1BEE7;'},
  {id: 8, content: 'OmniPath', start: '2016-11-01', group: 'Database', title: 'OmniPath — Meta-resource: 100+ signaling databases unified (Mol Sys Bio, 2016)', style: 'background-color: #FFF9C4;'},
  {id: 9, content: 'KSEAapp', start: '2017-01-01', group: 'Kinase Inference', title: 'KSEAapp — Kinase-substrate enrichment analysis (Bioinformatics, 2017)', style: 'background-color: #FFCCBC;'},
  {id: 10, content: 'FragPipe', start: '2017-06-01', group: 'Identification', title: 'FragPipe/MSFragger — Ultra-fast search with PTMProphet (Nat Methods, 2017)', style: 'background-color: #BBDEFB;'},
  {id: 11, content: 'CausalPath', start: '2018-01-01', group: 'Pathway', title: 'CausalPath — Causal signaling from phospho data (PLOS Comp Bio, 2018)', style: 'background-color: #E1BEE7;'},
  {id: 12, content: 'DeepPhos', start: '2019-01-01', group: 'Identification', title: 'DeepPhos — Deep learning phosphosite predictor (Bioinformatics, 2019)', style: 'background-color: #BBDEFB;'},
  {id: 13, content: 'CARNIVAL', start: '2019-01-01', group: 'Pathway', title: 'CARNIVAL — Causal network optimization via ILP (npj Sys Bio, 2019)', style: 'background-color: #E1BEE7;'},
  {id: 14, content: 'INKA', start: '2019-01-01', group: 'Kinase Inference', title: 'INKA — Integrative inferred kinase activity (Mol Sys Bio, 2019)', style: 'background-color: #FFCCBC;'},
  {id: 15, content: 'PTMsigDB', start: '2019-01-01', group: 'Database', title: 'PTMsigDB — Phosphosite signatures for enrichment (MCP, 2019)', style: 'background-color: #FFF9C4;'},
  {id: 16, content: 'Krug (Breast)', start: '2020-06-01', group: 'Pan-Cancer', title: 'Krug et al. — CPTAC breast cancer phosphoproteomics (Cell, 2020)', style: 'background-color: #C8E6C9;'},
  {id: 17, content: 'DIA-NN', start: '2020-01-01', group: 'Identification', title: 'DIA-NN — Neural network DIA analysis (Nat Methods, 2020)', style: 'background-color: #BBDEFB;'},
  {id: 18, content: 'MusiteDeep', start: '2020-01-01', group: 'Identification', title: 'MusiteDeep — Transfer learning PTM prediction (NAR, 2020)', style: 'background-color: #BBDEFB;'},
  {id: 19, content: 'iGPS', start: '2020-01-01', group: 'Kinase Inference', title: 'iGPS — GPS + PPI network context (Mol Cell, 2020)', style: 'background-color: #FFCCBC;'},
  {id: 20, content: 'funscoR', start: '2021-01-01', group: 'Benchmark', title: 'funscoR — Functional phosphosite scoring (Mol Sys Bio, 2021)', style: 'background-color: #CFD8DC;'},
  {id: 21, content: 'COSMOS', start: '2021-01-01', group: 'Pathway', title: 'COSMOS — Multi-omics causal integration (Mol Sys Bio, 2021)', style: 'background-color: #E1BEE7;'},
  {id: 22, content: 'KEA3', start: '2021-01-01', group: 'Kinase Inference', title: 'KEA3 — Multi-library kinase enrichment (NAR, 2021)', style: 'background-color: #FFCCBC;'},
  {id: 23, content: 'RoKAI', start: '2021-01-01', group: 'Kinase Inference', title: 'RoKAI — Network propagation for kinase inference (NAR, 2021)', style: 'background-color: #FFCCBC;'},
  {id: 24, content: 'PhosR', start: '2021-01-01', group: 'Pathway', title: 'PhosR — Comprehensive phosphoproteomics analysis in R (NAR, 2021)', style: 'background-color: #E1BEE7;'},
  {id: 25, content: 'decoupleR', start: '2022-01-01', group: 'Kinase Inference', title: 'decoupleR — Unified activity inference framework (Bioinf Adv, 2022)', style: 'background-color: #FFCCBC;'},
  {id: 26, content: 'KSTAR', start: '2022-01-01', group: 'Kinase Inference', title: 'KSTAR — Kinase-substrate activity relationships (Mol Sys Bio, 2022)', style: 'background-color: #FFCCBC;'},
  {id: 27, content: 'AlphaPept', start: '2022-01-01', group: 'Identification', title: 'AlphaPept — Open-source Python proteomics pipeline (Nat Comm, 2022)', style: 'background-color: #BBDEFB;'},
  {id: 28, content: 'Geffen (Pan-Cancer)', start: '2023-03-01', group: 'Pan-Cancer', title: 'Geffen et al. — 110K phosphosites across 10 CPTAC cancers (Cell, 2023)', style: 'background-color: #C8E6C9;'},
  {id: 29, content: 'Vasaikar (CPTAC)', start: '2023-07-01', group: 'Pan-Cancer', title: 'Vasaikar et al. — 1,524 tumors, 14 cancer types (Cancer Cell, 2023)', style: 'background-color: #C8E6C9;'},
  {id: 30, content: 'Li (Kinase)', start: '2023-07-01', group: 'Pan-Cancer', title: 'Li et al. — Pan-cancer kinase activity landscape (Cell, 2023)', style: 'background-color: #C8E6C9;'},
  {id: 31, content: 'KinaseLibrary', start: '2023-01-01', group: 'Kinase Inference', title: 'KinaseLibrary — 303 Ser/Thr kinase motifs (Nature, 2023)', style: 'background-color: #FFCCBC;'},
  {id: 32, content: 'GPS 6.0', start: '2023-01-01', group: 'Kinase Inference', title: 'GPS 6.0 — 617 kinase prediction system (NAR, 2023)', style: 'background-color: #FFCCBC;'},
  {id: 33, content: 'PhosX', start: '2024-01-01', group: 'Kinase Inference', title: 'PhosX — Annotation-free kinase activity from motifs (Bioinformatics, 2024)', style: 'background-color: #FFCCBC;'},
  {id: 34, content: 'benchmarKIN', start: '2024-01-01', group: 'Benchmark', title: 'benchmarKIN — 11 kinase inference methods compared (Brief Bioinf, 2024)', style: 'background-color: #CFD8DC;'},
  {id: 35, content: 'Cao (Drug)', start: '2024-01-01', group: 'Pan-Cancer', title: 'Cao et al. — Phospho-to-drug sensitivity prediction (Cancer Disc, 2024)', style: 'background-color: #C8E6C9;'}
]);

var container = document.getElementById('timeline');
var options = {
  stack: true,
  horizontalScroll: true,
  zoomKey: 'ctrlKey',
  maxHeight: 500,
  start: '2003-01-01',
  end: '2025-06-01',
  tooltip: {followMouse: true, overflowMethod: 'cap'},
  groupOrder: function(a, b) {
    var order = ['Identification', 'Kinase Inference', 'Pathway', 'Pan-Cancer', 'Database', 'Benchmark'];
    return order.indexOf(a.id) - order.indexOf(b.id);
  }
};

var timeline = new vis.Timeline(container, items, groups, options);

// Filter buttons
document.querySelectorAll('.tl-btn').forEach(function(btn) {
  btn.addEventListener('click', function() {
    document.querySelectorAll('.tl-btn').forEach(function(b) {
      b.style.background = 'white';
      b.style.color = b.style.borderColor;
    });
    this.style.background = this.style.borderColor || '#009688';
    this.style.color = 'white';

    var group = this.getAttribute('data-group');
    if (group === 'all') {
      items.forEach(function(item) { items.update({id: item.id, visible: true}); });
    } else {
      items.forEach(function(item) {
        items.update({id: item.id, visible: item.group === group});
      });
    }
  });
});
</script>

<style>
.vis-item { border-radius: 4px; font-size: 0.8rem; }
.vis-item .vis-item-content { padding: 3px 8px; }
</style>

---

## How to Read This Timeline

- **Scroll horizontally** to navigate through time (2004-2025)
- **Hover** over items for paper details
- **Filter** by category using the buttons above
- **Zoom** with Ctrl+scroll

The timeline reveals several patterns:

1. **2004-2008**: Foundation era — databases (PhosphoSitePlus) and search engines (MaxQuant) established
2. **2015-2019**: Methods explosion — kinase inference tools, pathway reconstruction, and ILP approaches
3. **2020-2022**: The DIA shift and activity inference frameworks (DIA-NN, decoupleR)
4. **2023-2024**: Pan-cancer atlas era (CPTAC at scale) and comprehensive motif data (KinaseLibrary)
