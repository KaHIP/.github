# KaHIP &mdash; High Quality Decomposition

<p align="center">
  <img src="https://raw.githubusercontent.com/KaHIP/.github/main/profile/kahip-logo.png" alt="KaHIP Logo" width="600"/>
</p>

We develop scalable algorithms for **graph decomposition**: partitioning, clustering, cuts, process mapping, and more. Developed at the [Algorithm Engineering Group, Heidelberg University](https://ae.ifi.uni-heidelberg.de).

## What We Work On

Our research covers a broad range of graph decomposition problems:

- **Graph Partitioning** -- divide a graph into *k* balanced blocks while minimizing the edges cut between them. NP-hard and central to parallel computing, VLSI design, scientific simulations, sparse matrix factorization, and route planning. Our tools range from high-quality multilevel methods with evolutionary search, to shared-memory and distributed-memory parallel partitioners, to streaming algorithms for graphs that do not fit in memory.
- **Graph Cuts** -- find minimum and maximum edge cuts in undirected graphs. Applications include network reliability, connectivity analysis, and image segmentation. We provide shared-memory parallel algorithms for exact and inexact minimum cuts, cactus representations of all minimum cuts, and multiterminal cuts.
- **Graph Clustering** -- identify densely connected communities without requiring a predefined number of clusters. Our tools optimize modularity, support motif-based local clustering, correlation clustering on signed graphs, and streaming approaches for large-scale inputs.
- **Process Mapping** -- assign communicating processes to hardware topologies so that communication cost is minimized. Closely related to graph partitioning, but accounts for hierarchical network distances.
- **Hypergraph Partitioning** -- partition hypergraphs where edges can connect more than two vertices. We provide [FREIGHT](https://github.com/KaHIP/FREIGHT), a fast streaming hypergraph partitioner. For high-quality hypergraph partitioning, see our sister organization [KaHyPar](https://github.com/kahypar).

---

## Projects

### Graph Partitioning

| Repository | Description |
|:-----------|:------------|
| [KaHIP](https://github.com/KaHIP/KaHIP) | Flagship framework: multilevel partitioning (KaFFPa), evolutionary algorithms (KaFFPaE), distributed-memory parallel partitioning (ParHIP), edge partitioning, node ordering, and ILP-based improvement |
| [KaMinPar](https://github.com/KaHIP/KaMinPar) | Shared-memory and distributed-memory parallel partitioner optimized for speed and low memory usage |
| [mt-KaHIP](https://github.com/KaHIP/mt-KaHIP) | Shared-memory parallel multilevel graph partitioning using TBB and OpenMP |
| [HeiStream](https://github.com/KaHIP/HeiStream) | Buffered streaming graph and edge partitioner for graphs that do not fit in memory |
| [FREIGHT](https://github.com/KaHIP/FREIGHT) | Fast streaming hypergraph partitioner (SEA 2023 Best Paper Award) |
| [CompressedStreamingGraphPartitioning](https://github.com/KaHIP/CompressedStreamingGraphPartitioning) | Memory-efficient streaming partitioning via compressed block assignments |

### Process Mapping

| Repository | Description |
|:-----------|:------------|
| [VieM](https://github.com/KaHIP/VieM) | Vienna Mapping and Sparse Quadratic Assignment (superseded by [SharedMap](https://github.com/KaHIP/SharedMap)) |
| [IntegratedProcessMapping](https://github.com/KaHIP/IntegratedProcessMapping) | Integrated multilevel process mapping on hierarchical topologies (superseded by [SharedMap](https://github.com/KaHIP/SharedMap)) |
| [OnlineMultiSection](https://github.com/KaHIP/OnlineMultiSection) | Streaming process mapping and hierarchical graph partitioning |
| [SharedMap](https://github.com/KaHIP/SharedMap) | Shared-memory algorithm for process mapping |
| [mpicartreorderlib](https://github.com/KaHIP/mpicartreorderlib) | Reordering algorithms for the MPI_Cart_comm reorder flag |

### Graph Cuts

| Repository | Description |
|:-----------|:------------|
| [VieCut](https://github.com/KaHIP/VieCut) | Shared-memory parallel minimum cut algorithms (inexact, exact, cactus) |
| [HeiCut](https://github.com/KaHIP/HeiCut) | Exact minimum cuts in hypergraphs at scale using data reduction |
| [fpt-max-cut](https://github.com/KaHIP/fpt-max-cut) | FPT-based data reduction and exact/heuristic solvers for the maximum cut problem |

### Graph Clustering

| Repository | Description |
|:-----------|:------------|
| [HeidelbergMotifClustering](https://github.com/KaHIP/HeidelbergMotifClustering) | Local motif clustering via triangle-based flow and partitioning methods |
| [VieClus](https://github.com/KaHIP/VieClus) | State-of-the-art for highest possible modularity values (formerly [VieClus org](https://github.com/VieClus)) |
| [CluStRE](https://github.com/KaHIP/CluStRE) | Get good clusters fast via streaming with multi-stage refinement |
| [ScalableCorrelationClustering](https://github.com/KaHIP/ScalableCorrelationClustering) | Multilevel and memetic signed/correlation graph clustering |

---

## Quick Start

### KaHIP
```bash
brew install KaHIP/kahip/kahip
kaffpa network.graph --k 8 --preconfiguration=strong --output_filename=partition.txt
```

### KaMinPar
```bash
git clone --recursive https://github.com/KaHIP/KaMinPar.git && cd KaMinPar
cmake -B build -DCMAKE_BUILD_TYPE=Release && cmake --build build -j
./build/apps/KaMinPar -G network.graph -k 8 -t 16
```

### HeiStream
```bash
brew install KaHIP/kahip/heistream
heistream network.graph --k=8 --batch_size=32768                                        # node partitioning
heistream network.graph --k=8 --batch_size=32768 --buffer_size=65536 --run-parallel     # BuffCut (parallel)
heistream_edge network.graph --k=8 --batch_size=32768                                   # edge partitioning
```

### SharedMap
```bash
brew install KaHIP/kahip/sharedmap
SharedMap -g network.graph -h 4:8:8 -d 1:10:100 -e 0.03 -c strong -t 16
```

### VieClus
```bash
brew install KaHIP/kahip/vieclus
vieclus network.graph --time_limit=60 --output_filename=clustering.txt
```

### CluStRE
```bash
brew install KaHIP/kahip/clustre
clustre network.graph --one_pass_algorithm=modularity --mode=strong
```

### FREIGHT
```bash
brew install KaHIP/kahip/freight
hmetis_to_freight_stream hypergraph.hgr hypergraph.netl  # convert hMETIS to net-list format
freight_cut hypergraph.netl --k=8                        # hypergraph partitioning (cut-net)
freight_con hypergraph.netl --k=8                        # hypergraph partitioning (connectivity)
freight_graphs network.graph --k=8                       # graph partitioning
```

### StreamCPI
```bash
brew install KaHIP/kahip/streamcpi
stream_cpi network.graph --k=8 --rle_length=0 --kappa=20
```

### HeiCut
```bash
git clone https://github.com/KaHIP/HeiCut.git && cd HeiCut
./install_mtkahypar.sh
mkdir build && cd build && cmake -DCMAKE_BUILD_TYPE=Release .. && make
./build/heicut_kernelizer path/to/hypergraph.hgr --ordering_type=tight --lp_num_iterations=1
```

### fpt-max-cut
```bash
brew install KaHIP/kahip/fpt-max-cut
fpt_max_cut -action kernelization -f network.graph -iterations 1 -total-allowed-solver-time 10
```

### VieCut
```bash
brew install KaHIP/kahip/viecut
viecut_mincut network.graph vc                        # heuristic minimum cut
viecut_mincut_parallel network.graph exact             # exact parallel minimum cut
viecut_mincut_parallel -s -b network.graph cactus      # most balanced minimum cut
```

### HeidelbergMotifClustering
```bash
brew install KaHIP/motifclustering/motifclustering
heidelberg_motif_clustering --algorithm social --graph network.graph --seed_node 42 --output community.txt
```

### SCC (Scalable Correlation Clustering)
```bash
brew install KaHIP/kahip/scc
scc signed_network.graph --seed=0                                    # multilevel clustering
mpirun -n 4 scc_evolutionary signed_network.graph --time_limit=120   # memetic algorithm
```

