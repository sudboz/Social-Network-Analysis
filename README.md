# Network Analysis of the Map of Science
Structural analysis of a scientific knowledge graph built from English Wikipedia. This project explores the topology, community structure, and centrality of 687 scientific fields connected by content similarity, using Python and igraph.
 
Social Network Analysis  
**Author:** Sude Boz
 
---
 
## Dataset
 
The network is sourced from **Calderone (2020)**, extracted from English Wikipedia.
 
| Property | Value |
|---|---|
| Nodes | 687 scientific fields |
| Edges | 6,523 similarity links |
| Edge weight | Cosine similarity between Wikipedia page contents |
| Node attributes | `name`, `Class` (Applied / Formal / Natural / Social), `WikipediaUrl` |
 
Each node is a Wikipedia page about a scientific field. Two nodes are connected if their page contents are sufficiently similar (measured by cosine similarity).
 
---
 
## Analysis Overview
 
### Q1 — Network Description
Basic characterization: node/edge counts, density, and sparsity. The network has a density of ~0.028, meaning only 2.8% of all possible connections exist — a very sparse graph.
 
### Q2 — Degree Statistics
Mean degree ≈ 19, standard deviation ≈ 18. The high variance relative to the mean (and a max degree of 105 vs. a median of 14) shows that the average alone is not a good descriptor — the distribution is heavily skewed by a few hub nodes.
 
### Q3 — Degree Distribution
Plots in both linear-linear and log-log scale. The log-log scale reveals a roughly linear descending pattern consistent with a power-law-like, heavy-tailed distribution — typical of real-world networks.
 
### Q4 — Degree Assortativity
Assortativity ≈ 0.24 (mildly positive). High-degree fields tend to connect to other high-degree fields, and low-degree specialized fields cluster together.
 
### Q5 — Community Detection (Louvain)
The Louvain method detects **15 communities** with modularity **0.62**, indicating strong community structure. Comparison with the 4 ground-truth science classes (Applied, Formal, Natural, Social) using NMI = 0.34 shows partial but meaningful alignment — some communities are near-pure class clusters, while others are interdisciplinary mixes.
 
### Q6 — Centrality Analysis
Top nodes by degree and betweenness centrality are compared:
 
- **High degree + high betweenness** (e.g., Economics, Algorithm, School Psychology): true global hubs
- **High degree, low betweenness** (e.g., Cognitive Science, Information Science): local hubs within dense clusters
- **Low degree, high betweenness** (e.g., Population Biology, Evolutionary Psychology): structural bridges between communities
### Q7 — Clustering Coefficient vs. Configuration Model
The real clustering coefficient (0.47) is statistically impossible under the configuration model (mean ≈ 0.09, p-value ≈ 0). The network has far more triangular structure than expected from the degree sequence alone, consistent with the strong community structure found in Q5.
 
---
 
## Requirements
 
```
igraph
matplotlib
numpy
pandas
scipy
python-louvain
```
 
Install with:
 
```bash
pip install -r requirements.txt
```
 
---
 
## How to Run
 
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/map-of-science-network-analysis.git
   cd map-of-science-network-analysis
   ```
 
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
 
3. Open the notebook:
   ```bash
   jupyter notebook notebooks/map.ipynb
   ```
 
> Make sure the `data/MapOfScience.gml` file is in the correct location. The notebook loads it with a relative path.
 
---
 
## Project Structure
 
```
map-of-science-network-analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── MapOfScience.gml
└── notebooks/
    └── map.ipynb
```
