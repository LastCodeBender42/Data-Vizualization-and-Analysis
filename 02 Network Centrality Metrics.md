# Network Centrality Metics

Network centrality metrics are crucial for quantifying the topology of biological systems, offering profound insights into the roles and significance of various components within these complex networks. These metrics, such as degree centrality, betweenness centrality, and closeness centrality, help identify key nodes that may represent critical proteins, genes, or metabolites in biological pathways. By evaluating the importance and influence of these nodes, researchers can pinpoint potential targets for therapeutic intervention and understand the underlying mechanisms of disease. Degree centrality highlights nodes with numerous direct connections, indicating their potential influence on network stability and function. Betweenness centrality identifies nodes that act as critical connectors or hubs, facilitating communication and interaction within the network. Closeness centrality measures how efficiently information spreads from a node to all other nodes, reflecting its overall accessibility within the network. By leveraging these centrality metrics, scientists can dissect the intricate architecture of biological systems, leading to more targeted and effective approaches in drug discovery, disease diagnosis, and treatment development.

## Contents:
- [Network Centrality as a Metric of Topology](#network-centrality-as-a-metric-of-topology)
- [Betweenness Centrality](#betweenness-centrality)
- [Closeness Centrality](#closeness-centrality)
- [Degree Centrality](#degree-centrality)
- [Eigenvector Centrality](#eigenvector-centrality)
- [Comparing Metrics of Network Centrality](#comparing-metrics-of-network-centrality)

## Network Centrality as a Metric of Topology

Before reviewing commonly utilized metrics of network centrality, it is probably best to review more basic concepts.

A graph $G$, or network, is composed of two sets of elements: A set of vertices and a set of edges. A standard formal definition of a graph is given as $G = (V, E)$. The set of vertices, or nodes. for a graph $G$ is denoted by $V(G)$. The set of edges is composed of unordered pairs of vertices and is denoted by $E(G)$. Vertices are commonly indicated using the notation $v_1, v_2, v_3,..., v_N$, where N is the size of the vertex set and we write that $(v_1, v_2, v_3,..., v_N) \subset V(G)$. Edges are given by similar notation. Where two vertices $v_i, v_j \in V(G)$ are connected by an edge, the edge is defined as $e_{ij} = (v_i,v_j) \in E(G)$. Vertices that are connected by an edge in a graph are said to be *adjacent* and the edge connecting two vertices is said to be *incident*. The total number of edges connected to a node $v_i$ is
called the *node degree* and is denoted as $\delta(v_i)$. There are three coefficients that are used to describe networks: The number of nodes, the number of edges, and the average node degree, $<\delta>$. Another fundamental concept is that of *shortest paths*. A path represents a sequence of edges that can be traced between two nodes, e.g., $v_i \rightarrow v_j \rightarrow v_k$. A shortest path is a series edges that represents the shortest distance traversed between two nodes. The formal defintion of a shortest path is given by

```math
P_s(v_i,v_j) = \min_{ij} p_{ij} \in P_{ij},
```

where $P_s(v_i,v_j)$ is the subset of minimum path length between $v_i$ and $v_j$ of the set of all possible paths $P_{ij}$. Path lengths are often used in the definition of other network metrics. 

Consider a very simple network. This network has 13 nodes that compose the vertex set $(v_1, v_2,...,v_{13}) \subset V(G)$ and 17 edges that make up the edge set $(e_{1,3}=(v_1,v_3), e_{2,3} = (v_2,v_3),...,e_{12,13} = (v_12,v_13)) \subset E(G)$. Simple inspection will show that this network has a structure, or *topology*. Network topology refers to the arrangement or distributiuon of edges among the nodes. Frequently the topology of a network can be quantified by looking at how network properties are distributed. For example, networks where the degree distribution follows a binomial pattern, then the network topology is likely *homogeneous*, i.e., the edges are uniformly distributed. Where the degree distribution follows a power-law, then the network topology is likely *inhomogeneous*, i.e., nonuniformly distributed, which is what we have with this simple network. Using this network as a baseline for comparison, four network centrality properties will be reviewed below and the nodes in the network will be scaled by the network centrality to visualize how that network centrality can be used to evaluate network topology.


---

<img width="474" alt="image" src="https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/1ccd3237-9dcb-4bcd-9d09-19cbf74a6a99">

#### NOTE: The Python code for gnerating the network images is [here](./02-network-centrality-metrics-supp.ipynb)
---

## Betweenness Centrality

Betweenness Centrality ($BC$) utilizes concept of shortest path to assign significance to vertices. In descriptive terms, the $BC$ of a vertex $v_i$ is the ratio of the number of shortest paths incident on vi to the total number of shortest path lengths in the network. Therefore, the $BC$ evaluated for any vertex $v_i$ is equal to the proportion

```math
B(v_i) = \frac{\sum s_i}{S(G)}
```

where $s_i$ denotes the set of shortest paths that include vi and $S(G)$ denotes the complete set of shortest paths for a random graph $G$. Vertices with the large BC are understood to be important for maintaining the global connectivity of the graph. Vertices with larger $BC$ also decrease the overall average path length and diameter of the graph. $BC$ also contributes to the rate of diffusion on graphs. Vertices with large $BC$ increase the rate of diffusion across the graph due to smaller average path lengths.

---

<img width="582" alt="image" src="https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/2395507f-858c-438d-8034-2846928734b0">

---

## Closeness Centrality

Closeness Centrality ($CC$) is a measure that identifies vertices that have the shortest
paths to all other nodes. In other words, these are the vertices that are at the geodesic
“center” of the graph. $CC$ is defined as

```math
C(v_i) = 1/\sum_j^N d(v_iv_j),
```

where $d(v_i, v_j)$ is the distance between $v_i$ and all other vertices $j$ in $G$. This definition of $CC$
implies that the largest possible $CC$ for $v_i$ in $G$ is $C(v_i) = 1/N$ and $C(v_i) → 0$ for vertices at
the graph periphery. Note: A vertex that is close to the center of a graph will have a $CC$ approximately equal to the radius of the graph. Given the definition of $CC$, the question arises as to whether $BC$ and $CC$ are somewhat redundant. It can be the case that nodes that are ‘close’ are also ’between’, but that is not necessarily the case. But, the principle difference between $CC$ and $BC$ are at the end points of the distances measured. $BC$ evaluates the shortest path from $v_h$ through $v_i$ to $v_j$ and $CC$ begins at $v_i$ and evaluates the distanceto every other vertex $v_j$.

---

<img width="539" alt="image" src="https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/3c864c97-3af4-4d9d-a3d7-c74e51416391">

---

## Degree Centrality 

Degree Centrality ($DC$) is simplest of the centrality measures to understand intuitively. $DC$ is just the count of all the nodes adjacent to vi or alternatively a count of the edgesincident on $v_i$. Using the definition of counting incident edges, we have

```math
D(v_i) = \sum_j^N e_{ij}
```

It does not require much imagination to rationalize the logic of degree centrality: Things that are important tend to be well-connected. Whether it’s social groups, interstate traffic, or biological pathways, things that are important exert a lot of influence over the system of interest. So, whereas $BC$ and $CC$ communicate influence, vertices with high $DC$ exert influence. Additionally, the topology of graphs with with scale-free degree distribution cohere through the existence of a small number of highly connected nodes. Targeted removal of these vertices can dramatically effect network connectivity resulting in the decomposition of large components smaller components or even bifurcation of the network.

---

<img width="549" alt="image" src="https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/5a64e5ef-e365-4ec9-aae5-4b49e0688387">


---

## Eigenvector Centrality

Eigenvector Centrality ($EC$) builds on the concept of DC. If the vertices that are the most well-connected (highest ranked by degree centrality) exert the most influence on the network, then vertices immediately adjacent to these are likely vertices that are also ”influential”. $EC$ is a concept akin to guilt-by-association. The $EC$ of a vertex $v_i$ is proportional to

```math
E(v_i) = \frac{1}{\lambda} \sum_{j=1}^N A_{ij}v_i
```

which satisfies $Av = \lambda v$. The “significance” of node $v_i$ is defined by the eigenvector of the adjacency matrix A and scaled by the inverse of the associated eigenvalue $\lambda$. The entries of $v$ are $EC$ values. The eigenvalue $\lambda$ is the largest eigenvalue of the adjacency matrix $A$. One of the consequences of this centrality measure is that in scale-free networks $EC$ ’drives’ the centrality value of vertices that are not adjacent to high degree vertices to zero. In other words, $EC$ for a vertex may be high because it has many neighbors or because it is adjacent to an influential neighbor. For this reason, in scale-free networks, $EC$ tends to result in ’clusters’ of many vertices of high $EC$ centered on high-degree vertices with large swaths of vertices in the network characterized $EC$ values near zero.

---

<img width="539" alt="image" src="https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/075c5004-0c94-482e-8b0e-e241583b183a">


---



## Comparing Metrics of Network Centrality  

---

<img width="748" alt="image" src="https://github.com/LastCodeBender42/Drug-Screening-Project/assets/159676076/b8eb6994-7c47-4904-a415-ebd186c66e50">

---
