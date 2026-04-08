# Explorer

Interactive maps for navigating the phosphoproteomics landscape. Switch between the **Method Map** (tool taxonomy) and the **Biology Map** (kinase-substrate-pathway-drug network).

<style>
.tab-container { margin-bottom: 1rem; }
.tab-btn { padding: 0.5rem 1.2rem; border: 1px solid #009688; background: white; color: #009688; cursor: pointer; font-size: 0.9rem; font-weight: 500; border-radius: 4px 4px 0 0; margin-right: 2px; }
.tab-btn.active { background: #009688; color: white; }
.tab-panel { display: none; }
.tab-panel.active { display: block; }
.cy-container { width: 100%; height: 550px; border: 1px solid #e0e0e0; border-radius: 0 8px 8px 8px; background: #fafafa; }
.legend { display: flex; gap: 1rem; flex-wrap: wrap; margin-top: 0.5rem; font-size: 0.8rem; color: #5a5a7a; }
.legend-item { display: flex; align-items: center; gap: 0.3rem; }
.legend-dot { width: 12px; height: 12px; border-radius: 50%; display: inline-block; }
</style>

<div class="tab-container">
  <button class="tab-btn active" onclick="switchTab('method')">Method Map</button>
  <button class="tab-btn" onclick="switchTab('biology')">Biology Map</button>
</div>

<div id="method-panel" class="tab-panel active">
  <div id="cy-method" class="cy-container"></div>
  <div class="legend">
    <div class="legend-item"><span class="legend-dot" style="background:#1976D2;"></span> Identification</div>
    <div class="legend-item"><span class="legend-dot" style="background:#E64A19;"></span> Kinase Inference</div>
    <div class="legend-item"><span class="legend-dot" style="background:#7B1FA2;"></span> Pathway Reconstruction</div>
    <div class="legend-item"><span class="legend-dot" style="background:#2E7D32;"></span> Functional Scoring</div>
    <div class="legend-item"><span class="legend-dot" style="background:#F57F17;"></span> Database</div>
    <div class="legend-item"><span class="legend-dot" style="background:#009688;"></span> Infrastructure</div>
  </div>
  <p style="font-size:0.85rem; color:#5a5a7a; margin-top:0.5rem;">Click a node to see details. Edges show data flow (tool A feeds into tool B). Drag nodes to rearrange.</p>
</div>

<div id="biology-panel" class="tab-panel">
  <div id="cy-biology" class="cy-container"></div>
  <div class="legend">
    <div class="legend-item"><span class="legend-dot" style="background:#E64A19;"></span> Kinase</div>
    <div class="legend-item"><span class="legend-dot" style="background:#1976D2;"></span> Substrate</div>
    <div class="legend-item"><span class="legend-dot" style="background:#7B1FA2;"></span> Pathway</div>
    <div class="legend-item"><span class="legend-dot" style="background:#2E7D32;"></span> Drug</div>
    <div class="legend-item"><span class="legend-dot" style="background:#F57F17;"></span> Cancer Type</div>
  </div>
  <p style="font-size:0.85rem; color:#5a5a7a; margin-top:0.5rem;">Click a node to highlight connections. Edges show kinase-substrate, pathway membership, and drug-target relationships.</p>
</div>

<script src="https://unpkg.com/cytoscape@3.28.1/dist/cytoscape.min.js"></script>

<script>
function switchTab(tab) {
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  if (tab === 'method') {
    document.querySelectorAll('.tab-btn')[0].classList.add('active');
    document.getElementById('method-panel').classList.add('active');
  } else {
    document.querySelectorAll('.tab-btn')[1].classList.add('active');
    document.getElementById('biology-panel').classList.add('active');
    if (!window.cyBioInitialized) { initBiology(); window.cyBioInitialized = true; }
  }
}

// === METHOD MAP ===
var cyMethod = cytoscape({
  container: document.getElementById('cy-method'),
  style: [
    {selector: 'node', style: {
      'label': 'data(label)', 'text-valign': 'center', 'text-halign': 'center',
      'background-color': 'data(color)', 'color': '#fff', 'font-size': '10px',
      'width': 'data(size)', 'height': 'data(size)', 'text-wrap': 'wrap', 'text-max-width': '80px',
      'border-width': 1, 'border-color': '#333'
    }},
    {selector: 'edge', style: {
      'width': 1.5, 'line-color': '#bbb', 'target-arrow-color': '#bbb',
      'target-arrow-shape': 'triangle', 'curve-style': 'bezier', 'arrow-scale': 0.8
    }},
    {selector: 'node:selected', style: {'border-width': 3, 'border-color': '#000'}},
    {selector: '.highlighted', style: {'background-color': '#FF5722', 'border-width': 3}},
    {selector: '.faded', style: {'opacity': 0.25}}
  ],
  elements: {
    nodes: [
      // Identification
      {data: {id: 'maxquant', label: 'MaxQuant', color: '#1976D2', size: 40, desc: 'DDA search engine, gold standard'}},
      {data: {id: 'fragpipe', label: 'FragPipe', color: '#1976D2', size: 35, desc: 'MSFragger-based, ultra-fast'}},
      {data: {id: 'diann', label: 'DIA-NN', color: '#1976D2', size: 35, desc: 'Neural network DIA analysis'}},
      {data: {id: 'alphapept', label: 'AlphaPept', color: '#1976D2', size: 28, desc: 'Open-source Python pipeline'}},
      // Kinase Inference
      {data: {id: 'klib', label: 'Kinase\nLibrary', color: '#E64A19', size: 40, desc: '303 Ser/Thr kinase motifs'}},
      {data: {id: 'kseaapp', label: 'KSEAapp', color: '#E64A19', size: 35, desc: 'Kinase-substrate enrichment'}},
      {data: {id: 'kea3', label: 'KEA3', color: '#E64A19', size: 30, desc: 'Multi-library kinase enrichment'}},
      {data: {id: 'rokai', label: 'RoKAI', color: '#E64A19', size: 30, desc: 'Network propagation kinase inference'}},
      {data: {id: 'phosx', label: 'PhosX', color: '#E64A19', size: 28, desc: 'Annotation-free motif-based'}},
      {data: {id: 'decoupler', label: 'decoupleR', color: '#E64A19', size: 38, desc: 'Unified activity inference API'}},
      {data: {id: 'gps', label: 'GPS 6.0', color: '#E64A19', size: 30, desc: '617 kinases, hierarchical'}},
      {data: {id: 'networkin', label: 'NetworKIN', color: '#E64A19', size: 28, desc: 'Motif + network context'}},
      {data: {id: 'kstar', label: 'KSTAR', color: '#E64A19', size: 28, desc: 'Kinase-substrate activity'}},
      // Pathway
      {data: {id: 'phonemes', label: 'PHONEMeS', color: '#7B1FA2', size: 32, desc: 'ILP pathway reconstruction'}},
      {data: {id: 'carnival', label: 'CARNIVAL', color: '#7B1FA2', size: 35, desc: 'Causal network optimization'}},
      {data: {id: 'cosmos', label: 'COSMOS', color: '#7B1FA2', size: 38, desc: 'Multi-omics causal integration'}},
      {data: {id: 'causalpath', label: 'CausalPath', color: '#7B1FA2', size: 30, desc: 'Causal signaling from phospho'}},
      {data: {id: 'phosr', label: 'PhosR', color: '#7B1FA2', size: 28, desc: 'R phosphoproteomics toolkit'}},
      // Functional
      {data: {id: 'funscor', label: 'funscoR', color: '#2E7D32', size: 32, desc: 'Functional phosphosite scoring'}},
      {data: {id: 'mimp', label: 'MIMP', color: '#2E7D32', size: 30, desc: 'Mutation impact on phospho'}},
      // Databases
      {data: {id: 'psp', label: 'Phospho\nSitePlus', color: '#F57F17', size: 42, desc: '~240K phosphosites, curated'}},
      {data: {id: 'omnipath', label: 'OmniPath', color: '#F57F17', size: 38, desc: '100+ databases unified'}},
      {data: {id: 'ptmsigdb', label: 'PTMsigDB', color: '#F57F17', size: 28, desc: 'Phosphosite signatures'}},
      // Infrastructure
      {data: {id: 'perseus', label: 'Perseus', color: '#009688', size: 30, desc: 'Statistical analysis platform'}},
      {data: {id: 'msstats', label: 'MSstats', color: '#009688', size: 28, desc: 'Statistical framework for PTM'}}
    ],
    edges: [
      // Data flow: identification → kinase inference
      {data: {source: 'maxquant', target: 'kseaapp'}},
      {data: {source: 'maxquant', target: 'perseus'}},
      {data: {source: 'fragpipe', target: 'kseaapp'}},
      {data: {source: 'diann', target: 'decoupler'}},
      {data: {source: 'maxquant', target: 'decoupler'}},
      // Kinase inference dependencies
      {data: {source: 'psp', target: 'kseaapp'}},
      {data: {source: 'psp', target: 'kea3'}},
      {data: {source: 'psp', target: 'rokai'}},
      {data: {source: 'klib', target: 'phosx'}},
      {data: {source: 'klib', target: 'gps'}},
      {data: {source: 'omnipath', target: 'decoupler'}},
      {data: {source: 'omnipath', target: 'networkin'}},
      {data: {source: 'ptmsigdb', target: 'decoupler'}},
      // Kinase inference → pathway
      {data: {source: 'decoupler', target: 'carnival'}},
      {data: {source: 'decoupler', target: 'cosmos'}},
      {data: {source: 'kseaapp', target: 'phonemes'}},
      {data: {source: 'omnipath', target: 'carnival'}},
      {data: {source: 'omnipath', target: 'cosmos'}},
      {data: {source: 'omnipath', target: 'phonemes'}},
      {data: {source: 'omnipath', target: 'causalpath'}},
      // Functional scoring inputs
      {data: {source: 'psp', target: 'funscor'}},
      {data: {source: 'psp', target: 'mimp'}}
    ]
  },
  layout: {name: 'cose', idealEdgeLength: 120, nodeRepulsion: 8000, padding: 30}
});

cyMethod.on('tap', 'node', function(evt) {
  cyMethod.elements().removeClass('highlighted faded');
  var node = evt.target;
  var neighborhood = node.neighborhood().add(node);
  neighborhood.addClass('highlighted');
  cyMethod.elements().not(neighborhood).addClass('faded');
});
cyMethod.on('tap', function(evt) {
  if (evt.target === cyMethod) { cyMethod.elements().removeClass('highlighted faded'); }
});

// === BIOLOGY MAP (lazy init) ===
function initBiology() {
  var cyBiology = cytoscape({
    container: document.getElementById('cy-biology'),
    style: [
      {selector: 'node', style: {
        'label': 'data(label)', 'text-valign': 'center', 'text-halign': 'center',
        'background-color': 'data(color)', 'color': '#fff', 'font-size': '9px',
        'width': 'data(size)', 'height': 'data(size)', 'text-wrap': 'wrap', 'text-max-width': '70px',
        'border-width': 1, 'border-color': '#333'
      }},
      {selector: 'edge', style: {
        'width': 1.5, 'line-color': '#ccc',
        'target-arrow-shape': 'triangle', 'target-arrow-color': '#ccc',
        'curve-style': 'bezier', 'arrow-scale': 0.7, 'label': 'data(label)',
        'font-size': '7px', 'color': '#999', 'text-rotation': 'autorotate'
      }},
      {selector: 'node:selected', style: {'border-width': 3, 'border-color': '#000'}},
      {selector: '.highlighted', style: {'border-width': 3, 'border-color': '#FF5722'}},
      {selector: '.faded', style: {'opacity': 0.2}}
    ],
    elements: {
      nodes: [
        // Kinases
        {data: {id: 'egfr', label: 'EGFR', color: '#E64A19', size: 38, type: 'kinase'}},
        {data: {id: 'braf', label: 'BRAF', color: '#E64A19', size: 35, type: 'kinase'}},
        {data: {id: 'akt1', label: 'AKT1', color: '#E64A19', size: 35, type: 'kinase'}},
        {data: {id: 'cdk4', label: 'CDK4/6', color: '#E64A19', size: 32, type: 'kinase'}},
        {data: {id: 'mtor', label: 'mTOR', color: '#E64A19', size: 33, type: 'kinase'}},
        {data: {id: 'mek1', label: 'MEK1/2', color: '#E64A19', size: 30, type: 'kinase'}},
        {data: {id: 'erk1', label: 'ERK1/2', color: '#E64A19', size: 30, type: 'kinase'}},
        {data: {id: 'src', label: 'SRC', color: '#E64A19', size: 28, type: 'kinase'}},
        {data: {id: 'jak2', label: 'JAK2', color: '#E64A19', size: 28, type: 'kinase'}},
        // Substrates / TFs
        {data: {id: 'rb1', label: 'RB1\nS807/S811', color: '#1976D2', size: 28, type: 'substrate'}},
        {data: {id: 'stat3', label: 'STAT3\nY705', color: '#1976D2', size: 28, type: 'substrate'}},
        {data: {id: 's6k', label: 'S6K\nT389', color: '#1976D2', size: 26, type: 'substrate'}},
        {data: {id: 'gsk3b', label: 'GSK3B\nS9', color: '#1976D2', size: 26, type: 'substrate'}},
        {data: {id: 'myc', label: 'MYC\nS62', color: '#1976D2', size: 26, type: 'substrate'}},
        // Pathways
        {data: {id: 'mapk', label: 'MAPK\nPathway', color: '#7B1FA2', size: 40, type: 'pathway'}},
        {data: {id: 'pi3k', label: 'PI3K/AKT\nPathway', color: '#7B1FA2', size: 40, type: 'pathway'}},
        {data: {id: 'cellcycle', label: 'Cell Cycle', color: '#7B1FA2', size: 35, type: 'pathway'}},
        {data: {id: 'jakstat', label: 'JAK/STAT', color: '#7B1FA2', size: 32, type: 'pathway'}},
        // Drugs
        {data: {id: 'osimertinib', label: 'Osimertinib', color: '#2E7D32', size: 30, type: 'drug'}},
        {data: {id: 'dabrafenib', label: 'Dabrafenib', color: '#2E7D32', size: 28, type: 'drug'}},
        {data: {id: 'palbociclib', label: 'Palbociclib', color: '#2E7D32', size: 28, type: 'drug'}},
        {data: {id: 'everolimus', label: 'Everolimus', color: '#2E7D32', size: 28, type: 'drug'}},
        {data: {id: 'trametinib', label: 'Trametinib', color: '#2E7D32', size: 28, type: 'drug'}},
        {data: {id: 'ruxolitinib', label: 'Ruxolitinib', color: '#2E7D32', size: 26, type: 'drug'}},
        // Cancer types
        {data: {id: 'nsclc', label: 'NSCLC', color: '#F57F17', size: 30, type: 'cancer'}},
        {data: {id: 'melanoma', label: 'Melanoma', color: '#F57F17', size: 28, type: 'cancer'}},
        {data: {id: 'breast', label: 'Breast', color: '#F57F17', size: 30, type: 'cancer'}},
        {data: {id: 'crc', label: 'Colorectal', color: '#F57F17', size: 28, type: 'cancer'}},
        {data: {id: 'gbm', label: 'GBM', color: '#F57F17', size: 26, type: 'cancer'}}
      ],
      edges: [
        // Kinase → substrate (phosphorylates)
        {data: {source: 'egfr', target: 'mek1', label: ''}},
        {data: {source: 'braf', target: 'mek1', label: ''}},
        {data: {source: 'mek1', target: 'erk1', label: ''}},
        {data: {source: 'erk1', target: 'myc', label: ''}},
        {data: {source: 'akt1', target: 'gsk3b', label: ''}},
        {data: {source: 'akt1', target: 'mtor', label: ''}},
        {data: {source: 'mtor', target: 's6k', label: ''}},
        {data: {source: 'cdk4', target: 'rb1', label: ''}},
        {data: {source: 'jak2', target: 'stat3', label: ''}},
        {data: {source: 'src', target: 'stat3', label: ''}},
        // Kinase → pathway
        {data: {source: 'egfr', target: 'mapk', label: ''}},
        {data: {source: 'braf', target: 'mapk', label: ''}},
        {data: {source: 'akt1', target: 'pi3k', label: ''}},
        {data: {source: 'mtor', target: 'pi3k', label: ''}},
        {data: {source: 'cdk4', target: 'cellcycle', label: ''}},
        {data: {source: 'jak2', target: 'jakstat', label: ''}},
        // Drug → kinase (inhibits)
        {data: {source: 'osimertinib', target: 'egfr', label: 'inhibits'}},
        {data: {source: 'dabrafenib', target: 'braf', label: 'inhibits'}},
        {data: {source: 'trametinib', target: 'mek1', label: 'inhibits'}},
        {data: {source: 'palbociclib', target: 'cdk4', label: 'inhibits'}},
        {data: {source: 'everolimus', target: 'mtor', label: 'inhibits'}},
        {data: {source: 'ruxolitinib', target: 'jak2', label: 'inhibits'}},
        // Cancer → kinase (frequently activated)
        {data: {source: 'nsclc', target: 'egfr', label: ''}},
        {data: {source: 'melanoma', target: 'braf', label: ''}},
        {data: {source: 'breast', target: 'cdk4', label: ''}},
        {data: {source: 'breast', target: 'akt1', label: ''}},
        {data: {source: 'crc', target: 'braf', label: ''}},
        {data: {source: 'crc', target: 'egfr', label: ''}},
        {data: {source: 'gbm', target: 'egfr', label: ''}},
        {data: {source: 'gbm', target: 'mtor', label: ''}}
      ]
    },
    layout: {name: 'cose', idealEdgeLength: 100, nodeRepulsion: 6000, padding: 30}
  });

  cyBiology.on('tap', 'node', function(evt) {
    cyBiology.elements().removeClass('highlighted faded');
    var node = evt.target;
    var neighborhood = node.neighborhood().add(node);
    neighborhood.addClass('highlighted');
    cyBiology.elements().not(neighborhood).addClass('faded');
  });
  cyBiology.on('tap', function(evt) {
    if (evt.target === cyBiology) { cyBiology.elements().removeClass('highlighted faded'); }
  });
}
</script>

---

## About These Maps

### Method Map

Shows the **data flow** between tools in a phosphoproteomics analysis pipeline. Nodes are colored by category (identification, kinase inference, pathway reconstruction, functional scoring, databases, infrastructure). Edges indicate that one tool's output feeds into another tool's input.

Key patterns visible in the map:

- **PhosphoSitePlus and OmniPath** are central hubs — most kinase inference and pathway tools depend on them as prior knowledge sources
- **decoupleR** bridges kinase inference and pathway reconstruction by providing a unified API
- The **Saez-Rodriguez lab ecosystem** (OmniPath → decoupleR → CARNIVAL/COSMOS) forms a connected subgraph

### Biology Map

Shows the **biological relationships** between kinases, substrates, pathways, drugs, and cancer types. This is a simplified representation of the signaling landscape that phosphoproteomics tools aim to reconstruct.

Key patterns:

- **EGFR** is a convergence point — targeted by osimertinib, activated in NSCLC/CRC/GBM, feeds into MAPK pathway
- **Drug-kinase-cancer triangles** show the therapeutic logic: cancer activates kinase, drug inhibits kinase
- **Pathway nodes** aggregate multiple kinases, showing how individual phosphorylation events connect to higher-order signaling programs
