# KaHIP &mdash; Karlsruhe High Quality Partitioning

<p align="center">
  <img src="https://raw.githubusercontent.com/KaHIP/.github/main/profile/kahip-logo.png" alt="KaHIP Logo" width="600"/>
</p>

We develop scalable algorithms for **graph partitioning**: dividing a graph's vertices (or edges) into balanced blocks while minimizing the edges (or vertices) cut between them.

## The Problem

Given a graph with **N** vertices and a number **k**, the **graph partitioning problem** asks for a division of the vertex set into **k** blocks of roughly equal size such that the number of edges running between blocks is minimized. The problem is NP-hard and arises in parallel computing (load balancing, domain decomposition), VLSI design, scientific simulations, sparse matrix factorization, route planning, and many other domains.

Our tools tackle this problem at multiple levels of scale and parallelism: from high-quality multilevel methods with evolutionary search, to shared-memory and distributed-memory parallel partitioners, to streaming algorithms that partition graphs too large to fit in memory. We also provide algorithms for **edge partitioning**, **process mapping**, **node ordering** (nested dissection), and **graph clustering**. For **hypergraph partitioning**, see our sister organization [KaHyPar](https://github.com/kahypar).

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
| [IntegratedProcessMapping](https://github.com/KaHIP/IntegratedProcessMapping) | Integrated multilevel process mapping on hierarchical topologies |
| [OnlineMultiSection](https://github.com/KaHIP/OnlineMultiSection) | Streaming process mapping and hierarchical graph partitioning |

### Graph Clustering

| Repository | Description |
|:-----------|:------------|
| [VieClus](https://github.com/KaHIP/VieClus) | State-of-the-art for highest possible modularity values (formerly [VieClus org](https://github.com/VieClus)) |
| [CluStRE](https://github.com/KaHIP/CluStRE) | Get good clusters fast via streaming with multi-stage refinement |

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
git clone https://github.com/KaHIP/HeiStream.git && cd HeiStream && make
./heistream network.graph --k 8 --stream_buffer=1024
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
git clone https://github.com/KaHIP/FREIGHT.git && cd FREIGHT && make
./freight hypergraph.hgr --k 8
```

